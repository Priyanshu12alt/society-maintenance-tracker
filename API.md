# Society Maintenance Tracker API Documentation

## Base URL

For local development:

http://localhost:4000/api

The production frontend uses the deployed backend URL configured through the `VITE_API_URL` environment variable.

---

# 1. Health Check

## GET /api/health

Checks whether the backend API is running.

### Request

No authentication required.

### Response

```json
{
  "name": "John Doe",
  "email": "john@example.com",
  "password": "Password123"
}
{
  "id": 2
}
{
  "email": "admin@society.local",
  "password": "Admin@123"
}
{
  "token": "<JWT_TOKEN>",
  "user": {
    "id": 1,
    "name": "Society Admin",
    "email": "admin@society.local",
    "role": "admin"
  }
}
{
  "id": 1,
  "name": "Society Admin",
  "email": "admin@society.local",
  "role": "admin"
}
category: Plumbing
description: Water leakage in the bathroom
photo: bathroom.jpg
{
  "status": "In Progress",
  "priority": "High",
  "note": "Maintenance team has been assigned."
}
{
  "ok": true
}
[
  {
    "id": 1,
    "complaint_id": 1,
    "status": "Open",
    "actor_id": 2,
    "actor_name": "John Doe",
    "note": "Complaint created",
    "created_at": "2026-08-24 10:00:00"
  }
]
{
  "title": "Water Supply Maintenance",
  "body": "Water supply will be unavailable from 10 AM to 2 PM.",
  "important": true
}
{
  "byStatus": [
    {
      "status": "Open",
      "count": 5
    },
    {
      "status": "In Progress",
      "count": 3
    },
    {
      "status": "Resolved",
      "count": 10
    }
  ],
  "byCategory": [
    {
      "category": "Plumbing",
      "count": 6
    },
    {
      "category": "Electrical",
      "count": 4
    }
  ],
  "overdue": 2
}
Administrator updates complaint
            |
            v
Complaint status updated
            |
            v
Complaint history recorded
            |
            v
Resident email retrieved
            |
            v
Notification email sent
Administrator creates important notice
            |
            v
Notice stored in database
            |
            v
Resident email addresses retrieved
            |
            v
Notification email sent
{
  "ok": true
}
