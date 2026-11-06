# Strived User Guide

The user guide of **Strived**, the e-learning platform by THE TEAM, built with
[Mintlify](https://mintlify.com). Step-by-step guides with screenshots of the web app and the phone
app, in English and French, for each role:

English pages live at the root, French pages in `fr/` with the same file names, so the
**English / Français** menu in the header opens the same page in the other language.

| Role | English | French |
| :-- | :-- | :-- |
| Student | `student-guide/` (10 guides) | `fr/student-guide/` |
| Instructor | `instructor-guide/` (7 guides) | `fr/instructor-guide/` |
| Content manager | `content-manager-guide/` (6 guides) | `fr/content-manager-guide/` |
| Admin | `admin-guide/` (10 guides) | `fr/admin-guide/` |

The home page (`index.mdx` "Presentation", French `fr/index.mdx` "Présentation") presents the
platform and what each role does, with a diagram, screenshots of the iPhone app and the App Store
and Google Play badges (`images/presentation/`; their links are still `#`, see `CLAUDE.md` §4) and a
"coming soon" video of the AI assistant. Guide screenshots are in
`images/<folder>/`;
navigation, header, footer and language menu in `docs.json`; a little custom CSS in `style.css`.
Writing and screenshot rules are in [`CLAUDE.md`](CLAUDE.md).

## Preview

```bash
npm i -g mint@latest
mint dev            # http://localhost:3000
mint broken-links
```

## Publishing

Once the Mintlify GitHub app is connected to this repo
([dashboard](https://dashboard.mintlify.com/settings/organization/github-app)), every push to `main`
is deployed.
