---
name: polkadot-docs-contribution
description: Write, edit, review, or plan content for the Polkadot developer documentation at docs.polkadot.com (the polkadot-developers/polkadot-docs MkDocs repository). Covers page templates, required frontmatter, file and asset placement, .nav.yml registration, snippets, the full documentation style guide, Vale linting, and the pull request workflow. Use this skill whenever the user is writing or editing any Polkadot documentation page, drafting a tutorial, guide, concept, or reference page, adding a new docs section, planning documentation for a product launch, reviewing a docs pull request, or asking where content should live in the docs. Use it even when the user only asks for "a quick page", "a short doc", or "just fix this page" — the conventions apply to every change, and a page that ignores them fails review or CI.
---

# Contributing to the Polkadot Developer Documentation

This skill produces content for [`polkadot-developers/polkadot-docs`](https://github.com/polkadot-developers/polkadot-docs), the MkDocs site published at `docs.polkadot.com`.

The repository is public and the site is open source. Contributions come from Parity internal teams who own the products being documented, and from external contributors. In both cases the Documentation Engineer (`@bucanero`, Builder Experience) reviews and owns the documentation system: information architecture, style, tooling, and review. The team that builds the product owns the accuracy of its pages.

That division matters for how this skill behaves. The person you are helping holds knowledge you do not have. Your job is to give them correct structure, correct formatting, and clean prose, and to be explicit about every place where you are guessing.

## The Rule That Overrides Everything Else

**Never invent technical content.** Not a method name, not a parameter, not a CLI flag, not an error string, not a version number, not terminal output, not a behaviour.

Documentation that is fluent and wrong is worse than no documentation, because readers act on it and support absorbs the cost. This is the single highest-risk failure mode when an AI agent drafts documentation, and it is invisible to the reviewer, who cannot verify your claims either.

When you do not know something, do not produce a plausible version of it. Leave a marker the human cannot miss:

```markdown
<!-- VERIFY: parameter list taken from the issue description, not from source. Confirm against the runtime before merging. -->
```

Use `<!-- VERIFY: ... -->` for anything you inferred, and `<!-- TODO: ... -->` for anything you left blank. At the end of your work, list every marker you left so the human knows exactly what needs checking. A draft with ten honest gaps is more useful than a complete-looking draft with two invented facts buried in it.

Never write terminal output from imagination. Ask the human to paste a real run.

## Step 1: Establish What Kind of Change This Is

Three paths, and they carry different obligations. Identify which one applies before writing anything.

**Path 1 — Fixing or improving an existing page.** Typos, wrong output, an outdated parameter, a clarification, a new example on a page that already exists. No permission needed, no planning document. Go straight to editing, then open a pull request.

**Path 2 — Adding a new page inside a section that already exists.** The author should check placement with the Documentation Engineer in the docs channel before writing, because misplaced content is the most expensive thing to fix after publication. If the user has not done this, say so once, then help them draft; a draft in the wrong directory is still recoverable, and stalling them is not helpful.

**Path 3 — A new section, a new product, or a launch.** This needs an information architecture proposal and a documentation plan, agreed with the Documentation Engineer 4 to 6 weeks before the launch date. If the user is asking you to bulk-generate a whole new section without that conversation having happened, tell them plainly that placement decisions made now will likely be redone, and offer to help them fill in the documentation plan template instead.

## Step 2: Pick the Page Type

Four page types. The distinction is what the reader is doing while reading, and mixing two types on one page is the most common structural problem in review.

| Type | The reader is | Signals it is the right choice |
| :--: | :-----------: | :----------------------------: |
| Concept | Trying to understand something before deciding to use it | "What is X", "how does X work", "when should I use X" |
| How-to guide | Executing one specific task, entering the page at any point | "How do I do X" where the reader already knows why |
| Tutorial | Learning by building, reading start to finish in order | "Build X from nothing", teaching a workflow |
| Reference | Looking up an exact value, signature, or name | Parameters, extrinsics, methods, errors, CLI flags, config keys |

If a guide stops to explain architecture for four paragraphs, that explanation belongs on a concept page and the guide should link to it. If a reference page has narrative sections, it is two pages.

## Step 3: Get the Templates

Templates live in the public [`paritytech/polkadot-docs-templates`](https://github.com/paritytech/polkadot-docs-templates) repository:

```
polkadot-docs-templates/
├── README.md                       Conventions, decision table, linting, variables
├── page-concept.md                 Concept page skeleton
├── page-how-to-guide.md            Task-oriented guide skeleton
├── page-tutorial.md                End-to-end tutorial skeleton, with badge and test frontmatter
├── page-reference.md               API, extrinsic, parameter, and error reference skeleton
├── section-index.md                Section landing page plus .nav.yml structure
├── documentation-plan.md           Intake document for a launch or a new product
└── pr-self-review-checklist.md     Pre-review self-check
```

Fetch the template for the page type you identified and start from it rather than composing a page from scratch:

```bash
# Raw file, for a single template
curl -O https://raw.githubusercontent.com/paritytech/polkadot-docs-templates/main/page-how-to-guide.md

# Or clone once and copy from it
git clone https://github.com/paritytech/polkadot-docs-templates.git
cp polkadot-docs-templates/page-how-to-guide.md docs/<section>/<subsection>/<page-name>.md
```

If you cannot reach the repository, use the skeletons in the "Page Blueprints" section of this skill, which mirror the templates.

Templates contain HTML comments carrying inline guidance. **Delete every comment and every bracketed instruction before the page is finished.** Leftover scaffolding in a pull request is the fastest route to a rejected review.

## Step 4: Place the File

Naming rules, all mandatory:

- kebab-case, lowercase, no spaces, no special characters.
- Descriptive of the content: `submit-a-transaction.md`, not `guide2.md`.
- Correct extension for the file type.

Assets mirror the documentation structure exactly. For a page at `docs/<section>/<subsection>/<page-name>.md`:

```
docs/images/<section>/<subsection>/<page-name>/
docs/.snippets/code/<section>/<subsection>/<page-name>/
```

Register the page in the `.nav.yml` of its directory:

```yaml
- 'Your Page Display Name': 'your-file-name.md'
```

For a new section, create the directory with its own `.nav.yml`:

```yaml
title: Section Display Name
nav:
  - 'Overview': index.md
  - 'Page Display Name': 'file-name.md'
  - subdirectory-name
```

`index.md` always comes first when it exists. Files use `'Display Name': 'file-name.md'`. Subdirectories are listed by directory name alone. Nav order is deliberate, not alphabetical: order pages the way a new reader should meet them.

## Step 5: Write the Frontmatter

Every page opens with a YAML block. Three fields are required.

| Field | Constraint |
| :---: | :--------: |
| `title` | 60 characters or fewer, for search results |
| `description` | 120 to 160 characters |
| `categories` | Comma-separated, values only from `categories_info` in `llms_config.json` at the repository root |

**Read `llms_config.json` before setting `categories`.** Do not guess a category name. If you cannot read the file, leave `<!-- TODO: set categories from llms_config.json -->` and say so.

Optional fields, used when they apply:

- `short_description`: Shorter text for auto-generated index tables. Falls back to `description`.
- `tools`: Tools used on the page, shown in index tables. String or YAML list.
- `hide`: List. Accepts `navigation` and `toc`.
- `footer_nav`: `true` to include in footer navigation, or an integer for explicit order.
- `extra_javascript` / `extra_css`: Per-page assets for interactive widgets.
- `page_badges.tutorial_badge`: `Beginner`, `Intermediate`, or `Advanced`. Required on tutorials; also drives the Difficulty column in index tables.
- `page_badges.test_workflow`: Workflow filename without `.yml`, from `polkadot-developers/polkadot-cookbook`.
- `page_tests.path`: Path to a test file relative to the root of `polkadot-developers/polkadot-cookbook`. Renders a "View tests" link.
- `toggle`: Groups page variants (for example EVM and PVM) behind a switcher. All pages in a group share `group`; each sets `variant` and `label`; one sets `canonical: true`.
- `template`: Only used on the homepage.

Example for a tutorial:

```yaml
---
title: Build a Multisig Transfer Script
description: Create, sign, and submit a multisig transfer using the Polkadot API, from project setup through on-chain verification.
categories: INSERT_CATEGORY
page_badges:
  tutorial_badge: Intermediate
---
```

## Step 6: Use the Right Content Elements

**Code blocks** always carry a language shortcode: ` ```js `, ` ```rust `, ` ```bash `, ` ```json `, ` ```py `, ` ```solidity `. A block without one loses syntax highlighting.

**Snippets** hold anything longer than a few lines, and anything reused across pages. Store under `docs/.snippets/code/<path-matching-doc-structure>/` and transclude:

```text
--8<-- 'code/<subdirectory>/<snippet-file-name>.js'
--8<-- 'code/<subdirectory>/<snippet-file-name>.js:10:20'
```

The line-range form lets a tutorial walk through one part of a file at a time. Never inline code that already exists as a snippet. Text snippets are `.md`; code snippets use the language extension.

**Shared variables** live in `variables.yml` at the repository root, referenced as `{{ variable_name }}`. Check it before writing any version number into a page. A hardcoded version needs a manual edit on every release, and it is the edit nobody remembers.

**Images** are `.webp`, stored at `docs/images/<path-matching-doc-structure>/`, named `<page-name>-01.webp` with a zero-padded sequence reflecting order on the page:

```markdown
![Descriptive alt text.](/images/<section>/<subsection>/<page-name>/<page-name>-01.webp)
```

Desktop screenshots are 1512px wide with variable height. Browser extension screenshots are 400x600px, at 300 DPI and 150% zoom, in dark mode where the site offers both themes, including the full browser window with the address bar. Annotate with arrows from `.assets/annotations`; if more than one arrow is needed, number them and match an ordered list in the prose. Informative images get descriptive alt text. Decorative images, including screenshots whose information is already in the surrounding text, use empty `alt=""` so assistive technology skips them.

**Callouts** replace bolding a sentence for emphasis. Content indents four spaces:

```markdown
!!! note
    Information the reader should retain.

!!! tip
    A shortcut or a better path.

!!! warning
    A risk, a caveat, or anything that can cost funds or data.
```

**Terminal output** uses termynal, showing the command, the output, and a blank prompt at the end when the command returns control to the shell:

```html
<div class="termynal" data-termynal>
    <span data-ty="input"><span class="file-path"></span>INSERT_COMMAND</span>
    <span data-ty="progress"></span>
    <span data-ty>INSERT_OUTPUT</span>
    <span data-ty="input"><span class="file-path"></span></span>
</div>
```

**External links** open in a new tab automatically through the MkDocs plugin. Never add `{target=_blank}` by hand.

## Step 7: Apply the Style Rules

The canonical sources are [`AGENTS.md`](https://github.com/polkadot-developers/polkadot-docs/blob/master/AGENTS.md) at the root of `polkadot-docs`, which is loaded automatically by agents working in a clone, and the [documentation style guide](https://github.com/papermoonio/documentation-style-guide) it points to. Precedence when rules conflict:

1. `polkadot-docs/AGENTS.md`. Project-specific overrides win.
2. The canonical style guide.
3. The [Google developer documentation style guide](https://developers.google.com/style), as fallback.

Apply these rules while generating, not as a cleanup pass afterwards.

### Voice and tone

- Formal, confident, neutral. No slang, no sales language, no emotional framing.
- Address the reader as "you". Avoid "we", "our", and "let's" outside informal tutorials.
- Active voice in instructional content. Passive voice is acceptable in conceptual content.
- Short sentences. Provide context rather than assuming the reader has it.
- Contractions sparingly. Expand them (`do not`, `cannot`, `it is`) in reference and conceptual pages.
- Write timeless documentation. Nothing anchored to the moment of writing.
- Define every acronym on first use, on every page.

### Banned phrases

Rewrite or delete these wherever they appear:

| Banned | Use instead |
| :----: | :---------: |
| delve into, dive into | Omit, or "explore", "walk through" |
| leverage | use |
| utilize | use |
| seamless, seamlessly | Omit |
| robust | Omit, or be specific: "production-tested", "fault-tolerant" |
| powerful, cutting-edge, state-of-the-art | Omit |
| simply, just, easily, obviously | Omit. Never describe a step as easy |
| it's important to note that | Omit and state the thing |
| it's worth noting that | Omit |
| in summary, in conclusion | Omit. Structure carries it |
| feel free to | Omit |
| under the hood | Omit, or "internally" |
| in today's world, in the modern era | Omit |
| currently, at the time of writing | Omit. Write timeless docs |
| etc. | "and more" or "and so on" |

### Formatting

- **Bold** is only for UI element names and for the term in a description list. Nothing else. Never bold for emphasis, never bold a sentence.
- `_Italics_` for drawing attention to a single word or phrase, such as introducing a new term.
- Never underline.
- No emoji anywhere: not in headings, prose, bullets, or callouts. For comparisons use the text labels `Do:` and `Do not:`.
- No ampersands unless naming a UI element that contains one.
- No exclamation marks.
- Em dash `—` (U+2014), spaced, at most one per sentence; rewrite the paragraph if it needs two. Never `--`. En dash `–` only for numeric ranges. Hyphen for compounds and identifiers.
- Oxford commas. Colons rather than dashes to introduce lists.
- Double quotes in prose, with commas and periods inside them. Single quotes only in code, where the language convention calls for them.
- Chicago title case in titles and headings. Capitalize product names. Avoid capitalizing anything else without a reason.
- Spell out zero through nine in prose; digits for 10 and above. Always digits for versions, measurements, CLI flags, and anything inside a table.

### Headings

- Exactly one H1 per page. Headings descend without skipping levels.
- Task headings are imperative: "Create an Instance", not "Creating an Instance".
- Conceptual headings are noun phrases that do not start with an `-ing` verb: "Blockchain Consensus Mechanisms", not "Understanding Blockchain Consensus".
- No numbers in headings.
- Never put a subheading directly above a list that a lead-in sentence already introduces. Replace it with a sentence or drop it.

### Lists

- Numbered lists for sequences. Bulleted lists for everything else.
- All items share a grammatical form: all verb phrases, or all noun phrases.
- Capitalize the first letter unless case carries meaning, as with `kebab-case` identifiers.
- End each item with a period, except when the item is a single word, contains no verb, is entirely in code font, or is entirely link text or a document title.
- **Never mix punctuated and unpunctuated items in one list.** If they come out inconsistent, rewrite for parallel construction or punctuate every item.
- A numbered step ending in a colon is already punctuated. Do not add a period after the colon.
- Description lists use `**Term**: Description.` — bold term, capitalized, colon, capitalized description, closing period. If one item in a list uses this format, every item must. Never mix description-list bullets with free-form bullets.

### Links

Descriptive link text, using the target page's title. Never "here", "this", "click here", "read more", or "learn more". No inline formatting on links.

```markdown
Do:     See the [project's faucet](https://example.com/faucet/) for test tokens.
Do not: Get test tokens [here](https://example.com/faucet/).
```

### Accessibility

Hierarchical headings, alt text on informative images, descriptive link text, and no directional language: avoid "above", "below", and "the following section", which break for screen readers and on reflowed layouts.

### Terminology

| Use | Not |
| :-: | :-: |
| ERC-20, ERC-721, ERC-1155 | ERC20, ERC 20 |
| JSON-RPC | JSON RPC, JSONRPC |
| dApp | dapp, DApp (DApp only sentence-initial or in a title-case heading) |
| TestNet | testnet, test net |
| MainNet | mainnet, main net |
| smart contract | smart-contract, except as a compound adjective: `smart-contract platform` |
| supermajority | super majority, super-majority |
| and more, and so on | etc. |

Token standards take a dash between the prefix and the identifier. Hyphenated identifiers such as config flags, CLI options, release profiles, and package names keep their canonical casing on every mention: never capitalize one because it starts a sentence. Rephrase the sentence instead.

### Code identifiers in prose

Wrap every code identifier in backticks, on every mention: function and method names, module, type, and class names, variables and parameters, and file paths. Dropping backticks on the second or third mention is the most consistently flagged AI-generated defect in review.

Identifier consistency within a page is absolute. If you write `getUserId` once, never switch to `get_user_id` later. Use the form that appears in the source code. The same applies to terms: do not call a role "author" in one paragraph and "editor" in the next unless they are genuinely distinct roles on that page.

### Code formatting by language

| | JavaScript / TypeScript | JSON | Python | Solidity |
| :-: | :-: | :-: | :-: | :-: |
| Formatter | Prettier | Prettier | Black | Prettier Solidity plugin |
| Indent | 2 spaces | 4 spaces | 4 spaces | 4 spaces |
| Max line | 80 | 80 | 80 | 80 |
| Quotes | single | double | double | double |
| Trailing comma | yes | no | yes | no |
| Semicolons | yes | no | no | no |

Python uses snake_case; JavaScript uses camelCase. Declare root-level variables at the top, after imports and before functions. Reserve all-uppercase names for exported constants.

### Placeholder values

Any value the reader must supply becomes a variable with an `INSERT_` placeholder: uppercase, snake_case, descriptive, starting with `INSERT`, never using `HERE` or another generic suffix, quoted when the value requires quoting.

```js
Do:     const contractAddress = 'INSERT_CONTRACT_ADDRESS';
Do:     const amount = INSERT_AMOUNT_TO_SEND;
Do not: const address = 'INSERT_CONTRACT_ADDRESS_HERE';
Do not: const address = 'INSERT-CONTRACT-ADDRESS';
```

When creating variables for function arguments, name them after the parameters. For `execute(dest, weight)`, use `dest` and `weight`, not `xcmDest` and `xcmWeight`.

## Page Blueprints

Use these when the templates repository is unavailable. Section headings are the expected shape, not a rigid requirement: drop what does not apply rather than padding.

**Concept**: Introduction (topic, the existing approach and its limits, how this addresses them, what the page covers) → one section per idea, noun-phrase headings → How It Works, with a diagram if the mechanism is spatial → optional comparison table when two mechanisms overlap → Constraints and Limitations → Where to Go Next.

The limitations section is the highest-value part of a concept page and the most commonly omitted. Hard limits and their values, known failure modes, unsupported combinations, and anything that surprises people in practice.

**How-to guide**: Introduction, one or two paragraphs, linking out for background → Prerequisites, specific and version-pinned → task sections with imperative headings and numbered steps → Verify the Result → optional Troubleshooting table → Where to Go Next.

Omitting verification is the most common defect in guides: without it the reader cannot distinguish finished from silently broken.

**Tutorial**: Introduction (what they build, what they learn, scope) → Prerequisites including assumed knowledge → action-oriented step sections → Verification, mandatory → optional Troubleshooting → Where to Go Next. Every code example tested and functional, every dependency version specified. Place the tutorial under the most relevant existing section, not in a separate tutorials silo.

**Reference**: Short introduction, or none → one subsection per item in a consistent order, each with signature, description, parameter table, returns, events, errors, and cost → Errors table with literal error strings → Limits and Defaults → Where to Go Next.

Exhaustiveness matters more here than anywhere else: a reference page missing three of twelve parameters is worse than none, because the reader cannot tell it is incomplete. Where a generated source of truth exists (rustdoc, an OpenAPI spec, type definitions), link to it rather than transcribing it.

**Section index**: Introduction (what the section covers, who it serves, what it does not cover) → optional orientation section or diagram → Get Started, signposting child pages grouped by reader intent rather than listed flat.

## Step 8: Verify Before Handing Back

Run these in order. Do not report the work as done until they pass or until you have told the user exactly what did not.

```bash
./.github/scripts/sync-styleguide-vale.sh   # pull canonical Vale rules and vocab
vale .                                      # lint
```

Vale runs in CI against every changed markdown file on every pull request, so a local run only moves the failure earlier. It catches most mechanical style violations. It catches nothing in the accuracy or structure categories.

If Vale flags a legitimate Polkadot term, the fix is to add it to `styles/config/vocabularies/Polkadot/`, which is committed to the repository, and to mention that in the pull request. The `styles/PaperMoon/` directories are gitignored and pulled fresh on every run: never edit them.

Then build the site locally and read the rendered page in a browser, following the instructions in the repository README. Broken snippet paths, broken image paths, and nav registration mistakes do not surface any other way.

## Pre-Output Checklist

Run this before returning a draft. Check each item against the actual text, not against your intent.

**Accuracy**
- [ ] No invented method, parameter, flag, error string, version, or behaviour.
- [ ] Every unverified claim carries a `<!-- VERIFY: ... -->` marker, and every marker is listed in your summary.
- [ ] No fabricated terminal output.
- [ ] Versions come from `variables.yml` where a shared value exists.
- [ ] Identifiers match the source exactly in spelling, casing, and form.

**Frontmatter and placement**
- [ ] `title` present, 60 characters or fewer.
- [ ] `description` present, 120 to 160 characters.
- [ ] `categories` present and drawn from `llms_config.json`.
- [ ] Tutorials set `tutorial_badge`.
- [ ] File name is kebab-case and descriptive; the page sits in the right section.
- [ ] Page registered in `.nav.yml` at a deliberate position.
- [ ] Asset directories mirror the docs path; images are `.webp` with `-01` sequence naming.

**Structure**
- [ ] The page is one type and does not drift between two.
- [ ] One H1; headings descend without skipping.
- [ ] Task headings imperative; concept headings noun phrases; no numbers in headings.
- [ ] No subheading directly above a lead-in list.
- [ ] Guides and tutorials have complete prerequisites and a verification section.

**Language and formatting**
- [ ] No banned phrases; no step described as easy.
- [ ] No time-anchored language; no first person; no directional language.
- [ ] Bold only on UI elements and description-list terms.
- [ ] No emoji, no exclamation marks, no manual `{target=_blank}`.
- [ ] At most one em dash per sentence, written as `—`.
- [ ] List punctuation consistent throughout each list; description lists uniform.
- [ ] Every code block has a language shortcode; every identifier in prose is backticked, including in tables.
- [ ] Link text descriptive, never "here" or "learn more".
- [ ] Every template comment and bracketed instruction deleted.

## Step 9: The Pull Request

Simple text changes can go through the GitHub web editor: edit the file, use **Propose changes**, and check **Allow edits from maintainers**. Anything involving `.nav.yml`, snippets, images, or rendering needs a fork and a local build.

```bash
git clone https://github.com/YOUR_USERNAME/polkadot-docs.git
cd polkadot-docs
git checkout -b YOUR_FEATURE_BRANCH
```

In the pull request:

- Describe what changed and why, linking the issue or launch if one exists.
- Use the PR template to indicate review preference.
- Check **Allow edits from maintainers** so small fixes do not need a round trip.
- Request review from `@bucanero`.
- Say explicitly if the change is release-blocking, and name the date.
- List every `<!-- VERIFY: -->` marker still in the diff, so the reviewer knows the author has not yet confirmed them. Markers must be resolved and removed before merge.

## How to Report Back to the User

End with a short summary containing:

1. What you produced and where each file goes.
2. Every `VERIFY` and `TODO` marker, as a list, stated as things only they can confirm.
3. Anything you deliberately left out, and why.
4. The next concrete step: run Vale, build locally, confirm the examples, request review.

Do not claim a page is complete when it contains markers. Do not claim code works when nobody has run it. The value of an AI draft is that it arrives with correct structure and honest gaps, and the person who owns the product fills the gaps in minutes rather than writing the page from nothing.
