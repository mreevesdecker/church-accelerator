# Church Accelerator Framework

Landing page and application page for the Church Accelerator Framework, a
System & Soul engagement delivered by Dr. Gavin Adams. Built to live at
`systemandsoul.com/church-accelerator-framework`.

## What's in here

| File | What it is |
|------|------------|
| `index.html` | Church Accelerator Framework landing page |
| `apply.html` | Application page for the 12-month engagement, with a Mailchimp-ready form |
| `training.html` | Executive Pastor Training event page (Sept 23–24, Woodstock City Church), with a Mailchimp-ready registration form |
| `assets/system-and-soul-gavin-adams-lockup.png` | Co-brand logo, for uploading to Webflow |

### Still to fill in on `training.html`

Search for these tokens and replace every instance:

- `[[TRAINING_PRICE]]` — e.g. `$1,495 per leader`
- `[[SEATS]]` — e.g. `24`

Dates and venue are already filled in (September 23 & 24, 2026 at Woodstock City
Church, Woodstock, GA). The training page also needs one extra Mailchimp merge
field beyond the list below: a `TRAINING` **dropdown** whose option value matches
the training date string exactly, plus a `TENSION` text field.

Both pages are fully self-contained. All CSS is inline, the logo is embedded
directly in the HTML, and the only external dependency is Poppins from Google
Fonts. Open either file in a browser and it just works.

## Publishing a preview on GitHub Pages

1. Create a new repository on GitHub.
2. Upload every file in this folder, keeping `assets/` as a folder.
3. Go to **Settings → Pages**.
4. Under **Source**, choose **Deploy from a branch**, pick `main` and `/ (root)`.
5. Wait about a minute. Your pages will be live at:
   - `https://YOURNAME.github.io/YOUR-REPO/` (landing)
   - `https://YOURNAME.github.io/YOUR-REPO/apply.html` (application)

The Apply buttons link to `apply.html` relatively, so they work on GitHub Pages
and will keep working wherever else you host these.

## Before this goes live: hook up Mailchimp

The form in `apply.html` is wired to Mailchimp's embedded-form format but still
has placeholder IDs. It will not capture submissions until you replace them.

**Step 1 — Get your IDs.** In Mailchimp, go to *Audience → Signup forms →
Embedded form*. Copy the form action URL. It looks like:

```
https://us21.list-manage.com/subscribe/post?u=abc123def456&id=7890xyz
```

**Step 2 — Paste them into `apply.html`.** Search for `YOURDC`, `USER_ID`, and
`LIST_ID` and replace them in two places: the `<form action="...">` tag, and the
hidden honeypot input named `b_USER_ID_LIST_ID`.

**Step 3 — Create the audience fields.** In *Audience → Settings → Audience
fields and \*|MERGE|\* tags*, add these so the form's field names line up:

| Tag | Type | Label |
|-----|------|-------|
| `EMAIL` | Email | Email *(built in)* |
| `FNAME` | Text | First Name *(built in)* |
| `LNAME` | Text | Last Name *(built in)* |
| `PHONE` | Phone | Phone |
| `CHURCH` | Text | Church Name |
| `ADDRESS` | Address | Church Address |
| `ROLE` | Dropdown | Your Role |
| `ATTEND` | Dropdown | Average Weekend Attendance |
| `CHALLENGE` | Text | Biggest Challenge |
| `OUTCOME` | Text | Successful 12-Month Outcome |

For the two dropdowns, the option values must match the form exactly. `ROLE`:
Senior / Lead Pastor, Executive Pastor, Campus Pastor, Staff Pastor, Ministry /
Department Director, Other Church Leader. `ATTEND`: < 100, 100 - 199, 200 - 499,
500 - 999, 1,000 - 2,500, > 2,500.

**A limitation worth knowing.** Mailchimp text merge fields cap at 255
characters. The two open-ended questions (`CHALLENGE` and `OUTCOME`) are capped
at 255 with a live character counter, so nothing gets silently truncated. If you
want genuinely long answers, point the form at a handler that supports them
(Webflow Forms, Basin, Formspark) and pass only the contact fields to Mailchimp.

## Moving this into Webflow

1. Upload `assets/system-and-soul-gavin-adams-lockup.png` to your Webflow assets.
2. In both pages, find `<img class="cobrand"` and replace the long
   `src="data:image/png;base64,..."` with your Webflow asset URL. This drops the
   page size from ~107KB to ~38KB.
3. Rehost Gavin's headshot. In `index.html` it currently hotlinks his WordPress
   CDN; there's a `TODO` comment marking the spot.
4. The pages have no header, nav, or footer by design, so the System & Soul
   site's global navigation wraps them cleanly.

## Brand notes

Built to the System & Soul brand guidelines (June 2024).

- **Fonts:** Poppins throughout. `StreetWalks` is set up as an `.accent-word`
  class for emphasis words but is not loaded, since it isn't on Google Fonts.
  Upload the licensed font in Webflow and it will pick up automatically.
- **Primary colors (90% of usage):** Blue `#4D80F3`, Navy `#3C4258`,
  Pink `#EB078B`.
- **Accent colors (10%, "Shifts" only):** defined as CSS variables but
  deliberately unused.
- Headlines are navy, never black. White text on all colorful backgrounds. The
  hero navy is sampled to match the logo's own background exactly.
