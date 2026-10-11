# CareerForgeAI — AI Career Coach

Live: **https://careerforgeai.vercel.app/**

AI-powered career platform to accelerate your job search: real-time industry insights, ATS-optimized resume builder, AI cover letters, and role-specific interview prep with performance tracking.

## What it does (in short)

CareerForgeAI onboards you by industry + experience, then gives you 4 core tools:

1. **Industry Insights Dashboard** — salary ranges, growth rate, demand level, top skills, market outlook, key trends. Auto-refreshed weekly via Inngest + Gemini.
2. **Smart Resume Builder** — Markdown-based builder with ATS score + feedback, PDF export.
3. **AI Cover Letter Generator** — job-tailored letters (company, title, JD) with preview + dashboard management.
4. **Interview Prep** — AI-generated role-specific quizzes, instant scoring, improvement tips, stats cards + performance charts + history.

Plus: Clerk auth, dark/light mode, protected routes, landing page with features / how-it-works / FAQs.

## Tech Stack

- **Frontend:** Next.js 15 (App Router, Turbopack), React 19, Tailwind CSS, shadcn/ui, Lucide, Recharts, react-hook-form + zod, next-themes
- **Auth:** Clerk (`@clerk/nextjs`)
- **DB/ORM:** PostgreSQL + Prisma (`User, Assessment, Resume, CoverLetter, IndustryInsight`)
- **AI:** Google Gemini (`@google/generative-ai`)
- **Background Jobs:** Inngest (weekly industry-insight refresh)
- **Deploy:** Vercel

## Project Structure

```
app/
  page.js                 # landing page
  (auth)/sign-in, sign-up # clerk auth
  (main)/dashboard       # industry insights
  (main)/resume          # resume builder
  (main)/ai-cover-letter # generator + [id] view + new
  (main)/interview       # quiz + mock + results
  (main)/onboarding      # industry select
  api/inngest            # background job endpoint
actions/  # user.js, dashboard.js, resume.js, cover-letter.js, interview.js
lib/      # prisma.js, checkUser.js, inngest/
data/     # industries.js, features.js, faqs.js, howItWorks.js
prisma/schema.prisma
components/ui/  # shadcn
```

## Getting Started

### 1. Prerequisites
Node.js 18+, PostgreSQL DB, Clerk account, Gemini API key.

### 2. Install
```bash
npm install
```

### 3. Env — create `.env`:
```env
DATABASE_URL="postgresql://..."
NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY=...
CLERK_SECRET_KEY=...
NEXT_PUBLIC_CLERK_SIGN_IN_URL=/sign-in
NEXT_PUBLIC_CLERK_SIGN_UP_URL=/sign-up
GEMINI_API_KEY=...
```

### 4. DB
```bash
npx prisma migrate dev
npx prisma generate
```

### 5. Run
```bash
npm run dev
# + in separate terminal for background jobs:
npx inngest-cli@latest dev
```
Open http://localhost:3000

Build: `npm run build && npm start`

## Key Env / Services
- Clerk middleware protects `/dashboard, /resume, /interview, /ai-cover-letter, /onboarding`
- Inngest function `generate-industry-insights` runs weekly, updates `IndustryInsight` table.

## Roadmap Ideas
- Job tracker, LinkedIn optimizer, salary negotiator, learning paths, multi-resume versions.

---
Built with Next.js + Gemini + Clerk + Prisma.
