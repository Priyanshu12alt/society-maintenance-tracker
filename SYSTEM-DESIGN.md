# System Design – Society Maintenance Tracker

## Overview

Society Maintenance Tracker is a web application that allows residents to raise and track maintenance complaints while administrators manage complaints, update their status, monitor overdue issues, and publish society notices.

The system uses a React + Vite frontend, Node.js + Express backend, SQLite database, JWT authentication, Multer for photo uploads, and Nodemailer for email notifications.

---

## 1. Complaint History Model

Each complaint follows a simple lifecycle:

```text
Open → In Progress → Resolved
