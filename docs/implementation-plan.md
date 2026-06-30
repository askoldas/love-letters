# Implementation Plan

This plan is for the first real MVP implementation.

## Stage 1 — Project setup

Create a Next.js app with TypeScript.

Recommended choices:

```txt
Next.js App Router
TypeScript
CSS Modules or plain CSS with design tokens
Supabase JS client
Zod or lightweight validation
```

Do not add a heavy UI kit unless explicitly requested.

## Stage 2 — Environment and Supabase

Add environment variables:

```txt
NEXT_PUBLIC_SUPABASE_URL=
NEXT_PUBLIC_SUPABASE_ANON_KEY=
SUPABASE_SERVICE_ROLE_KEY=
NEXT_PUBLIC_SITE_URL=
EMAIL_PROVIDER_API_KEY=
EMAIL_FROM=
```

Create Supabase helpers:

```txt
lib/supabase/client.ts       public browser/client-safe client
lib/supabase/server.ts       server client
lib/supabase/admin.ts        service-role server-only client
```

Never import service-role client into client components.

## Stage 3 — Database migration

Create SQL migration based on `docs/database-schema.md`.

Minimum tables:

- `letters`
- `letter_likes`
- `letter_shares`
- `admin_profiles`

Minimum indexes:

- status + created_at
- status + hearts_count
- status + shares_count
- featured + status
- email_normalized

## Stage 4 — Public homepage

Build `/`:

- header
- hero heart visual placeholder/component
- `Open random letter` action
- `View archive` link
- sticky `Write your letter` CTA
- letter modal component
- submit letter modal component
- support `?letter=000127` to open a selected approved letter in modal

The heart visual can start as an image asset or placeholder. Keep component structure ready for replacement with final art.

## Stage 5 — Submit modal flow

Letter submission should happen in a global modal, not in a separate public page.

Open the submit modal from:

- sticky CTA
- header action
- letter modal `Write your own letter` action

Step 1:

- letter text
- author name optional
- anonymous checkbox
- city optional
- country optional
- language optional
- consent checkbox

Submit action:

- validates input
- creates letter with `pending` status
- returns archive number

Step 2 confirmation:

- show archive number
- optional email field
- send/save email
- skip button

## Stage 6 — Admin moderation

Build protected `/admin`:

- Supabase Auth login
- list pending letters
- approve/reject/hide
- edit minor metadata/text
- feature/unfeature

MVP can be simple and functional. Visual polish comes later.

## Stage 7 — Archive

Build `/archive`:

Sections or tabs:

- Featured
- Most loved
- Most shared
- Latest

Each card opens the modal.

Add search by archive number.

Support `/archive?letter=000127` to open a selected approved letter in modal.

## Stage 8 — Random letter

Create API/server function:

- fetch random approved letter
- return safe public fields only
- handle empty archive state

## Stage 9 — Likes/hearts

Implement heart action:

- anonymous visitor id stored in cookie/localStorage
- insert into `letter_likes`
- increment `hearts_count` only when new like inserted
- show filled heart locally

No 1-10 ratings.

No separate bookmark feature.

## Stage 10 — Sharing

Implement share action:

- generate link to `/?letter=000127` from homepage context
- generate link to `/archive?letter=000127` from archive context
- use Web Share API if available
- fallback copy to clipboard
- increment `shares_count`

Use query-parameter deep links for MVP.

## Stage 11 — Query-param modal deep links

Implement deep-link behavior for:

```txt
/?letter=000127
/archive?letter=000127
```

Behavior:

- if letter approved: render normal page with modal open
- if not approved/missing: show safe unavailable state

## Stage 12 — Email

Add email provider integration when ready.

Emails:

- confirmation after email entered post-submit
- approval/published notification
- find-my-letter email later

Until provider is connected, log emails in development.

## Stage 13 — About page

Build `/about`:

- project story
- Mīlestības bāka connection
- how the archive may become postcards, printed book, exhibition, installation
- POSTOS role

## Stage 14 — Polish and QA

Check:

- mobile layout
- sticky CTA behavior
- modal accessibility
- server validation
- public cannot see pending letters
- email never appears publicly
- admin-only routes protected
- empty states
- rate limiting/honeypot

## Suggested first Codex task

Start with:

```txt
Create the Next.js project structure, basic public routes, shared layout, design tokens, placeholder heart hero, letter modal, submit-letter modal, archive page shell, about page shell, admin shell, and Supabase helper files. Do not implement database mutations yet. Keep public reading and writing modal-first. Follow README.md, AGENTS.md and docs/*.md.
```

Then implement database and flows in smaller steps.
