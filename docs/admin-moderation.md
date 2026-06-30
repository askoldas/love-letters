# Admin & Moderation

## Purpose

No letter should appear publicly before human moderation.

The project is emotional and public-facing, so moderation protects:

- tone of the archive
- legal safety
- privacy
- cultural dignity
- future use in print/exhibitions

## Admin access

Use Supabase Auth for admins only.

Roles:

```txt
owner
admin
moderator
```

MVP can start with one admin account.

## Admin dashboard sections

Minimum:

```txt
Pending letters
Approved letters
Rejected letters
Featured letters
Search by archive number
```

Later:

```txt
Export
Collections
Statistics
Email logs
```

## Pending letter review

Admin should see:

```txt
Archive number
Created date
Letter text
Author name
Anonymous setting
City/country
Language
Email exists: yes/no
Status
Admin notes
```

Email address should be visible only to admins who need it. It must never be shown publicly.

## Actions

### Approve

Changes status to `approved` and sets `approved_at`.

If email exists, send publication email.

### Reject

Changes status to `rejected` and sets `rejected_at`.

Optional internal rejection reason.

MVP does not need to send rejection emails unless the owner specifically wants it.

### Hide

For already approved letters that should no longer be public.

Changes status to `hidden` and sets `hidden_at`.

### Edit small typo

Admin may fix minor typos, punctuation or formatting.

Admin should not rewrite the meaning of the letter.

### Feature / unfeature

Marks selected approved letters for the Featured archive section.

## Moderation guidelines

Approve messages that are:

- sincere
- kind
- relevant to love, memory, hope, future generations, family, city or humanity
- suitable for public archive

Reject or hide messages that include:

- hate, threats or humiliation
- political agitation that does not fit the archive tone
- explicit sexual content
- personal attacks
- spam or advertising
- private personal data of third parties
- copyrighted long texts copied from books/songs
- unclear or meaningless text
- trolling

## Editing rules

Allowed minor edits:

- obvious typos
- spacing
- punctuation
- accidental repeated characters
- capitalization

Avoid:

- changing meaning
- improving style too heavily
- turning the author’s voice into something else

If a letter is very strong but needs meaningful editing, contact the author if email is available, or leave it as submitted.

## Anonymity rules

If `is_anonymous = true`, do not show author name publicly even if it was submitted.

Public display:

```txt
— Anonymous
```

Russian:

```txt
— Анонимно
```

Latvian:

```txt
— Anonīmi
```

## Location rules

City/country should be optional.

Before public display, confirm product decision:

- show city/country if user provided it
- or keep it only for internal categorization

For MVP, displaying city/country is acceptable if the form makes it clear that it may be published.

## Email rules

Email is private.

Use email only for:

- confirmation after submission
- publication notification
- find-my-letter results
- admin contact if necessary

Do not use email for marketing unless a separate marketing consent is added.

## Approval email draft

English:

```txt
Subject: Your letter has been added to the archive

Thank you for leaving a message for the future.

Your letter has been approved and published in the archive.

Letter number: № 000127
Open your letter: [link]

With warmth,
Bridge of Time
```

Russian:

```txt
Тема: Ваше письмо добавлено в архив

Спасибо, что оставили послание для будущего.

Ваше письмо прошло модерацию и опубликовано в архиве.

Номер письма: № 000127
Открыть письмо: [ссылка]

С теплом,
Bridge of Time / POSTOS
```

## Submission confirmation email draft

English:

```txt
Subject: Your letter has been received

Thank you for leaving a message for the future.

Your letter has been received and is waiting for moderation.

Letter number: № 000127
Status: waiting for moderation

We will send another message if it is added to the public archive.
```

Russian:

```txt
Тема: Ваше письмо получено

Спасибо, что оставили послание для будущего.

Ваше письмо получено и ожидает модерации.

Номер письма: № 000127
Статус: ожидает модерации

Если письмо будет добавлено в открытый архив, мы пришлём вам ссылку.
```

## Find my letter email draft

Always show the same UI response after requesting lookup:

```txt
If this email is connected with any letters, we will send the information to it.
```

Email content if matches exist:

```txt
We found letters connected with this email:

№ 000127 — published
[Open letter]

№ 000145 — waiting for moderation
```

If no matches exist, either send nothing or send a neutral email. MVP can send nothing.

## Audit trail

For MVP, updated timestamps and admin notes are enough.

Later add `letter_events` for full history:

- submitted
- email added
- approved
- rejected
- hidden
- featured
- unfeatured

## Export needs

Admin should eventually export selected approved letters for:

- printed book
- postcards
- exhibition wall
- lighthouse/installation plaques
- partner presentation

MVP export can be CSV.

Fields to export:

```txt
archive_number
text
author_display
city
country
language
approved_at
hearts_count
shares_count
is_featured
```
