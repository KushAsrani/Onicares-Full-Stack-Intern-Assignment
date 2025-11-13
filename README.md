# 📚 Onicares Full-Stack Library System

**Tech Stack:** NestJS • PostgreSQL • Prisma • React (TypeScript) • JWT Auth • Docker (optional)

---

## 🎯 Project Overview

This is a full-stack library management system built as part of the **Onicares Full-Stack Intern Assignment**.

It provides:

* CRUD for **Books**, **Authors**, and **Users**
* Borrow / Return flows
* JWT Authentication for protected routes
* RESTful APIs (NestJS + Prisma + PostgreSQL)
* Frontend built with React (TypeScript)

---

## 🧱 Tech Stack

| Layer            | Technology                         |
| ---------------- | ---------------------------------- |
| Backend          | NestJS (TypeScript)                |
| ORM              | Prisma                             |
| Database         | PostgreSQL                         |
| Authentication   | JWT                                |
| Frontend         | React (TypeScript)                 |
| Containerization | Docker / Docker Compose (optional) |

---

## 📁 Project Structure

```
onicares/
 ├── backend/
 │    ├── src/
 │    │    ├── auth/
 │    │    ├── books/
 │    │    ├── authors/
 │    │    ├── users/
 │    │    ├── borrows/
 │    │    └── prisma.service.ts
 │    ├── prisma/
 │    │    ├── schema.prisma
 │    │    ├── seed.ts
 │    │    └── prisma.config.ts
 │    ├── .env.example
 │    ├── Dockerfile
 │    ├── package.json
 │    └── README.md
 │
 ├── frontend/
 │    ├── src/
 │    ├── .env.example
 │    ├── vite.config.ts
 │    ├── package.json
 │    └── README.md
 │
 ├── docker-compose.yml (optional)
 └── README.md (this file)
```

---

## ⚙️ Environment Variables

Create a `.env` file in `/backend` based on `.env.example`:

```bash
DATABASE_URL="postgresql://postgres:postgres@localhost:5432/onicares?schema=public"
JWT_SECRET="supersecret"
JWT_EXPIRY="1h"
```

For the frontend, create `/frontend/.env`:

```bash
VITE_API_URL=http://localhost:3000
```

---

## 🚀 Backend Setup

### 1️⃣ Install dependencies

```bash
cd backend
npm install
```

### 2️⃣ Set up the database

Run PostgreSQL locally or via Docker:

```bash
docker run --name onicares-db \
  -e POSTGRES_USER=postgres \
  -e POSTGRES_PASSWORD=postgres \
  -e POSTGRES_DB=onicares \
  -p 5432:5432 -d postgres
```

### 3️⃣ Run Prisma migrations

```bash
npx prisma migrate dev --name init
```

### 4️⃣ Seed sample data

```bash
npx prisma db seed
```

### 5️⃣ Start backend

```bash
npm run start:dev
```

Backend will run on [http://localhost:3000](http://localhost:3000)

---

## 🧠 API Endpoints Overview

| Method        | Endpoint                 | Description                           | Auth   |
| ------------- | ------------------------ | ------------------------------------- | ------ |
| **Auth**      |                          |                                       |        |
| POST          | `/auth/register`         | Register user                         | Public |
| POST          | `/auth/login`            | Login & get JWT                       | Public |
| GET           | `/auth/me`               | Get current user                      | JWT    |
| **Authors**   |                          |                                       |        |
| GET           | `/authors`               | List authors                          | Public |
| GET           | `/authors/:id`           | Get author details                    | Public |
| POST          | `/authors`               | Create author                         | JWT    |
| PATCH         | `/authors/:id`           | Update author                         | JWT    |
| DELETE        | `/authors/:id`           | Delete author                         | JWT    |
| **Books**     |                          |                                       |        |
| GET           | `/books`                 | List books (filter by author, status) | Public |
| GET           | `/books/:id`             | Get book details                      | Public |
| POST          | `/books`                 | Add new book                          | JWT    |
| PATCH         | `/books/:id`             | Update book                           | JWT    |
| DELETE        | `/books/:id`             | Delete book                           | JWT    |
| **Borrowing** |                          |                                       |        |
| POST          | `/borrows`               | Borrow a book                         | JWT    |
| POST          | `/borrows/:id/return`    | Return a borrowed book                | JWT    |
| GET           | `/users/:userId/borrows` | List user’s borrows                   | JWT    |
| **Users**     |                          |                                       |        |
| GET           | `/users`                 | List users                            | JWT    |
| POST          | `/users`                 | Create user                           | JWT    |

---

## 🧾 Authentication

All write operations (POST/PATCH/DELETE) require a valid JWT token.

1️⃣ Register or login to get a token:

```bash
POST /auth/login
{
  "email": "admin@onicares.com",
  "password": "password123"
}
```

Response:

```json
{ "accessToken": "<your-jwt-token>" }
```

2️⃣ Add it to headers:

```
Authorization: Bearer <your-jwt-token>
```

---

## 💻 Frontend Setup

### 1️⃣ Install dependencies

```bash
cd frontend
npm install
```

### 2️⃣ Run development server

```bash
npm run dev
```

Frontend runs at [http://localhost:5173](http://localhost:5173) (Vite default).

---

## 🐳 Docker Setup (optional)

Build and run backend + database:

```bash
docker-compose up --build
```

If you use Docker, update your `.env` in backend:

```
DATABASE_URL="postgresql://postgres:postgres@db:5432/onicares?schema=public"
```

Then run migrations inside the backend container:

```bash
docker-compose exec backend npx prisma migrate deploy
```

---

## 🧪 Testing

You can add Jest tests under `/backend/test/`.

Run:

```bash
npm run test
```

---

## 📖 API Docs (Swagger)

If enabled in `main.ts`:

```bash
npm run start:dev
```

Then open:
👉 [http://localhost:3000/api](http://localhost:3000/api)

---

## 🧰 Developer Tips

* Run `npx prisma studio` to browse data visually
* Use `npx prisma generate` whenever you edit the schema
* Keep your `.env` file private and commit `.env.example`
* Add meaningful error handling using `PrismaExceptionFilter`

---

## 🎥 Deliverables (for submission)

* ✅ GitHub repository containing backend + frontend
* ✅ Working APIs and functional frontend
* ✅ Demo video (show CRUD + borrow flow)
* ✅ `.env.example` file
* ✅ Clear README (this file)
* ✅ (Optional) Docker setup and Swagger documentation

---

## 🏁 Evaluation Criteria

| Criteria                        | Weight |
| ------------------------------- | ------ |
| Functional correctness          | ✅      |
| Schema design & relationships   | ✅      |
| Code quality / TypeScript usage | ✅      |
| Authentication (JWT)            | ✅      |
| Documentation (README)          | ✅      |
| UI functionality                | ✅      |
| Bonus (Docker, Swagger, Tests)  | ⭐      |

---
