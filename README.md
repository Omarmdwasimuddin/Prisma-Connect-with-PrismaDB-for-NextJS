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
