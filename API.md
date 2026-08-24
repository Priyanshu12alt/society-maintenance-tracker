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
  "ok": true
}
