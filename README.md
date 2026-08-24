# Society Maintenance Tracker

A resident/admin maintenance complaint platform for managing society complaints, status tracking, notices, and administrative workflows.

## Tech Stack

- **Frontend:** React + Vite
- **Backend:** Node.js + Express
- **Database:** SQLite
- **Authentication:** JWT + bcrypt
- **File uploads:** Multer
- **Email notifications:** Nodemailer

## Features

### Resident

- Register and log in
- Raise maintenance complaints
- Select complaint category
- Set complaint priority
- Upload an optional photo
- View complaint status
- View complaint history
- View society notices

### Admin

- Admin dashboard
- View all complaints
- Filter complaints by category, status, and date
- Change complaint status
- Change complaint priority
- Add administrator notes
- Track complaint history
- Detect overdue complaints
- Publish society notices
- Send notification emails

## System Architecture

```text
                    React + Vite Frontend
                              |
                              | REST API / HTTP
                              v
                    Node.js + Express
                              |
              +---------------+---------------+
              |               |               |
              v               v               v
           SQLite           Multer        Nodemailer
          Database       Photo Upload    Email Notifications
