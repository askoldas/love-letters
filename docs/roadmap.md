# Roadmap

## Guiding idea

Build the archive first. Physical and commercial formats should grow from the archive, not distract from it.

Do not start with Etsy.

## Phase 0 — Project foundation

Goal: agree on structure before design/development goes too far.

Decisions needed:

- final public name/domain
- main UI languages
- whether the initiative is Jūrmala-only, Latvia-wide or open worldwide
- whether city/country are public or internal
- exact letter length limit
- whether the public archive shows all approved letters or curated letters only

Deliverables:

- product specification
- UX flow
- database schema
- visual direction

## Phase 1 — MVP archive

Goal: launch a usable public initiative.

Features:

- homepage with heart visual
- random letter modal
- sticky `Write your letter` CTA
- submit form
- archive number assigned immediately
- optional email after submission
- admin moderation
- public archive
- heart/like count
- share action
- most loved / most shared / latest / featured
- about page

Technical:

- Next.js
- Vercel
- Supabase Postgres
- Supabase Auth for admin
- basic email provider integration

## Phase 2 — Public polish

Goal: make the archive feel alive and shareable.

Features:

- better random letter algorithm
- shareable modal links
- native Web Share API
- beautiful letter card design
- language filters
- search by archive number
- `Find my letter` by email
- improved admin dashboard
- simple analytics

## Phase 3 — Curation layer

Goal: prepare the archive for cultural use.

Features:

- admin collections
- editor’s selection
- export selected letters
- tags/categories
- Jūrmala / Latvia / worldwide grouping
- printable CSV/PDF export
- partner presentation page

Possible collections:

```txt
For children
For future generations
From Jūrmala
From Latvia
Most loved
Editor’s selection
```

## Phase 4 — Visual/postcard layer

Goal: turn letters into beautiful digital/printable objects.

Features:

- generated postcard view for each approved letter
- downloadable image/PDF
- social sharing image
- print-ready export
- optional Milda / Jurmala / paper motif templates

This phase can support future printed postcards, but it is not Etsy yet.

## Phase 5 — Printed catalogue / exhibition

Goal: create real cultural output from selected letters.

Deliverables:

- curated printed book/catalogue
- exhibition wall layout
- QR codes linking to archive letters
- printed postcards
- sponsor/partner materials

## Phase 6 — Physical installation / lighthouse revival

Goal: bring the archive into public space.

Possible forms:

- physical letter holders
- public stand
- sculpture object
- lighthouse-style installation
- rotating exhibition
- plaques with selected letters
- QR-based outdoor archive

The original **Mīlestības bāka** idea can be revived with proof that a real archive and community already exist.

## Later commercial ideas

These should wait until the archive has traction.

Possible:

- printed gift book
- postcard sets
- sponsor-supported editions
- cultural grants
- municipal partnerships
- school/library collaborations
- Etsy shop only if there is already a strong visual product line

## Avoid for now

- building Etsy store before the archive
- too many product branches at once
- complex user accounts
- comments/social network behavior
- paid features
- AI-generated content replacing real messages
- heavy branding that makes it feel like advertising

## MVP success criteria

The first version is successful if:

- people can submit letters without confusion
- admin can moderate safely
- approved letters look beautiful in archive/modal
- random letter interaction feels emotional
- hearts and sharing work
- emails help authors find letters later
- the project can be presented to partners as a serious public initiative
