<!--
SECTION INDEX TEMPLATE

Use this when creating a new section of the documentation. Talk to the
Documentation Engineer in [#docs-channel] before you build it: a new top-level
section changes the shape of the whole site, and it is usually the wrong answer.
Most content belongs inside a section that already exists.

A new section is justified when the content serves a distinct audience or a
distinct product surface, and when it will contain enough pages to warrant its
own navigation entry. Two pages do not need a section.

Directory structure to create:

    your-new-section/
    ├── .nav.yml
    ├── index.md          <- this file
    └── your-first-page.md

The .nav.yml in the section directory:

    title: Section Display Name
    nav:
      - 'Overview': index.md
      - 'Page Display Name': 'file-name.md'
      - subdirectory-name

Notes on .nav.yml:
- `title` is what appears in the left navigation.
- `index.md` is always first in the nav list when it exists.
- Files are listed as 'Display Name': 'file-name.md'.
- Subdirectories are listed by directory name alone.
- Nav order is deliberate, not alphabetical. Order pages the way a new reader
  should meet them.

Also create the matching asset directories so contributors have somewhere
obvious to put things:

    docs/images/<section>/
    docs/.snippets/code/<section>/

Delete this comment block and every other comment in the file before opening
the PR.
-->
---
title: <!-- 60 characters or fewer. The section name. -->
description: <!-- 120 to 160 characters. What this area of the docs covers and who it serves. -->
categories: <!-- Comma-separated. Only values from categories_info in llms_config.json. -->
---

# <!-- H1. The section name as a noun phrase. -->

## Introduction

<!--
Two or three paragraphs. A section landing page has one job: a reader who
arrives here should know within fifteen seconds whether this section holds what
they need, and where to click next.

Cover:
- What this section covers, in one or two sentences.
- Who it is for, and what they are assumed to know already.
- What it does not cover, with a link to wherever that content lives instead.

Do not write a product pitch. Do not restate the contents of every child page.
-->

## <!-- Optional: orientation heading, e.g. "How the Pieces Fit Together". -->

<!--
When the section covers a system with several parts, a short orientation
section or a diagram here saves the reader from assembling the mental model
themselves across five pages.

![Descriptive alt text for the diagram.](/images/<section>/<section-name>-01.webp)
-->

## Get Started

<!--
Signposting to the child pages, grouped by reader intent rather than listed
flat. Use description-list format consistently.

If the reader is new to this area:

- [Title of the Concept Page](/path/to/page/): One line on what it explains.
- [Title of the First Tutorial](/path/to/page/): One line on what they will build.

If the reader has a specific task:

- [Title of the Guide](/path/to/page/): One line on the task it covers.

If the reader needs exact values:

- [Title of the Reference Page](/path/to/page/): One line on what it documents.

Keep this list current when pages are added. A landing page that omits half the
section is a discoverability problem, and the left navigation does not replace
it, because readers arriving from search do not scan the nav.
-->
