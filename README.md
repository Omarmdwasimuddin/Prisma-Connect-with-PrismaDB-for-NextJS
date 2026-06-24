# Prisma Install with Next.js
---
## ১. Next.js Installation
নতুন Next.js প্রজেক্ট তৈরি করো এবং সেই ডিরেক্টরিতে প্রবেশ করো:
```bash
npx create-next-app@latest prisma-schema
cd prisma-schema
```
---
## ২. Prisma Dependencies Install
### Dev dependencies:
```bash
npm install prisma tsx @types/pg --save-dev
```
### Production dependencies:
```bash
npm install @prisma/client @prisma/adapter-pg dotenv pg
```
---
## ৩. Prisma Initialize করো
প্রজেক্টে Prisma সেটআপ করতে নিচের কমান্ড রান করো:
```bash
npx prisma init
```
এই কমান্ড চালালে যা তৈরি হবে:
| ফাইল / ডিরেক্টরি | বিবরণ |
|---|---|
| `prisma/schema.prisma` | Prisma schema ফাইল |
| `prisma.config.ts` | Prisma কনফিগারেশন ফাইল |
| `.env` | `DATABASE_URL` সহ environment file |
| `app/generated/prisma/` | Generated Prisma Client (পরে তৈরি হবে) |
> ⚠️ `app/generated/prisma` ডিরেক্টরি তখনই তৈরি হবে যখন `prisma generate` অথবা `prisma migrate dev` রান করবে।
---
## ৪. Database তৈরি করো
Prisma Postgres database তৈরি করতে রান করো:
```bash
npx create-db
```
![Database Creation](https://imgur.com/QTFm05H.png)
> ✅ কমান্ড সফল হলে একটি `postgres://...` connection string পাবে।  
> সেটি কপি করে `.env` ফাইলের `DATABASE_URL` এ পেস্ট করো।
**`.env` ফাইল উদাহরণ:**
```env
DATABASE_URL="postgres://your-connection-string-here"
```
---
## ৫. Schema কনফিগার করো
`prisma/schema.prisma` ফাইলটি খুলে নিচের মতো করে কনফিগার করো:
```prisma
generator client {
  provider = "prisma-client-js"
  output   = "../app/generated/prisma"
}

datasource db {
  provider = "postgresql"
}

model User {
  id    Int     @id @default(autoincrement())
  email String  @unique
  name  String?
  posts Post[]
}

model Post {
  id        Int     @id @default(autoincrement())
  title     String
  content   String?
  published Boolean @default(false)
  authorId  Int
  author    User    @relation(fields: [authorId], references: [id])
}
```

| অংশ | বিবরণ |
|---|---|
| `generator client` | Prisma Client কোথায় generate হবে তা নির্ধারণ করে |
| `output = "../app/generated/prisma"` | Next.js-এর `app/generated/prisma/` ফোল্ডারে Client তৈরি হবে |
| `datasource db` | PostgreSQL database ব্যবহার করা হবে |
| `model User` | ইউজার টেবিল — `id`, `email`, `name` এবং `posts` relation |
| `model Post` | পোস্ট টেবিল — `author` এর সাথে foreign key relation আছে |

> ✅ `User` এবং `Post` এর মধ্যে **one-to-many** relation রয়েছে — একজন User অনেকগুলো Post রাখতে পারবে।
---
## ৬. Migration চালাও এবং Prisma Client Generate করো
```bash
npx prisma migrate dev --name init
npx prisma generate
```
| কমান্ড | কাজ |
|---|---|
| `prisma migrate dev --name init` | Database-এ table তৈরি করে এবং migration history রাখে |
| `prisma generate` | Prisma Client কোড generate করে |
---
## ৭. Prisma Studio দিয়ে Verify করো
Database-এ table তৈরি হয়েছে কিনা চেক করতে:
```bash
npx prisma studio
```
Browser-এ `http://localhost:5555` এ Prisma Studio খুলবে।
![Prisma Studio](https://imgur.com/ZycYnKw.png)
> ✅ যদি table দেখতে পাও, তাহলে সেটআপ সফলভাবে সম্পন্ন হয়েছে!
---
## Quick Summary
```
create-next-app
     ↓
npm install (prisma, pg, client)
     ↓
prisma init
     ↓
create-db → .env তে DATABASE_URL পেস্ট
     ↓
schema.prisma কনফিগার করো (User + Post model)
     ↓
prisma migrate dev
     ↓
prisma generate
     ↓
prisma studio → verify ✅
```
