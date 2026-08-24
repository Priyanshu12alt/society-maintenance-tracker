# Society Maintenance Tracker

A resident/admin maintenance complaint platform for managing society complaints, status tracking, notices, and administrative workflows.

## Tech Stack

- Frontend: React + Vite
- Backend: Node.js + Express
- Database: SQLite
- Authentication: JWT + bcrypt
- File uploads: Multer
- Email: Nodemailer

## Features

### Resident

- Register and log in
- Raise maintenance complaints
- Select complaint category
- Set complaint priority
- Upload an optional photo
- View complaint status
- View complaint history
- View notice board

### Admin

- Admin dashboard
- View all complaints
- Filter complaints by category/status/date
- Change complaint status
- Change priority
- Add admin notes
- Track complaint history
- Detect overdue complaints
- Publish notices
- Send notification emails

## Local Setup

### 1. Install dependencies

From the project root:

```bash
npm install
npm run install:all
