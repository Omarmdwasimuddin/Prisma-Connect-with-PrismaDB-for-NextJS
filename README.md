## Prisma-Install-with-NextJs

### Nextjs Installation
```bash
npx create-next-app@latest prisma-schema
cd prisma-schema
```
---

### Prisma Install dependencies
```bash
npm install prisma tsx @types/pg --save-dev
npm install @prisma/client @prisma/adapter-pg dotenv pg
```
---

### Initialize Prisma in your project
```bash
npx prisma init --output ../app/generated/prisma
```
---

This will create:

- A prisma directory with a schema.prisma file.
- A prisma.config.ts file for configuring Prisma.
- A .env file containing a local DATABASE_URL at the project root.

The app/generated/prisma output directory for the generated Prisma Client will be created when you run prisma generate or prisma migrate dev in a later step.

### Create a Prisma Postgres database and replace the generated DATABASE_URL in your .env file with the postgres://... connection string from the CLI output:
```bash
npx create-db
```
---

### Run migrations and generate Prisma Client
```bash
npx prisma migrate dev --name init
npx prisma generate
```
---
