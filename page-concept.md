<!--
CONCEPT PAGE TEMPLATE

Use this when the reader is trying to understand something: what it is, why it
exists, how it fits with everything else, and whether they should use it.

A concept page does not contain step-by-step instructions. If you find yourself
writing "run this command", that content belongs in a how-to guide, and this
page should link to it.

Delete this comment block and every other comment in the file before opening
the PR.

Save to:   docs/<section>/<subsection>/<page-name>.md
Assets:    docs/images/<section>/<subsection>/<page-name>/
Snippets:  docs/.snippets/code/<section>/<subsection>/<page-name>/
-->
---
title: <!-- 60 characters or fewer. Chicago title case. -->
description: <!-- 120 to 160 characters. Written for search results: what the page covers and who it is for. -->
categories: <!-- Comma-separated. Only values from categories_info in llms_config.json. -->
---

# <!-- H1 title. May differ from the frontmatter title. Noun phrase, not a gerund. -->

## Introduction

<!--
Two or three paragraphs. The style guide's recipe, in order:

1. Introduce the topic in one or two sentences.
2. Describe the existing approach and its limitations, so the reader can see
   the problem this thing solves.
3. Explain how this addresses those limitations.
4. Say briefly what the rest of the page covers.

Do not assume the reader knows why they are here. A reader who lands on this
page from a search engine has no context from the surrounding navigation.

Define every acronym on first use.
-->

## <!-- First concept heading. Noun phrase: "Storage Deposits", not "Understanding Storage Deposits". -->

<!--
Explain one idea per section. Passive voice is acceptable in conceptual content.

If a section runs past roughly six paragraphs, it is probably two concepts and
should be split into two headings, or the page should be split into two pages.
-->

## How It Works

<!--
The mechanism. What happens, in what order, and what the reader can observe.

A diagram earns its place here more than anywhere else in the docs. Diagrams
are .webp files with consistent line weight, font, and shape sizing:

![Descriptive alt text for the diagram.](/images/<section>/<subsection>/<page-name>/<page-name>-01.webp)

Keep the text inside a diagram minimal. Anything that needs a sentence belongs
in the prose, not in the image.
-->

## <!-- Optional: comparison or decision heading, e.g. "Bundles Compared With Batches". -->

<!--
When two mechanisms overlap, readers need to know which one to reach for. A
table is usually clearer than prose. Table headers and values are centered, and
the table should be formatted (the Markdown Table Formatter extension does this).

| Property | Option A | Option B |
|:--------:|:--------:|:--------:|
|          |          |          |
-->

## Constraints and Limitations

<!--
What this does not do, what it costs, and where it breaks. This section is
consistently the most valuable one on a concept page and the most commonly
omitted.

Include: hard limits and their values, known failure modes, unsupported
combinations, and anything that surprises people in practice.

Use a warning callout for anything that can cause loss of funds or data:

!!! warning
    Description of the risk and how to avoid it.
-->

## Where to Go Next

<!--
Two to four links, each with descriptive link text using the target page's
title. Prefer the how-to guides and tutorials that put this concept into
practice.

- [Title of the Target Page](/path/to/page/): One line on why the reader would go there.
-->
