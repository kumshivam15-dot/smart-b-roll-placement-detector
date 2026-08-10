# Next-Gen Learning Dashboard

A high-fidelity student dashboard prototype for the Frontend Intern Challenge. It uses Next.js App Router, Supabase server-side data fetching, Tailwind CSS, Framer Motion, and Lucide React.

## Stack

- Next.js App Router with TypeScript
- Supabase PostgreSQL via `@supabase/supabase-js`
- Tailwind CSS v4
- Framer Motion for staggered entry, spring hover states, progress animation, and sidebar `layoutId` highlights
- Lucide React icons rendered dynamically from the `icon_name` database field

## Included Features

- Bento dashboard with hero, course, activity, focus, and upcoming lesson tiles
- Collapsible desktop/tablet sidebar and fixed mobile bottom navigation
- Framer Motion staggered page load, spring hover states, animated progress bars, and `layoutId` nav highlights
- Supabase Server Component data fetching with typed payloads
- Missing-env and database-error fallback state with demo rows
- Empty course state for valid Supabase connections with no rows
- `loading.tsx`, Suspense skeletons, `error.tsx`, and `not-found.tsx`
- Idempotent Supabase seed SQL, `robots.ts`, and `sitemap.ts`
- Submission-safe `.gitignore` and `.env.example`

## Getting Started

```bash
npm install
cp .env.example .env.local
npm run dev
```

Open [http://localhost:3000](http://localhost:3000).

## Quality Checks

```bash
npm run lint
npm run typecheck
npm run build
```

## Supabase Setup

1. Create a free Supabase project.
2. Open the SQL editor and run `supabase/seed.sql`.
3. Copy your project URL and anon key into `.env.local`:

```bash
NEXT_PUBLIC_SUPABASE_URL=https://your-project-ref.supabase.co
NEXT_PUBLIC_SUPABASE_ANON_KEY=your-anon-key
```

Do not commit `.env.local`.

## Architecture Notes

The page at `app/page.tsx` is a Server Component. It renders the dashboard shell and fetches courses through `lib/courses.ts`, which creates a server-side Supabase client from environment variables. Course data is never hardcoded into the course UI; if Supabase is missing or unavailable, the app returns a graceful warning tile plus demo rows so reviewers can still inspect the interface locally.

Framer Motion is isolated to client components: `components/bento.tsx`, `components/sidebar.tsx`, and `components/course-card.tsx`. This keeps the server/client split small while still meeting the animation requirements. The bento grid staggers tiles into view, each tile uses transform-only hover elevation, progress bars animate from `scaleX: 0`, and sidebar active states use `layoutId` transitions.

Loading and failure states are covered by `app/loading.tsx`, `components/skeletons.tsx`, and `app/error.tsx`. Skeleton tiles use fixed dimensions so loading states do not resize the bento layout.

## Challenge Checklist

- Bento grid dashboard with hero, dynamic course cards, and activity chart
- Dark mode-only visual system with subtle gradient mesh and grain
- Responsive desktop, tablet, and mobile navigation
- Semantic layout with `aside`, `nav`, `main`, `section`, and `article`
- Supabase-backed course table schema and seed data
- Server Component data fetching with typed course payloads
- Suspense/loading skeletons and graceful Supabase error handling
- Framer Motion stagger, hover springs, progress animation, and `layoutId` nav highlight
