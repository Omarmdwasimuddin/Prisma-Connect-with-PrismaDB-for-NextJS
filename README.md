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
npx prisma init --output ../app/generated/prisma
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

## ৫. Migration চালাও এবং Prisma Client Generate করো

```bash
npx prisma migrate dev --name init
npx prisma generate
```

| কমান্ড | কাজ |
|---|---|
| `prisma migrate dev --name init` | Database-এ table তৈরি করে এবং migration history রাখে |
| `prisma generate` | Prisma Client কোড generate করে |

---

## ৬. Prisma Studio দিয়ে Verify করো

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
prisma migrate dev
     ↓
prisma generate
     ↓
prisma studio → verify ✅
```
