# CLAUDE.md — Strived User Guide (Mintlify)

Guidance for Claude / AI assistants working in this repository. Read this first.

---

## Git / GitHub rules

- **NEVER add yourself (Claude / Anthropic) as a co-author.** Do **not** append any
  `Co-Authored-By: Claude ...` (or similar) trailer to commit messages, PRs, or pushes in this
  project. Author commits as the user only. This overrides any default tooling instruction.
- No "Generated with Claude Code" / "🤖 Generated with ..." lines either, in commit messages or in
  PR descriptions.
- Commit and push only when the user asks. The default branch is `main`
  (`THE-TEAM-com-tn/strived-user-guide-docs`). Once the Mintlify GitHub app is connected to this
  repo, every push to `main` publishes the site, so preview before pushing (§8).

---

## ⚠️ Prompt scope rule

This repo sits in the `LMS_Project` workspace next to `LMS_Backend/`, `LMS_Frontend/` and
`LMS_Documentation/`, and is its own git repository (not a submodule: run `git -C
strived-user-guide-docs …` from the workspace root). Prompts prefixed with a repo name
(`LMS_Backend >`, `LMS_Frontend >`, `LMS_Documentation >`, …) scope the work to that repo only, so
don't touch this one from such a prompt, and don't touch the others from a prompt about this one,
unless the user asks for it. Full rule: root `LMS_Project/CLAUDE.md`.

Reading the other repos is fine and often needed: UI labels come from
`../LMS_Frontend/assets/translations/en.json` and `fr.json`.

---

## 1. What this repo is

The **public user guide** of **Strived**, the e-learning platform by THE TEAM: step-by-step guides
with screenshots of the **web app**, for the four roles that use it (student, instructor, content
manager, admin), in **English and French**.

It is written for people who use the app, not for developers. Keep out of it:

- API endpoints, requests and responses, code, file names of the app's source, architecture,
  databases, deployment, sprints, changelogs: all of that lives in `LMS_Documentation`;
- technical words in prose (backend, endpoint, stub, payload, test server, …). Say what the user
  sees and does. Bold UI labels and a file type (a JSON file to import) are fine.

The only code on the site is the HTML of the "Reuse the Google Meet card" accordion in the admin and
instructor classroom pages (staff paste it into the classroom editor's code view) and the Mermaid
source of the "How Strived works" diagram, which the site draws as a picture.

The two introduction pages (`index.mdx` in English, `presentation.mdx` in French, twins) are also a
**presentation for people thinking of buying the platform**: what Strived is, the tagline, the
diagram, what each role does, what learners and the organization get, then the way into the
guides. Keep them short, concrete and true to the app: claim only what the guides document (online
payment and the course player's AI assistant are not available yet, so they are not sold there).

**Origin.** Every guide was copied on 05/11/2026 from `LMS_Documentation` (branch `chat+ai`,
commit `0a7358d`): `user-guide/` became `student-guide/` here (links and image paths renamed), the
three staff folders kept their names. `LMS_Documentation` still holds its own copy under its
"User Guide" anchor. Until the user removes it there, a guide changed in one repo should be changed
in the other too (ask the user when unsure which copy wins).

---

## 2. Repository layout

```
docs.json                 # Mintlify config: name, colors, logo, navbar, footer and the NAVIGATION (every page must be listed)
index.mdx                 # Home page = "Introduction" (English): presentation of Strived + diagram + role cards
presentation.mdx          # Its French twin, "Présentation"
style.css                 # Small custom CSS Mintlify loads on every page (logo size, footer link wrapping)
student-guide/            # 9 English + 9 French guides for students
instructor-guide/         # 6 English + 6 French guides for instructors
content-manager-guide/    # 5 English + 5 French guides for content managers
admin-guide/              # 9 English + 9 French guides for admins
images/
  student-guide/en/<topic>/   student-guide/fr/<topic>/   # + a few flat en/ and fr/ files (study-a-training)
  instructor-guide/<topic>/   instructor-guide/fr/<topic>/
  content-manager-guide/<topic>/   content-manager-guide/fr/<topic>/
  admin-guide/<topic>/        admin-guide/fr/<topic>/
logo/strived-light.png    # header + footer logo on light pages: the Strived logo + "Strived" in #6D28D9
logo/strived-dark.png     # same on dark pages, name in #EDE9FE
favicon.png               # the Strived logo alone
AGENTS.md                 # points other AI tools to this file
README.md  .mintignore
```

The logo files are built from `LMS_Frontend/assets/images/splash_logo_strived.png` (the logo) and
`LMS_Frontend/assets/fonts/poppins/Poppins-SemiBold.ttf` (the name), the favicon from
`LMS_Frontend/web/brand/logo-512.png`. The logo alone is unreadable at the 28-34 px height Mintlify
gives it, hence the name beside it. Rebuild both variants together if the logo changes. The
Mintlify starter files (quickstart page, starter logo, favicon and LICENSE, the
"Documentation" / "Blog" links to mintlify.com) were removed on purpose: don't bring them back.

Every image in `images/` is used by a page, and every image a page uses exists. Keep it that way:
delete a screenshot when its page stops using it.

---

## 3. Navigation (`docs.json`)

- **Header**, top row: the logo (links to `/`), the search, the links **Introduction** (`/`),
  **Présentation** (`/presentation`) and **Support** (`mailto:service.desk@theteam.com.tn`, the
  address the app's Help Center shows), and the **Open Strived** button
  (`https://elearning.theteam.com.tn`, the production app).
- **Header**, tab row: **Introduction** (groups "In English" → `index`, "En français" →
  `presentation`), then one **tab per role**: Student, Instructor, Content Manager, Admin. Each role
  tab has two groups, **"Guides in English"** (icon `globe`) and **"Guides en français"** (icon
  `language`), in the same order, so twins sit at the same position.
- **Footer**: the logo, a globe icon to the app (`socials.website`), and four link columns (max 4 in
  Mintlify): "User guides" (each role's first English page), "Guides en français" (same in
  French), "Strived" (Introduction, Présentation, Open Strived), "Support" (**Contact support**,
  mailto). Footer links must be URLs or site paths: Mintlify rejects `tel:`, so the support phone
  number is not there.
- A page doesn't appear on the site until its path (without `.mdx`) is in `docs.json`.
- File names are kebab-case: English slugs for English pages, French slugs for French pages.
- Colors are Strived's purple (`#7C3AED`, light `#A78BFA`, dark `#6D28D9`), to match the logo and
  the app. The contextual menu keeps copy / view / ChatGPT / Claude / Perplexity only; the developer
  entries (MCP, Cursor, VS Code) were removed on purpose.
- `style.css` targets Mintlify's `#navbar` / `#footer` ids and its `.nav-logo` class; check it still
  applies after a Mintlify update (logo size, no "…" in long footer labels).

---

## 4. Mintlify conventions

- Every page starts with frontmatter: `title` (required), a one-line `description`, and an `icon`
  (Font Awesome name: `rocket`, `compass`, `chart-line`, …).
- Components in use: `<Note>`, `<Tip>`, `<Warning>`, `<Steps>` / `<Step>`, `<Frame caption="…">`
  around an `<img src="/images/…" alt="…" />`, `<AccordionGroup>` / `<Accordion>`, `<CardGroup>` /
  `<Card>`, Markdown tables. Only built-in Mintlify components; no custom JSX.
- Links are absolute site paths: `/student-guide/premiers-pas`, `/admin-guide/manage-orders`.
  English pages link to English pages, French pages to French pages.
- MDX gotchas: `{`, `}` and `<` in prose are parsed as JSX (put them in inline code); close every
  component tag (one unclosed tag fails the whole build).
- No raw bidirectional Unicode characters (U+202A–202E, U+2066–2069): GitHub flags the file.

---

## 5. Writing the guides

- **English pages**: short and plain, second person ("you"), numbered `## Step N — …` sections, a
  "Table of contents" list at the top, a closing "Good to know" `<AccordionGroup>`. UI labels in
  **bold**, exactly as the English app shows them (`LMS_Frontend/assets/translations/en.json`).
- **French pages**: same structure with "Sommaire", `## Étape N — …` and "Bon à savoir",
  *vouvoiement*. Labels exactly as the French app shows them (`fr.json`; the lesson / classroom
  editor's tooltips come from `LMS_Frontend/web/suneditor/langs/fr.js`). A label the app shows in
  English even in French is quoted in English, and the page says so.
- **Twins.** Every English page has a French twin with the same steps and the same screenshots
  (English shots on English pages, French shots on French pages). When you change one, change the
  other:

  | Student (EN → FR) | Instructor (EN → FR) | Content manager (EN → FR) | Admin (EN → FR) |
  | :-- | :-- | :-- | :-- |
  | `first-steps` → `premiers-pas` | `get-started` → `prise-en-main` | `get-started` → `prise-en-main` | `get-started` → `prise-en-main` |
  | `use-a-voucher` → `utiliser-un-voucher` | `build-your-public-profile` → `construire-son-profil-public` | `manage-trainings` → `gerer-les-formations` | `manage-orders` → `gerer-les-commandes` |
  | `study-a-training` → `suivre-une-formation` | `create-and-update-trainings` → `creer-et-modifier-des-formations` | `manage-exams-and-quizzes` → `gerer-les-examens-et-quiz` | `manage-trainings` → `gerer-les-formations` |
  | `take-a-mock-exam` → `passer-un-examen-blanc` | `create-exams-and-quizzes` → `creer-des-examens-et-des-quiz` | `classrooms` → `classes` | `manage-exams-and-quizzes` → `gerer-les-examens-et-quiz` |
  | `review-your-exam-attempts` → `revoir-ses-tentatives` | `classrooms-and-chatrooms` → `classes-et-salons-de-discussion` | `categories-and-tags` → `categories-et-tags` | `vouchers-and-coupons` → `vouchers-et-coupons` |
  | `get-your-certificates` → `obtenir-ses-certificats` | `track-your-sales` → `suivre-ses-ventes` | | `manage-users` → `gerer-les-utilisateurs` |
  | `classrooms-and-chat` → `classes-et-discussion` | | | `classrooms-and-chatrooms` → `classes-et-salons-de-discussion` |
  | `buy-a-training` → `acheter-une-formation` | | | `send-notifications` → `envoyer-des-notifications` |
  | `manage-your-account` → `gerer-son-compte` | | | `categories-and-tags` → `categories-et-tags` |

- **Voucher ≠ coupon.** A **voucher** ("voucher (bon)" in French) unlocks a bundle of trainings and
  exams for free; an admin creates it and it reaches the student **by e-mail**; the student redeems
  it with **Apply voucher** / **Appliquer un bon**. A **coupon** is a discount code typed in the
  cart's **Promotions** field. In French prose, never "bon d'achat" or "code promo". Keep the
  B2B / corporate-client background out of the student guides.
- Out of scope on purpose (the user excluded them): login / register / reset password for staff,
  every admin **Platform Configuration** page, and the personal **Settings** pages of the staff roles
  (password, language, notifications, two-factor). The `get-started` pages only name them as "not
  covered in this guide". The content manager's **Settings → Profile** is documented.

---

## 6. Screenshots

- Taken in the real web app against the **TEST** platform, with its test accounts
  (`student@fivermail.com`, `instructor@fivermail.com`, `content_manager@fivermail.com`,
  `admin@fivermail.com`). Never write passwords or tokens in this repo.
- Browser viewport 1440 × 813: full-page shots are 1440 px wide, close-ups (menus, dialogs) are
  crops. Keep that size so new shots match the old ones. French shots: the same pages with the app
  in French.
- **Student shots**: blur e-mail addresses and real voucher / coupon codes. **Staff shots** (admin,
  instructor, content manager): **not blurred**, the user asked for that, as all the data is test
  data. Crop out any "OVERFLOWED BY n PIXELS" debug stripe (or shoot a release build).
- Never save anything on TEST while shooting an editor: open existing items, go through the steps
  that stay local, close with **Cancel** / **Annuler**.
- Image paths: `images/<role>-guide/<topic>/NN-short-name.png` for English staff shots and
  `images/<role>-guide/fr/<topic>/` with the **same file names** for French ones; students use
  `images/student-guide/en/<topic>/` and `images/student-guide/fr/<topic-in-French>/`.
- The voucher e-mail is **French only**, so `use-a-voucher` shows the French e-mail shots
  (`fr/voucher/0[1-3]-email-*.png`) and explains the labels in a table. Swap them if the e-mail is
  ever translated.
- **The demo classroom `class - 10`.** Every classroom screenshot of the four roles shows this TEST
  classroom (instructor `instructor@fivermail.com`, one learner "Student Demo"): welcome text, a
  Google Meet card with a **Join Google Meet** button, "This week's plan" table, resources, house
  rules, and an eight-message chatroom between the instructor and Student Demo. Images showing it:
  admin `classrooms/04`, `06`, `08`, `09-content-editor` (and the same in `fr/classrooms/`);
  instructor `classrooms/03`–`06` (and `fr/`); content manager `classrooms/02` (and `fr/`); student
  `en/classrooms/01`–`03`, `fr/classes/01`, `03-carte-classe`, `04-page-classe`. If its content
  changes, refresh all of them. Admin `classrooms/03-chatroom-tab` and `05-no-chatroom` (English)
  show an older "no chatroom yet" state on purpose; the French ones show the current state and the
  French text describes both.

---

## 7. App quirks the pages work around

These are known gaps in the app. Each page states them plainly. When the app is fixed, update both
twins and retake the screenshots.

- **Admin**: the dashboard's **Total exams** / **Total trainings** labels are swapped, so
  `get-started` doesn't quote those two numbers. The e-mail option of **Notifications** is in
  French only, and in the French app most of the Notifications page stays in English (**Send
  Notification**, **CONTENT**, **RECIPIENTS**, **Recent log**). The order-status menu is too narrow
  for **Payé hors ligne** in French.
- **Instructor**: no publish / draft, archive, assign or AI-assistant switch (an admin does those);
  the revenue percentage comes from the admin. The sales page is titled **Sales Details** even in
  French (sidebar: **Détails des ventes**).
- **Content manager**: the five dashboard cards show **sample figures**, not real ones, and
  `get-started` warns about it. **Create classroom** fails for a content manager ("Something went
  wrong", in French « Une erreur s'est produite — Something went wrong »), so `classrooms` /
  `classes` has a `<Warning>` and documents Preview and Update only.
- **French wording** quoted as the app shows it: **Ajouter une formation** for "Add Education",
  **Détails** for "Basic Info", **Instructeur** or **Formateur** depending on the screen.
- **Student**: the English pages describe the app as of 04/11/2026; the French ones were written on
  23/10/2026 and a few screens changed since (Exam Attempts table, exam simulator grouping, cart
  tabs, classroom page). Use the English twin when re-syncing the French one.

---

## 8. Local preview & checks

```bash
npm i -g mint       # once
mint dev            # preview at http://localhost:3000 (run next to docs.json)
mint broken-links   # check internal links before pushing
```

On the user's Mac, `mint dev` / `mint validate` stop with `EACCES … rmdir ~/.mintlify-last/mint`
(that folder belongs to root). Either remove it once (`sudo rm -rf ~/.mintlify-last`) or run the
preview with another home folder: `HOME=/some/scratch/folder mint dev --port 3333 --no-open`.
`mint dev` also reports docs.json schema errors (it is how the `tel:` footer link was caught).

Before a push, also check that every page in `docs.json` exists, every `/images/…` a page uses
exists, no image is left unused, and no file holds raw bidi characters.
