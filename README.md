# Full-Stack SaaS AI Platform

A SaaS AI platform built with **Next.js 13**, React, Tailwind, Prisma, and Stripe. Users can access several AI services (with rate limits and optional Pro subscription): conversation (e.g. GPT-4-style chat), image generation, video generation, music generation, and code generation. Free tier is limited to a small number of requests; Pro is managed via Stripe (test mode). Authentication is handled with **Clerk**; the UI uses **shadcn** components. Customer support/live chat can be integrated with **Crisp**.

## Features

- Tailwind-based design, animations, and responsive layout
- **Clerk** authentication (email, Google, and other social logins)
- Client-side forms and validation with **react-hook-form**
- Server-side error feedback with **react-toast**
- **OpenAI:** conversation, code, and image generation
- **Replicate:** music and video generation
- Loading states and Stripe monthly subscription with free-tier limits
- Route handlers: POST, DELETE, GET in `app/api`
- Server components reading from the database without extra API layers
- Shared layouts and Next 13 App Router structure

## Prerequisites and dependencies

- Create the app:  
  `npx create-next-app@latest ai-saas --typescript --tailwind --eslint`
- Init shadcn (e.g. base color `slate`):  
  `npx shadcn-ui@latest init`
- Add components:  
  `npx shadcn-ui@latest add button sheet card form input avatar select progress dialog badge`
- **Clerk:** `npm i @clerk/nextjs`, wrap the app with the Clerk provider, add `middleware.ts` (see Clerk docs). Create sign-up and sign-in routes, e.g. `/sign-up/[[...sign-up]]/page.tsx` and `/sign-in/[[...sign-in]]/page.tsx`.
- **Forms:** `npm i @hookform/resolvers react-hook-form` (with Zod).
- **OpenAI:** `npm i openai` for conversation, code, and image APIs.
- **Markdown:** `npm i react-markdown` for rendering code in the code-generation UI.
- **Replicate:** `npm i replicate` for music and video generation.
- **Prisma:** `npm i -D prisma`, `npx prisma init`, `npm i @prisma/client`, then `npx prisma db push` and `npx prisma generate`. Optional: `npx prisma studio`. Reset DB: `npx prisma migrate reset`.
- **State:** `npm i zustand` (e.g. for free-tier counter and Pro upgrade modal).
- **Toasts:** `npm i react-hot-toast`.
- **Crisp:** `npm i crisp-sdk-web` and wrap the app body with the Crisp provider.
- **Landing:** `npm i typewriter-effect` for the typing effect.

**Node:** 18.x.x recommended.

## Environment

Create a `.env` file (example):

```env
NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY=
CLERK_SECRET_KEY=

NEXT_PUBLIC_CLERK_SIGN_IN_URL=/sign-in
NEXT_PUBLIC_CLERK_SIGN_UP_URL=/sign-up
NEXT_PUBLIC_CLERK_AFTER_SIGN_IN_URL=/dashboard
NEXT_PUBLIC_CLERK_AFTER_SIGN_UP_URL=/dashboard

OPENAI_API_KEY=
REPLICATE_API_TOKEN=

DATABASE_URL=

STRIPE_API_KEY=
STRIPE_WEBHOOK_SECRET=

NEXT_PUBLIC_APP_URL="http://localhost:3000"
```

## Database (Prisma)

Use a MySQL-compatible database (e.g. PlanetScale):

```bash
npx prisma db push
```

## Run the app

```bash
npm run dev
```

## Commands

| Command | Description        |
|--------|--------------------|
| `npm run dev` | Start development server |

## Replicate AI

- **Music:** Riffusion model.
- **Video:** e.g. zeroscope/anotherjesse model.

## Data and subscriptions

Prisma ORM is used for users and subscriptions; the example uses MySQL (e.g. PlanetScale) as the database provider.
