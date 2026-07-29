# Vertex Ops

Commercial-style Mini ERP + CRM operations portal for wholesale and distribution teams. It combines customer management, product stock, audit-ready inventory movements, and a transactional sales-challan workflow.

## What is included

- Premium responsive React/Vite dashboard with charts, operational KPIs, activity feed, dark mode, and challan modal
- Express + TypeScript REST API with JWT authentication, role checks, Zod validation, standard response envelopes, and centralized errors
- PostgreSQL Prisma schema covering users, customers, products, stock movements, challans, line-item snapshots, and follow-ups
- Atomic challan confirmation: rejects negative inventory, reduces stock, and creates audit records in one transaction
- Docker Compose, Render blueprint, Vercel SPA configuration, seed data, ERD, and Postman collection

## Quick start

```bash
cp backend/.env.example backend/.env
npm install
npx prisma migrate dev --schema backend/prisma/schema.prisma --name init
npm run seed
npm run dev
```

Visit `http://localhost:5173`; API is at `http://localhost:4000`. Demo users use password `Demo@123`: `admin@vertexops.dev`, `sales@vertexops.dev`, `warehouse@vertexops.dev`, and `accounts@vertexops.dev`.

## Roles

| Role | Access |
|---|---|
| Admin | Full system access |
| Sales | Customers and challans |
| Warehouse | Products and inventory |
| Accounts | Reserved for reporting/invoicing |

## API

All protected endpoints require `Authorization: Bearer <token>`. API responses are `{ success, message, data }`.

- `POST /api/auth/login`
- `GET|POST|PATCH|DELETE /api/customers`
- `GET|POST|PATCH|DELETE /api/products`
- `POST /api/challans`
- `POST /api/challans/:id/confirm`

See [the ER diagram](docs/ERD.md) and import `docs/Vertex-Ops.postman_collection.json` into Postman. For deployment, provision Neon and set `DATABASE_URL` and `JWT_SECRET` in Render; set your API URL in the frontend environment for a full production integration.
