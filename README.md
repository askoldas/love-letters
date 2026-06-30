# Love Letters / Bridge of Time

Public cultural platform for collecting, moderating, publishing, liking and sharing short love letters/messages for future generations.

Working public concept:

- **Bridge of Time**
- **Letters of Love for the Future**
- Possible Latvian positioning: **Vēstules nākotnei**
- Possible Russian positioning: **Письма будущему** / **Фразы о любви для будущих поколений**

The project started from the **Mīlestības bāka Jūrmalā** idea, but should be shaped as a broader public archive that can later become postcards, a printed catalogue, an exhibition, a physical installation, or a renewed lighthouse-style object.

## Product direction

This is not an Etsy shop and not an e-commerce-first project. The first version should focus on a clean cultural archive:

1. People write short messages about love for children, grandchildren, future generations, Jūrmala, Latvia, or the world.
2. A letter receives an archive number immediately after submission.
3. Admin reviews and approves/rejects it.
4. Approved letters appear in the public archive.
5. Visitors can open a random letter, like it with a heart, and share it.
6. The strongest letters can later be selected for printed or physical formats.

## Core MVP pages

The MVP should stay modal-first. Do not create separate public pages for composing or reading individual letters unless this is explicitly changed later.

```txt
/
  Homepage with centered heart made of letters, random-letter interaction, letter modal and submit-letter modal

/archive
  Public archive with Featured, Most loved, Most shared and Latest sections/tabs; cards open letters in modal

/about
  Story of the project, Mīlestības bāka background and future physical formats

/admin
  Protected moderation area
```

## Modal-first behavior

- Reading a letter happens in an overlay modal on the homepage or archive.
- Writing a letter happens in a submit modal opened from the sticky CTA or header action.
- Sharing should use a URL parameter such as `/?letter=000127` or `/archive?letter=000127`, which opens the selected letter in a modal.
- There is no classic `/letter/[archiveNumber]` public page in the MVP.
- There is no separate `/submit` page in the MVP.

## Preferred tech stack

- **Frontend:** Next.js
- **Hosting:** Vercel
- **Database:** Supabase Postgres
- **Auth:** Supabase Auth for admins only
- **Public users:** no registration
- **Email:** optional after submission, used only to send the letter number/link and approval notification

## Documentation

Read these files before implementation:

- [`docs/product-spec.md`](docs/product-spec.md)
- [`docs/ux-flows.md`](docs/ux-flows.md)
- [`docs/architecture.md`](docs/architecture.md)
- [`docs/database-schema.md`](docs/database-schema.md)
- [`docs/admin-moderation.md`](docs/admin-moderation.md)
- [`docs/roadmap.md`](docs/roadmap.md)
- [`docs/implementation-plan.md`](docs/implementation-plan.md)
- [`AGENTS.md`](AGENTS.md)
