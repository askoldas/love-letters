# AGENTS.md

Instructions for Codex and other AI coding agents working in this repository.

## Project summary

This project is a public cultural archive for short love letters/messages for future generations.

Working public concept:

- **Bridge of Time**
- **Letters of Love for the Future**
- Possible LV: **Vēstules nākotnei**
- Possible RU: **Письма будущему** / **Фразы о любви для будущих поколений**

It originated from the **Mīlestības bāka Jūrmalā** idea. The platform should make that idea broader: first an online archive, later postcards, printed catalogue, exhibition or physical installation.

## Read before coding

Before implementing anything, read:

- `README.md`
- `docs/product-spec.md`
- `docs/ux-flows.md`
- `docs/architecture.md`
- `docs/database-schema.md`
- `docs/admin-moderation.md`
- `docs/roadmap.md`
- `docs/implementation-plan.md`

If any implementation request conflicts with these docs, point it out and propose the smallest coherent adjustment.

## Core product decisions

Keep these decisions unless explicitly changed:

1. Use **Next.js** for frontend/app.
2. Host on **Vercel**.
3. Use **Supabase Postgres** for database.
4. Use **Supabase Auth only for admins**.
5. Public users must **not** be required to register.
6. A letter gets an archive number immediately after submission.
7. Letter publication requires admin moderation.
8. Ask for email only after letter submission, as an optional way to receive the link/find the letter later.
9. No token-based private user dashboard in MVP.
10. No 1-10 rating system.
11. Use hearts/likes. Liked = effectively saved/bookmarked for the visitor.
12. Homepage should be emotional and simple, centered around the heart made of letters.
13. Letter reading should be modal-first.
14. Letter submission should be modal-first.
15. Do **not** create a separate `/submit` public page for MVP.
16. Do **not** create a separate `/letter/[archiveNumber]` public page for MVP.
17. Shareable letter links should use a query parameter, for example `/?letter=000127` or `/archive?letter=000127`, and open the selected letter in a modal.
18. Archive rankings belong on `/archive`, not on the homepage.
19. Future physical formats belong mostly on `/about`.
20. Do not build Etsy-related features in this repository.

## UX requirements

### Homepage

- Include a centered heart visual made from letters/envelopes.
- Main interaction: `Open random letter`.
- Include `View archive`.
- Include sticky bottom-right CTA: `Write your letter`.
- Sticky CTA opens submit modal.
- Do not overload homepage with full archive/ranking sections.

### Submit modal

- The submit flow opens in an overlay modal, not a separate page.
- First ask user to write the letter.
- Do not make email the first step.
- After successful submit, show archive number and optional email field in the same modal flow.
- Make it clear email is not public.

### Letter modal

A letter should open in overlay/modal with:

- archive number
- date
- text
- author display or anonymous
- location if public
- heart count
- share action
- random/next action

### Archive

Archive should include:

- Featured
- Most loved
- Most shared
- Latest
- Search by archive number

Cards should open letters in modal.

### About

About should explain:

- story/background
- Mīlestības bāka connection
- future postcards/catalogue/exhibition/installation
- POSTOS role

## Database rules

Use schema from `docs/database-schema.md` as the starting point.

Important:

- Keep internal UUID separate from public archive number.
- Never expose email publicly.
- Public reads only approved letters.
- Pending/rejected/hidden letters are admin-only.
- Public writes should go through server-side validation.
- Admin writes require authenticated admin role.

## Security and privacy

- Never expose `SUPABASE_SERVICE_ROLE_KEY` to client code.
- Validate all public input server-side.
- Use moderation before publication.
- Add rate limiting/honeypot where practical.
- Do not reveal whether an email exists in the public UI.
- For `Find my letter`, always show a neutral success message and send results by email.
- Do not add public editing/deleting by archive number.

## Styling direction

The visual mood should be:

- warm paper / ivory / editorial
- elegant serif headings
- clean black typography
- restrained red heart accent
- minimal and cultural
- emotional but not childish

Avoid:

- cheap Valentine graphics
- glossy hearts
- e-commerce/product-shop feeling
- overloaded social media UI
- too many buttons/icons

## Implementation style

- Prefer clear, simple, maintainable code.
- Keep MVP scope tight.
- Do not introduce unnecessary libraries.
- Do not create complex abstractions before they are needed.
- Use TypeScript.
- Prefer server-side code for database mutations.
- Keep public components accessible and responsive.
- Keep copy easy to translate later.

## Suggested app structure

This is a suggestion, not a strict requirement:

```txt
app/
  layout.tsx
  page.tsx
  archive/page.tsx
  about/page.tsx
  admin/layout.tsx
  admin/page.tsx
  admin/letters/page.tsx
  api/letters/submit/route.ts
  api/letters/random/route.ts
  api/letters/like/route.ts
  api/letters/share/route.ts
  api/letters/email-link/route.ts
components/
  home/
  archive/
  letters/
    LetterModal.tsx
    LetterCard.tsx
  submit/
    SubmitLetterModal.tsx
  admin/
lib/
  supabase/
  validation/
  email/
  formatters/
```

Do not add `app/submit/page.tsx` or `app/letter/[archiveNumber]/page.tsx` for MVP unless explicitly requested.

## Naming and language

Names are not final. Do not hard-code too many public brand strings in deep components. Centralize public copy as much as practical.

Plan for at least these languages later:

- English
- Russian
- Latvian

MVP can start with one language if requested, but structure should not make localization painful.

## What not to do

Do not implement:

- Firebase
- public auth/accounts
- comments
- 1-10 ratings
- bookmarks separate from hearts
- Etsy/e-commerce features
- direct author edit/delete dashboard
- automatic publication without moderation
- heavy AI content generation
- separate public `/submit` page
- separate public `/letter/[archiveNumber]` page

## When unsure

Prefer the simpler modal-first archive solution.

If a requested feature risks scope creep, explain the tradeoff and suggest MVP-safe implementation.
