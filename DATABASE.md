# Database Schema

## Overview

The Society Maintenance Tracker uses SQLite as its database.

The database stores users, complaints, complaint history, and society notices.

The database file is configured through the `DB_FILE` environment variable.

---

## 1. Users Table

The `users` table stores resident and administrator accounts.

| Column | Type | Description |
|---|---|---|
| id | INTEGER | Primary key |
| name | TEXT | User's full name |
| email | TEXT | Unique email address |
| password_hash | TEXT | Hashed password |
| role | TEXT | `resident` or `admin` |
| created_at | DATETIME | Account creation timestamp |

A user can create multiple complaints, complaint history records, and notices.

---

## 2. Complaints Table

The `complaints` table stores maintenance complaints raised by residents.

| Column | Type | Description |
|---|---|---|
| id | INTEGER | Primary key |
| user_id | INTEGER | Resident who created the complaint |
| category | TEXT | Complaint category |
| description | TEXT | Description of the issue |
| photo_path | TEXT | Path of uploaded complaint photo |
| priority | TEXT | `Low`, `Medium`, or `High` |
| status | TEXT | `Open`, `In Progress`, or `Resolved` |
| created_at | DATETIME | Complaint creation timestamp |
| resolved_at | DATETIME | Resolution timestamp |

Foreign key:

`user_id → users.id`

---

## 3. Complaint History Table

The `complaint_history` table stores every status change made to a complaint.

| Column | Type | Description |
|---|---|---|
| id | INTEGER | Primary key |
| complaint_id | INTEGER | Related complaint |
| status | TEXT | Status after the update |
| actor_id | INTEGER | User who performed the action |
| note | TEXT | Optional administrator note |
| created_at | DATETIME | Time of the status change |

Foreign keys:

`complaint_id → complaints.id`

`actor_id → users.id`

This provides an audit trail of the complaint lifecycle.

---

## 4. Notices Table

The `notices` table stores announcements published by administrators.

| Column | Type | Description |
|---|---|---|
| id | INTEGER | Primary key |
| title | TEXT | Notice title |
| body | TEXT | Notice content |
| important | BOOLEAN | Whether the notice is important |
| created_by | INTEGER | Administrator who created the notice |
| created_at | DATETIME | Notice creation timestamp |

Foreign key:

`created_by → users.id`

---

## 5. Entity Relationships

```text
users
  |
  |----< complaints
  |
  |----< complaint_history
  |
  |----< notices

complaints
  |
  |----< complaint_history
