# Architecture

## Recommended stack

```txt
Frontend/app: Next.js
Hosting: Vercel
Database: Supabase Postgres
Admin auth: Supabase Auth
Public user auth: none
Email provider: Resend or similar later
Storage: Supabase Storage later if generated images/PDFs are added
```

## Why Supabase

The project is an archive. It needs relational querying:

- approved letters
- pending letters
- most loved
- most shared
- featured
- latest
- search by archive number
- filter by language/location later
- export selected letters for printed materials

Postgres/Supabase is a better fit than Firestore for this structure.

## App structure recommendation

Possible Next.js App Router structure:

```txt
app/
  layout.tsx
  page.tsx
  archive/
    page.tsx
  submit/
    page.tsx
  about/
    page.tsx
  letter/
    [archiveNumber]/
      page.tsx
  admin/
    layout.tsx
    page.tsx
    letters/
      page.tsx
      [id]/
        page.tsx
  api/
    letters/
      submit/route.ts
      random/route.ts
      like/route.ts
      share/route.ts
      email-link/route.ts
    admin/
      approve/route.ts
      reject/route.ts
      feature/route.ts
```

This is only a suggested structure. Prefer server actions where simpler, but keep validation and abuse protection on the server.

## Public routes

### `/`

Homepage with letter heart and random letter modal.

### `/archive`

Archive browse page with tabs/sections:

- Featured
- Most loved
- Most shared
- Latest

Clicking a card opens a modal.

### `/submit`

Letter composition and post-submit email capture.

### `/about`

Project story and future physical formats.

### `/letter/[archiveNumber]`

Shareable route. It should not feel like a separate article page. It can render the normal site and open the matching letter in a modal.

If the letter is not approved, show a safe fallback:

```txt
This letter is not available in the public archive yet.
```

## Admin routes

Admin area is protected by Supabase Auth and role checks.

Minimum admin features:

- list pending letters
- read full submission
- approve
- reject
- edit small typo/metadata
- mark/unmark featured
- hide approved letter
- export CSV later

## Public users

Public users should not register.

They can:

- read approved letters
- submit a letter
- optionally add email after submission
- like/heart approved letters
- share approved letters
- search by archive number

They cannot:

- edit after submit
- delete directly
- manage privacy directly
- see pending/rejected letters

If they need changes, they contact admin and provide letter number.

## Email logic

Email is optional and requested after successful submission.

Recommended events:

1. Letter submitted: show archive number immediately.
2. User optionally provides email.
3. Send confirmation email with letter number/status.
4. After approval, send published email with public link.
5. `Find my letter` sends letter links to the entered email if matches exist.

No tokens are required for MVP.

## API behavior

### Submit letter

Input:

- text
- author name optional
- anonymous boolean
- city optional
- country optional
- language optional
- consent boolean

Server:

- validate length and consent
- assign `archive_number`
- insert with status `pending`
- return archive number

### Add email after submit

Input:

- archive number or internal letter id returned from submit
- email

Server:

- validate email
- attach email to pending letter if allowed
- send confirmation email

Do not allow arbitrary public update of any letter just by archive number. The immediate post-submit page can hold the internal id in memory/session. For MVP, keep it simple but avoid open update endpoints that can attach emails to someone else's letter.

Safer options:

- after submit, return internal id and one short-lived session value
- or store email in same submit request if user provides it before leaving confirmation screen
- or require email immediately in the same browser session

No long-lived tokens are needed.

### Random letter

Return one approved letter.

Suggested random weighting later:

```txt
70% random approved letters
20% featured letters
10% most loved letters
```

MVP can be plain random from approved letters.

### Like letter

Prevent simple repeated likes.

Options:

- anonymous visitor id in cookie/localStorage
- IP/user-agent coarse rate limit on server
- `letter_likes` table with `visitor_id`

For MVP, local visitor id + server uniqueness is enough.

### Share letter

Track share clicks on server if desired.

Minimum MVP:

- increment shares_count when user clicks share
- use native share/copy link on client

## Data access and security

Use Supabase Row Level Security if reading/writing from client directly. However, for public writes, prefer Next.js server routes/actions because they allow:

- validation
- rate limiting
- spam checks
- email handling
- cleaner secret management

Recommended:

- public reads can use safe Supabase queries for approved letters
- public writes go through server
- admin writes require authenticated admin role

## Environment variables

Expected environment variables later:

```txt
NEXT_PUBLIC_SUPABASE_URL=
NEXT_PUBLIC_SUPABASE_ANON_KEY=
SUPABASE_SERVICE_ROLE_KEY=
EMAIL_PROVIDER_API_KEY=
EMAIL_FROM=
NEXT_PUBLIC_SITE_URL=
```

Never expose `SUPABASE_SERVICE_ROLE_KEY` to the browser.

## Abuse protection

MVP should include at least basic protection:

- server-side length validation
- consent required
- rate limit submissions by IP or visitor id
- rate limit likes/shares
- moderation before publication
- optional simple honeypot field on submit form

Do not publish letters automatically.

## Future storage

Supabase Storage may be used later for:

- generated postcard images
- exported PDFs
- public media
- archive scans

Not needed for first MVP.
