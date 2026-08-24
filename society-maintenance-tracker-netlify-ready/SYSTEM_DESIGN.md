# System Design — Society Maintenance Tracker

## 1. Complaint history model
The application separates the current complaint state from its immutable status history. A `complaints` row stores the resident, category, description, optional photo path, current priority, current status, creation/resolution timestamps and the computed overdue flag. Every status transition creates a `complaint_history` row containing the complaint ID, new status, actor ID, optional note and timestamp. The initial `Open` state is also recorded as the first history event. This design makes the resident timeline and audit trail straightforward while keeping list queries fast because the current status and priority are available directly on the complaint row. The history table is linked with a foreign key and cascade delete.

## 2. Overdue detection
The overdue threshold is configurable through `OVERDUE_DAYS` and defaults to seven days. Before complaint-list and dashboard reads, the backend updates the overdue flag for unresolved complaints whose age exceeds the configured threshold. Resolved complaints are explicitly cleared from overdue status. The admin complaint query sorts overdue records first, followed by priority and newest records. This makes the most urgent operational work visible without requiring a background scheduler. In a larger deployment, the same rule can be moved to a scheduled job while retaining the database flag for fast filtering.

## 3. Photo handling
Residents submit complaints as `multipart/form-data`. Multer accepts only image MIME types and limits files to 5 MB. Files are written to the backend `uploads` directory and the complaint stores a relative `/uploads/...` path. Express serves this directory as static content. The API does not accept arbitrary file types. For production on a multi-instance host, local filesystem storage should be replaced with object storage such as S3-compatible storage, while the database continues to store the resulting object URL/key.

## 4. Notification flow
Authentication identifies the resident or admin with a signed JWT. When an admin changes a complaint status, the backend creates the history record and then sends an email to the complaint owner's email address. When an admin creates an important notice, the notice is stored with `important=1` and every resident is notified. Nodemailer is used for SMTP integration. If SMTP variables are not configured, the same notification flow logs an `[EMAIL MOCK]` message, allowing local testing without an external mail service.

## 5. Roles, API and dashboard
Residents can register, log in, create complaints and view only their own complaints/history. Admins can view all complaints, filter them by category/status/date, change priority/status, post notices and access dashboard aggregates. Role middleware is enforced server-side rather than relying only on the UI. The dashboard returns complaint totals grouped by status and category plus the overdue count. The frontend consumes a small REST API and keeps the JWT in local storage for this demo; production deployments can move to secure HTTP-only cookies.
