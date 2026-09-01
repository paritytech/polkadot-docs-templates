<!--
HOW-TO GUIDE TEMPLATE

Use this when the reader has one specific task and wants the shortest correct
path through it. The reader is assumed to already know why they are doing this.

A how-to guide is not a tutorial. A tutorial teaches by building something from
nothing and is read start to finish. A guide is consulted for one job and may be
entered at any point. If your page teaches rather than instructs, use
page-tutorial.md instead.

Resist explaining concepts inline. Link to the concept page and keep moving.

Delete this comment block and every other comment in the file before opening
the PR.

Save to:   docs/<section>/<subsection>/<page-name>.md
Assets:    docs/images/<section>/<subsection>/<page-name>/
Snippets:  docs/.snippets/code/<section>/<subsection>/<page-name>/
-->
---
title: <!-- 60 characters or fewer. Task-based and imperative: "Deploy a Contract With Hardhat". -->
description: <!-- 120 to 160 characters. State the task and the tool or context. -->
categories: <!-- Comma-separated. Only values from categories_info in llms_config.json. -->
---

# <!-- H1. Imperative task heading: "Deploy a Contract", not "Deploying a Contract". -->

## Introduction

<!--
One or two paragraphs, no more. Cover:

- What the reader will accomplish by the end of the page.
- The context or tool this applies to, and any variant it does not apply to.
- A link to the relevant concept page for readers who need background.

Do not restate the whole procedure here.
-->

## Prerequisites

<!--
Everything the reader must have in place before step one. Be specific and
version-pinned. A guide that fails at step three because of an unstated
dependency generates support load.

Use description-list format, and note the style guide rule: if one item uses
`**Term**: Description.`, every item in the list must.

- **Node.js**: Version 20 or later installed.
- **Funded account**: An account on INSERT_NETWORK_NAME with a balance sufficient to cover fees.
- **RPC endpoint**: A WebSocket endpoint for the target network.

If prerequisites require their own setup pages, link to them rather than
duplicating the instructions.
-->

## <!-- First task section. Imperative: "Install the Dependencies". -->

<!--
Numbered steps for anything sequential. Each step is one action.

The style guide rule for numbered steps: a step label ending in a colon counts
as punctuated, so do not add a trailing period after the colon.

1. Install the required packages:

    ```bash
    npm install polkadot-api@INSERT_VERSION
    ```

2. Create the configuration file:

    ```js
    --8<-- 'code/<section>/<subsection>/<page-name>/config.js'
    ```

Always pin dependency versions in commands. An unpinned command is correct for
a shrinking window of time.

Never write "simply run" or "just add". Never describe a step as easy.
-->

## <!-- Second task section. -->

<!--
Show terminal output where the reader needs to confirm what they should see:

<div class="termynal" data-termynal>
    <span data-ty="input"><span class="file-path"></span>INSERT_COMMAND</span>
    <span data-ty>INSERT_OUTPUT</span>
    <span data-ty="input"><span class="file-path"></span></span>
</div>

For UI steps, use a screenshot with numbered arrow annotations from
.assets/annotations, and an ordered list in the prose that matches the numbers:

![](/images/<section>/<subsection>/<page-name>/<page-name>-01.webp)

Screenshots whose information is already in the surrounding text are decorative.
Use empty alt text so assistive technology skips them.
-->

## Verify the Result

<!--
How the reader confirms it worked. A command to run, a value to check, a state
to observe, with the expected output shown.

Omitting this section is the most common defect in guides. Without it the reader
cannot distinguish "finished" from "silently broken".
-->

## Troubleshooting

<!--
Optional but high value. The errors people actually hit, in a table.

Include the literal error string where you can, because that is what the reader
pastes into search.

|             Error             |             Cause             |            Resolution           |
|:-----------------------------:|:-----------------------------:|:-------------------------------:|
| `INSERT_ERROR_MESSAGE`        |                               |                                 |
-->

## Where to Go Next

<!--
Two to four links with descriptive link text. The natural next task, the
reference page for what was used here, and the concept page for deeper context.
-->
