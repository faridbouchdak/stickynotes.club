# StickyNotes.club

This repository contains the public website pages, Help Center documentation and product design documents for [StickyNotes.club](https://stickynotes.club).

StickyNotes.club is a place where ideas can grow together.

People can share thoughts on the worldwide wall or use private boards to collect, organise and develop ideas with others.

## Documentation website

The Help Center is published at:

**[docs.stickynotes.club](https://docs.stickynotes.club)**

It is built with [Jekyll](https://jekyllrb.com/) and the [Just the Docs](https://just-the-docs.github.io/just-the-docs/) theme, and is published through GitHub Pages.

## Repository structure

The repository contains three types of documents.

### Help Center pages

These pages explain StickyNotes.club from the user's perspective:

- `index.md` — Help Center homepage
- `getting-started.md` — account setup and first steps
- `sticky-notes.md` — public sticky notes and the worldwide wall
- `private-boards.md` — creating and managing private boards
- `collaboration.md` — working together on boards
- `organize-your-work.md` — tags, due dates and board organisation
- `manage-your-profile.md` — profile and account settings
- `plans-and-subscriptions.md` — plans, payments and cancellation
- `privacy-and-safety.md` — privacy controls and account safety
- `community-guidelines.md` — expected community behaviour
- `faq.md` — frequently asked questions
- `troubleshooting.md` — common problems and solutions
- `contact-and-support.md` — support and feedback

### Public information and policies

- `about.md` — the purpose and story of StickyNotes.club
- `privacy.md` — Privacy Policy
- `tos.md` — Terms of Service

### Product and documentation design

These documents record the principles and decisions behind the product:

- `00_Product_Constitution.md` — enduring product principles
- `01_Product_Model.md` — product promise, boundaries and lifecycles
- `02_Product_Playbook.md` — practical product and writing rules
- `03_Product_Design_Notes.md` — discoveries, open questions and future ideas
- `04_Help_Center_Architecture.md` — documentation structure and page template

## Product principles

The core purpose of StickyNotes.club is:

> **Help ideas grow.**

The main principles are:

1. Keep It Super Simple.
2. Users think in goals, not features.
3. Public inspires. Private builds.
4. Trust users by default.
5. Calm software beats noisy software.
6. Documentation is part of the product.
7. Consistency beats cleverness.

## Writing and documentation

Help Center pages should:

- start with the user's goal;
- explain outcomes before actions;
- use short paragraphs and plain language;
- describe implemented behaviour only;
- answer one main question per page;
- include links to related guides;
- keep existing permalinks stable.

The preferred tone is friendly, practical and human, without hype.

## Making changes

When product behaviour changes:

1. Start with the user problem.
2. Describe the intended behaviour.
3. Update the relevant Help Center page.
4. Build or change the feature.
5. Test the documented workflow.
6. Record new insights in the design documents.

Documentation should be updated as part of the product change, not afterwards.

## Local preview

To preview the Help Center locally, use a Jekyll-compatible development environment and run:

```bash
bundle exec jekyll serve
```

Then open the local address shown in the terminal, usually:

```text
http://localhost:4000
```

The GitHub Pages configuration is stored in `_config.yml`.

## Links

- [Open StickyNotes.club](https://stickynotes.club)
- [Open the Help Center](https://docs.stickynotes.club)
- [Report a problem or suggest an idea](mailto:farid@stickynotes.club)

## Status

StickyNotes.club is independently developed and actively evolving.

The product documents in this repository are living documents unless explicitly marked otherwise.
