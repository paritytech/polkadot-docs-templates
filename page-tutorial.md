<!--
TUTORIAL TEMPLATE

Use this when the reader learns by building something end to end. A tutorial is
read start to finish, in order, and every step must work for a reader who has
only the prerequisites listed.

Tutorials carry the highest maintenance cost of any page type, because they break
whenever any dependency in the chain changes. Before writing one, be sure a
how-to guide would not serve the reader as well.

Tutorial-specific requirements from CONTRIBUTING.md:
- Every code example must be tested and functional.
- Every dependency version must be specified.
- Section titles must be action-oriented.
- Verification steps are mandatory.

Place the tutorial under the most relevant existing section rather than in a
separate tutorials silo.

Delete this comment block and every other comment in the file before opening
the PR.

Save to:   docs/<section>/<subsection>/<tutorial-name>.md
Assets:    docs/images/<section>/<subsection>/<tutorial-name>/
Snippets:  docs/.snippets/code/<section>/<subsection>/<tutorial-name>/
-->
---
title: <!-- 60 characters or fewer. What the reader builds. -->
description: <!-- 120 to 160 characters. -->
categories: <!-- Comma-separated. Only values from categories_info in llms_config.json. -->
page_badges:
  tutorial_badge: <!-- Beginner, Intermediate, or Advanced. Also drives the Difficulty column in index tables. -->
  test_workflow: <!-- Optional. Filename of the GitHub Actions workflow without .yml, from polkadot-developers/polkadot-cookbook. -->
page_tests:
  path: <!-- Optional. Path to the test file, relative to the root of polkadot-developers/polkadot-cookbook. Renders a "View tests" link. -->
---

# <!-- H1. What the reader builds: "Build a Multisig Transfer Script". -->

## Introduction

<!--
Two or three paragraphs:

- What the reader will have built by the end, concretely.
- What they will learn along the way.
- The approximate scope, and any variant this does not cover.

If a finished version of the code exists in a repository, link to it here. Some
readers want to run it first and read second.
-->

## Prerequisites

<!--
Everything required, version-pinned. Tutorials are entered by less experienced
readers than guides are, so be more explicit than feels necessary.

- **Node.js**: Version 20 or later.
- **Package manager**: `npm` version 10 or later.
- **Funded account**: An account on INSERT_NETWORK_NAME with at least INSERT_AMOUNT for fees.
- **Prior reading**: [Title of the Prerequisite Concept Page](/path/to/page/).

Assumed knowledge counts as a prerequisite. Say so if the reader needs to be
comfortable with a language or a toolchain.
-->

## <!-- First step section. Action-oriented: "Set Up the Project". -->

<!--
Numbered steps. Each step is one action, with the command or code that performs
it and, where useful, the output that confirms it.

1. Create the project directory and initialize it:

    ```bash
    mkdir INSERT_PROJECT_NAME && cd INSERT_PROJECT_NAME
    npm init -y
    ```

2. Install the dependencies, pinned to a known-good version:

    ```bash
    npm install polkadot-api@INSERT_VERSION
    ```

Store anything longer than a few lines as a snippet so it can be tested in CI
and fixed in one place:

    ```js
    --8<-- 'code/<section>/<subsection>/<tutorial-name>/index.js'
    ```

The snippet syntax supports line ranges when you want to walk through one part
of a file at a time:

    ```js
    --8<-- 'code/<section>/<subsection>/<tutorial-name>/index.js:10:20'
    ```
-->

## <!-- Second step section. -->

<!--
Explain what each piece of code does before or after showing it, not inside it
as a wall of comments. The reader needs to understand why, not just copy.

Keep concept explanation to a couple of sentences and link out for the rest.
-->

## <!-- Third step section: usually running or deploying the thing. -->

<!--
Show the command and its real output in a termynal block:

<div class="termynal" data-termynal>
    <span data-ty="input"><span class="file-path"></span>INSERT_COMMAND</span>
    <span data-ty="progress"></span>
    <span data-ty>INSERT_OUTPUT</span>
    <span data-ty="input"><span class="file-path"></span></span>
</div>

Copy real output. Do not paraphrase it from memory, because readers compare
character by character when something goes wrong.
-->

## Verification

<!--
Mandatory. How the reader proves the thing works: a command, an expected value,
a block explorer view, a returned hash. Show what success looks like.

If there are several success signals, list them so a reader who gets a partial
result can identify which stage failed.
-->

## Troubleshooting

<!--
Optional but strongly recommended for tutorials, because a stuck reader
abandons the page.

|             Error             |             Cause             |            Resolution           |
|:-----------------------------:|:-----------------------------:|:-------------------------------:|
| `INSERT_ERROR_MESSAGE`        |                               |                                 |
-->

## Where to Go Next

<!--
Two to four links with descriptive link text: the next tutorial in the
progression, the reference for the API used, or the concept page that explains
what was built.
-->
