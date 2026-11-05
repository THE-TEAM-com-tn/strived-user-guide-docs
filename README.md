# Strived User Guide

The user guide of **Strived**, the e-learning platform by THE TEAM, built with
[Mintlify](https://mintlify.com). Step-by-step guides with screenshots of the web app, in English and
French, for each role:

| Role | Folder | Guides |
| :-- | :-- | :-- |
| Student | `student-guide/` | 9 English + 9 French |
| Instructor | `instructor-guide/` | 6 English + 6 French |
| Content manager | `content-manager-guide/` | 5 English + 5 French |
| Admin | `admin-guide/` | 9 English + 9 French |

Screenshots are in `images/<folder>/`, navigation in `docs.json`. Writing and screenshot rules are
in [`CLAUDE.md`](CLAUDE.md).

## Preview

```bash
npm i -g mint
mint dev            # http://localhost:3000
mint broken-links
```

## Publishing

Once the Mintlify GitHub app is connected to this repo
([dashboard](https://dashboard.mintlify.com/settings/organization/github-app)), every push to `main`
is deployed.
