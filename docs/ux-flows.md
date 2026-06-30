# UX Flows

## UX principle

The platform should feel like opening and leaving real letters, not like filling a bureaucratic form.

Keep the emotional action first. Ask for practical data only when needed.

MVP is modal-first:

- reading happens in a letter modal
- writing happens in a submit modal
- sharing opens the normal homepage/archive with the selected letter in a modal

## Main public navigation

Suggested header:

```txt
Logo
Archive
Write your letter
About
Language switch
```

Suggested sticky CTA:

```txt
Write your letter
```

On desktop: bottom-right floating pill/button.

On mobile: bottom sticky pill/button, easy to tap.

Hide sticky CTA when the submit modal is already open.

## Homepage flow

### Goal

Make visitors curious, let them read a random message, then invite them to contribute.

### Layout

1. Header
2. Hero with centered heart made of letters/envelopes
3. Primary action on/near heart: `Open random letter`
4. Secondary action: `View archive`
5. Sticky bottom-right CTA: `Write your letter`

Avoid placing heavy archive rankings on homepage. Keep homepage emotional and focused.

### Interaction

Clicking the heart or `Open random letter`:

1. Fetch random approved letter.
2. Open letter in modal overlay.
3. Show archive number, date, text, author/location if available, heart count, share action.
4. Provide `Another random letter` action.
5. Provide subtle `Write your own letter` action inside modal.

Clicking `Write your letter` opens the submit modal, not a separate page.

## Letter modal flow

### Modal content

```txt
№ 000127
12.07.2026

“Letter text..."

— Anna, Jūrmala

♥ 248     Share

[Another random letter]
[Write your own letter]
```

### Modal actions

- Heart/like
- Share
- Open another random letter
- Open submit modal
- Close

### Share behavior

Share should copy/share a link that opens the same letter in modal.

Use query-parameter deep links:

```txt
/?letter=000127
/archive?letter=000127
```

Behavior:

- `/?letter=000127` opens homepage and then opens the selected letter modal
- `/archive?letter=000127` opens archive and then opens the selected letter modal
- if the letter is missing or not approved, show a safe unavailable state

Do not implement a separate `/letter/[archiveNumber]` page for MVP.

## Submit letter modal flow

### Step 1: Write letter

Keep the form minimal.

Fields:

```txt
Your letter *
Author name
Publish anonymously checkbox
City
Country
Language
Consent checkbox *
Submit
```

Email is not requested at this stage by default.

### Consent copy

Draft:

```txt
I confirm that this is my own message and allow the project to publish it in the public archive after moderation.
```

Russian draft:

```txt
Я подтверждаю, что это моё собственное послание, и разрешаю опубликовать его в открытом архиве проекта после модерации.
```

### Step 2: Confirmation after submit

Immediately after submission, keep the user in the same modal and show:

```txt
Your letter has been received for moderation.

Your letter number is № 000127.

If you want to receive the link and find your letter in the future, leave your email. Email will not be published.
```

Actions:

```txt
Email input
Send link to my email
Skip
```

If email is skipped:

```txt
Please save your letter number if you want to find it later: № 000127.
```

### Step 3: Email added after submit

If user provides email:

- save email on letter record
- send confirmation email with archive number and current status
- after approval, send publication email

No visitor account is created.

## Archive flow

Archive page should contain the browse/ranking experience.

Recommended heading:

```txt
Archive of Letters
```

Tabs/sections:

```txt
Featured
Most loved
Most shared
Latest
```

Search:

```txt
Search by letter number
```

Optional later filters:

```txt
Language
City
Country
Jūrmala / Latvia / Worldwide
```

Clicking any archive card opens the letter modal.

Opening `/archive?letter=000127` should load the archive and open that letter modal if the letter is approved.

## Like flow

Visitor clicks heart:

1. If not liked before, create like record or register visitor like.
2. Increment `hearts_count`.
3. Show filled heart.
4. Treat this as saved/bookmarked for the current visitor.

No separate bookmark button in MVP.

Avoid 1-10 ratings.

## Share flow

When visitor clicks share:

1. Increment/share-track according to selected behavior.
2. Use native Web Share API where available.
3. Fallback to copy link.
4. Link should open the exact letter in modal using query param.

Do not make sharing dependent on login.

## Find my letter flow

Optional but recommended.

Footer/archive link:

```txt
Find my letter
```

Flow:

1. User enters email.
2. System does not reveal matches directly on screen.
3. System sends email with letters associated with that email.
4. Email contains archive numbers and links/statuses.

This avoids exposing whether a given email exists in the database.

## Admin moderation flow

1. Admin logs in.
2. Opens pending submissions.
3. Reviews letter text and metadata.
4. Optionally fixes small typos.
5. Approves, rejects or hides.
6. If approving and email exists, send approval email.
7. Approved letter becomes visible in archive.

## Error and empty states

### No approved letters yet

```txt
The archive is just beginning. Be the first to leave a letter for the future.
```

### Random letter unavailable

```txt
No published letters are available yet. You can write the first one.
```

### Deep-linked letter unavailable

```txt
This letter is not available in the public archive yet.
```

### Submission successful but email failed

```txt
Your letter was received, but we could not send the email right now. Please save your letter number: № 000127.
```

## Mobile UX notes

- Heart visual should remain central but not too tall.
- Sticky `Write your letter` button should not cover archive cards or form controls.
- Letter modal should be full-screen or near full-screen on mobile.
- Submit modal should also be full-screen or near full-screen on mobile.
- Use large tap targets for heart/share/random/submit.
