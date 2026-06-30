# Product Specification

## Working name

The repository name is `love-letters`, but the public-facing name can still be finalized.

Current working direction:

- **Bridge of Time**
- **Letters of Love for the Future**
- Latvian possible name: **Vēstules nākotnei**
- Russian possible name: **Письма будущему** / **Фразы о любви для будущих поколений**

The platform should feel like a public cultural initiative, not a commercial postcard shop.

## One-sentence concept

A public archive where people leave short letters and phrases about love for future generations, with selected messages later becoming postcards, a catalogue, an exhibition, or a physical installation.

## Background

The idea comes from the **Mīlestības bāka Jūrmalā** social project. Even if the physical lighthouse was not funded through the city vote, the idea can continue as an online cultural archive and later grow into physical formats.

Important framing:

> The lighthouse project did not end with the voting. It became the beginning of a wider public archive of love, memory and hope.

## Main goals

1. Collect sincere messages about love.
2. Give every message an archive number.
3. Moderate content before publication.
4. Publish approved letters in a beautiful archive.
5. Let visitors open random letters from the central heart visual.
6. Let visitors like and share letters.
7. Create a curated base for future postcards, printed catalogues, exhibitions and physical objects.

## Non-goals for MVP

Do not build these in the first version:

- Etsy integration
- public user accounts
- passwords for visitors
- comments
- complex private dashboards
- direct editing/deleting by authors
- payment/donation flows
- AI-generated postcards
- heavy social network mechanics
- separate public submit page
- separate public page for every short letter

## Target users

### Letter authors

People who want to leave a short emotional message for children, grandchildren, future generations, their city, Latvia, or the world.

They should not need to register.

### Readers

People browsing the archive, opening random letters, liking meaningful messages and sharing them.

### Admins/moderators

Project owner or trusted helpers who review submissions, correct minor spelling issues, approve/reject letters and feature selected messages.

### Future partners

Cultural institutions, schools, libraries, city organizations, sponsors, publishers or exhibition spaces.

## Content type

The platform should collect short letters/messages. The exact max length can be decided later, but MVP should encourage concise text.

Suggested length:

- Minimum: 20 characters
- Maximum: 1,000 characters
- Ideal display: 100-500 characters

## Letter fields

Required before submit:

- Letter text
- Consent checkbox

Optional before submit:

- Author name
- Anonymous publishing option
- City
- Country
- Language

Optional after submit:

- Email address to receive the letter number/link and approval notification

## Email philosophy

Do not ask for email before the user writes the letter. The writing flow should feel emotional and frictionless.

After submission, show the archive number and offer email as a practical follow-up:

> Your letter has been received for moderation. Your letter number is № 000127. If you want to receive the link and find it in the future, leave your email. Email will not be published.

Email is optional. If the author skips it, they are responsible for saving the archive number.

## Archive number

Assign archive number immediately on creation.

Example formats:

```txt
№ 000127
LL-2026-000127
BT-2026-000127
```

Recommendation for MVP: use simple public display `№ 000127` and keep internal IDs separate.

Gaps in public numbering are acceptable if some submissions are rejected or hidden.

## Letter statuses

- `pending` - submitted, waiting for moderation
- `approved` - publicly visible
- `rejected` - not shown publicly
- `hidden` - previously approved but removed from public archive

## Core public features

### Homepage

The homepage should be emotional and simple.

Hero idea:

- centered heart made of letters/envelopes
- main action: **Open random letter**
- secondary action: **View archive**
- sticky bottom-right action: **Write your letter**

Clicking the heart or random button opens a letter modal.

Clicking `Write your letter` opens the submit modal. Do not route the user to a separate submit page for MVP.

### Submit modal

The submit modal is the main writing experience.

Step 1 fields:

- letter text
- author name optional
- anonymous checkbox
- city optional
- country optional
- language optional
- consent checkbox

Step 2 after successful submit:

- show archive number
- optional email field
- `Send link to my email`
- `Skip`

### Letter modal

The modal is the main reading experience.

Contents:

- archive number
- date
- letter text
- author display name or Anonymous
- location if available
- heart/like count
- share action
- random/next action

Example:

```txt
№ 000127
12.07.2026

“Love is the light we leave for those who come after us.”

— Anna, Jūrmala

♥ 248     Share
```

### Likes / hearts

Do not use 1-10 ratings.

Use simple hearts:

- visitor clicks heart
- count increases
- liked letter is considered saved/bookmarked for that visitor
- no separate bookmark feature in MVP

Ranking is based on total hearts.

Preferred labels:

- Most loved
- Most shared
- Featured
- Latest

### Sharing

Each approved letter should be shareable, but MVP should not create a classic standalone page for every short letter.

Use query-parameter deep links that open the selected letter in modal, for example:

```txt
/?letter=000127
/archive?letter=000127
```

Recommended behavior:

- from homepage random modal, share `/?letter=000127`
- from archive modal, share `/archive?letter=000127`
- opening either link loads the normal page and opens the letter modal automatically
- if the letter is missing or not approved, show a safe unavailable state in the modal/page area

Do not implement `/letter/[archiveNumber]` for MVP unless explicitly requested later.

## Archive page

The archive is where browsing/ranking belongs.

Suggested sections/tabs:

- Featured
- Most loved
- Most shared
- Latest
- Search by number

Clicking a card opens the letter modal.

Optional later:

- By language
- By city/country
- From Jūrmala
- From Latvia
- Worldwide

## About page

Move future physical formats here, not on homepage.

About should explain:

- story of Mīlestības bāka
- why the archive exists
- how messages may later become postcards, a catalogue, an exhibition or public installation
- role of POSTOS as organizer/supporter

## Visual style

Desired mood:

- editorial
- warm white / paper / ivory
- black typography
- restrained red heart accent
- elegant serif typography for headings/logo
- minimal interface
- emotional but not childish
- cultural, not e-commerce

Avoid:

- cheap Valentine style
- glossy hearts
- overloaded card grids
- social-network noise
- commercial Etsy-like product language

## Language strategy

Need to decide exact public scope, but MVP should support language as data.

Possible UI languages:

- Latvian
- Russian
- English

Possible letter languages:

- any of the above initially

Important unresolved product question:

If the project is positioned around Jūrmala and the future lighthouse, should letters be only from Jūrmala, from Latvia, or from anyone? Keep data model flexible enough for all three.

## POSTOS role

POSTOS can be visible but secondary.

Suggested footer framing:

```txt
An initiative by POSTOS
```

or

```txt
Created with the support of POSTOS
```

The platform itself should feel like a public initiative rather than just a company page.
