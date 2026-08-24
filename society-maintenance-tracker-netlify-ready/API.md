# API Documentation

Base URL: `http://localhost:4000/api`

## Authentication
`POST /auth/register` — `{name,email,password}`

`POST /auth/login` — `{email,password}` → `{token,user}`

Protected requests use `Authorization: Bearer <token>`.

## Complaints
`GET /complaints` — resident gets own complaints; admin gets all. Optional query parameters: `category`, `status`, `date`.

`POST /complaints` — resident multipart form: `category`, `description`, optional `photo`.

`GET /complaints/:id` — complaint and full history.

`GET /complaints/:id/history` — history entries.

`PATCH /complaints/:id` — admin JSON `{status,priority,note}`. Valid status values: `Open`, `In Progress`, `Resolved`. Priority values: `Low`, `Medium`, `High`.

## Notices
`GET /notices` — all notices, important first.

`POST /notices` — admin JSON `{title,body,important}`.

## Dashboard
`GET /dashboard` — admin only; returns `byStatus`, `byCategory`, and `overdue`.

`GET /health` — health check.
