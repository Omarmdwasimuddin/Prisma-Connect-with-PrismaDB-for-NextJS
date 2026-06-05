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
