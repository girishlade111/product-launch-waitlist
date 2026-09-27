# Product Launch Waitlist

A product-launch waitlist landing page with email signup. Visitors join the waitlist with their email, which is stored in Upstash Redis and confirmed with a welcome email sent via Resend — all powered by Next.js Server Actions.

## What it does

- **Waitlist signup form** — email input with zod validation
- **Redis-backed storage** — emails stored in an Upstash Redis set (`waitlist_emails`)
- **Welcome email** — confirmation email rendered from a React email template, sent via Resend
- **Live waitlist count** — shows how many people have signed up
- **Social links** — Discord, X, Instagram, LinkedIn, Facebook icons
- **Light/dark theme** — theme toggle via next-themes
- **Toast feedback** — success/error toasts on signup

## Tech stack

- **Framework:** Next.js 15 (App Router, Server Actions)
- **Language:** TypeScript
- **UI:** React 19, Tailwind CSS, shadcn/ui (Radix primitives)
- **Database:** Upstash Redis (`@upstash/redis`)
- **Email:** Resend (`resend` + React email template)
- **Validation:** zod
- **Package manager:** pnpm

## Quick start

```bash
# install dependencies
pnpm install
# or: npm install --legacy-peer-deps

# copy the example env file and fill in values
cp .env.example .env.local

# run the dev server
pnpm dev        # http://localhost:3000

# production build + start
pnpm build
pnpm start
```

## Project structure

```
app/
  page.tsx                    # landing page
  layout.tsx                  # root layout
  actions/
    waitlist.ts               # 'use server' action: validate email, store in Redis, send welcome email
  lib/
    redis.ts                  # Upstash Redis client
  components/
    waitlist-form.tsx         # signup form (uses server action)
    waitlist-signup.tsx       # signup card wrapper
    email-template.tsx        # Resend welcome-email template
    avatar.tsx, social-icon.tsx, icons/  # social icons
    ui/                       # shadcn/ui primitives
lib/
  utils.ts                    # cn() classnames helper
public/                       # static assets
```

## Environment variables

Create a `.env.local` (or set these in your hosting provider):

| Variable | Purpose |
|---|---|
| `UPSTASH_REDIS_REST_URL` | Upstash Redis REST endpoint |
| `UPSTASH_REDIS_REST_TOKEN` | Upstash Redis REST token |
| `RESEND_API_KEY` | Resend API key for sending welcome emails |

## Deployment

This app requires a Node.js server (Server Actions) plus Upstash Redis and a Resend key — it cannot be statically exported to GitHub Pages.

- **Vercel (recommended, original v0 deployment):** set the three env vars above in the project settings, then deploy.

Originally generated with [v0.app](https://v0.app).

## License

Open source — free to use and modify.

---

Built by Girish Lade — https://ladestack.in
