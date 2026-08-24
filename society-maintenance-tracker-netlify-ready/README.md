# Society Maintenance Tracker

A complete resident/admin maintenance complaint platform based on the supplied project brief. The brief requires resident registration/login, complaint creation with optional photos, status history, admin filtering/priority/status management, overdue detection, notice board, email updates, dashboard, role-based auth, API/database documentation and deployment guidance. fileciteturn0file0L10-L41

## Stack
- Frontend: React 19 + Vite
- Backend: Node.js + Express
- Database: SQLite (better-sqlite3)
- Auth: JWT + bcrypt
- Uploads: Multer, 5 MB image limit
- Email: Nodemailer; if SMTP is not configured, emails are logged as `[EMAIL MOCK]`

## Local setup
1. Install Node.js 20+.
2. From the project root run `npm install` (for concurrently) and `npm run install:all`.
3. Copy `backend/.env.example` to `backend/.env` and change `JWT_SECRET`.
4. Run `npm run dev`.
5. Open `http://localhost:5173`.

Default admin:
- Email: `admin@society.local`
- Password: `Admin@123`

## API
- `POST /api/auth/register` resident registration
- `POST /api/auth/login` login
- `GET /api/me` current user
- `GET /api/complaints` resident own / admin all, with `category`, `status`, `date` filters
- `POST /api/complaints` resident complaint + optional image
- `GET /api/complaints/:id` complaint + complete history
- `GET /api/complaints/:id/history` history only
- `PATCH /api/complaints/:id` admin status/priority/note
- `GET /api/notices` notice board
- `POST /api/notices` admin notice
- `GET /api/dashboard` admin dashboard
- `GET /api/health` health check

All protected endpoints use `Authorization: Bearer <JWT>`.

## Database schema
`users` stores residents/admins. `complaints` stores the current state and optional photo path. `complaint_history` stores every status transition with timestamp, actor and note. `notices` stores announcements and the important/pinned flag. Foreign keys preserve complaint/history ownership.

## Overdue logic
The configurable `OVERDUE_DAYS` value defaults to 7. On complaint reads/dashboard refresh, unresolved complaints older than the threshold are flagged overdue and sorted first in the admin complaint list. Resolved complaints are never overdue.

## Photo handling
Images are accepted through multipart upload and stored under `backend/uploads`. Only image MIME types are accepted and files are limited to 5 MB. The complaint stores the relative URL path.

## Notification flow
When an admin changes a complaint status, the backend sends an email to the resident. When an admin posts an important notice, every resident receives an email. Without SMTP configuration the app logs the email payload so the full workflow remains testable locally.

## Deployment
Deploy backend and frontend separately on Render/Railway/Vercel or similar. Set the frontend `VITE_API_URL` to the deployed backend `/api` URL and set backend environment variables. For production, use managed object storage for uploads and a managed database rather than local SQLite/filesystem if multiple instances are used.

## Project structure
```
backend/
  src/server.js
  .env.example
frontend/
  src/main.jsx
  src/style.css
README.md
```
