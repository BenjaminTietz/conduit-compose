# Conduit Containerized

## Table of Contents

1. [Introduction](#introduction)
2. [Project Structure](#project-structure)
3. [Quickstart](#quickstart)
4. [Environment Variables](#environment-variables)
5. [Usage](#usage)
6. [Contact](#contact)
7. [Checklist](checklist.pdf)

---

## Introduction

This repository provides a fully containerized setup for the **Conduit** full‑stack application  
(Angular frontend + Django REST backend) using Docker Compose.  
It demonstrates a practical containerization setup using Docker Compose,
with a focus on understanding how frontend and backend services
communicate in a real-world (and partly legacy) project.

---

## ⚠️ Legal & Hosting Notice

This project is intended for educational and local development purposes only.

It is **not suitable for public hosting or production use**, as it does not
provide any GDPR-compliant features such as:

- Privacy policy
- Legal notice / imprint
- Consent handling for personal data

Do not deploy or expose this application publicly without adding the
required legal and compliance-related components.

## Project Structure

```
conduit-container/
├── docker-compose.yaml
├── .env.template          # Template for environment variables
├── .gitmodules           # Submodules: backend + frontend
├── backend/              # Django backend (git submodule)
├── frontend/             # Angular frontend (git submodule)
└── README.md
```

---

## Quickstart

### 1. Clone the repository (including submodules)

```sh
git clone --recurse-submodules https://github.com/BenjaminTietz/conduit-container.git
cd conduit-container
```

If you forgot `--recurse-submodules`:

```sh
git submodule update --init --recursive
```

---

### 2. Create your environment file

```sh
cp .env.example .env
```

Modify if needed.

---

### 3. Start the full stack

```sh
docker-compose up --build
```

Backend → http://localhost:8000  
Frontend → http://localhost:8282

---

## Frontend (Angular) – Configuration Note

The Angular frontend uses a static environment configuration.

After cloning the repositories, the backend API base URL must be updated
manually in the frontend environment file:

Example:

```ts
export const environment = {
  apiUrl: "http://backend:8000/api",
};
```

This is a deliberate design choice for this legacy project to keep changes
minimal and make configuration explicit at the application level.

## Environment Variables

The container uses `.env` to configure Django and PostgreSQL:

```env
DJANGO_SECRET_KEY=changeme
DJANGO_DEBUG=True
DJANGO_ALLOWED_HOSTS=*

CORS_ALLOWED_ORIGINS=http://localhost:8282,http://127.0.0.1:8282

DB_NAME=conduit
DB_USER=postgres
DB_PASSWORD=changeme
DB_HOST=db
DB_PORT=5432
```

---

## Usage

### Backend (Django)

Run inside the backend container:

```
docker exec -it conduit_backend bash
python manage.py createsuperuser
```

---

### Frontend (Angular)

The production build is embedded in an NGINX container and served at:

```
http://localhost:8282
```

---

## Logging

All services log to stdout/stderr and are managed by Docker's json-file logging driver.
Log rotation is enabled to prevent excessive disk usage.

Logs can be accessed via:

```bash
docker logs backend
docker logs frontend
```

## Contact

### 👤 Personal

- Portfolio: https://benjamin-tietz.com
- Mail: mail@benjamin-tietz.com

### 🌍 Social

- LinkedIn: https://www.linkedin.com/in/benjamin-tietz/

### 💻 Project Repository

- https://github.com/BenjaminTietz/conduit-container

```

```
