# PR Self-Review Checklist

Work through this before requesting review from `@bucanero`. It takes a few minutes and removes most review round trips, which means your PR merges the same day instead of three days later.

Copy the relevant section into your PR description if that helps you track it.

## Accuracy

The reviewer cannot verify any of this. It is yours.

- [ ] Every code example has been run, against the version stated on the page.
- [ ] Every dependency version is pinned in install commands.
- [ ] Every identifier matches the source code exactly: spelling, casing, and form.
- [ ] Terminal output is copied from a real run, not written from memory.
- [ ] Screenshots reflect the shipped UI, not a pre-release build.
- [ ] Every claim about behaviour is something you have observed or read in the code.
- [ ] Placeholder values use the `INSERT_` convention and describe the value: `INSERT_CONTRACT_ADDRESS`, not `YOUR_ADDRESS` or `INSERT_ADDRESS_HERE`.

## Frontmatter and Build

- [ ] `title` is present and 60 characters or fewer.
- [ ] `description` is present and 120 to 160 characters.
- [ ] `categories` is present, and every value exists in `categories_info` in `llms_config.json`.
- [ ] Tutorials set `page_badges.tutorial_badge` to `Beginner`, `Intermediate`, or `Advanced`.
- [ ] The page is registered in the `.nav.yml` of its directory, in a deliberate position.
- [ ] The site builds locally and you have read the rendered page in a browser.
- [ ] Every internal link resolves. Every external link opens.
- [ ] Every snippet transclusion resolves and renders the code you expect.
- [ ] Every image renders and its path matches the docs structure.

## Files and Assets

- [ ] File name is kebab-case, lowercase, no spaces or special characters, and describes the content.
- [ ] The page lives under the section that matches its subject, not in a new directory created for convenience.
- [ ] Images are `.webp`, stored at `docs/images/<path-matching-doc-structure>/`.
- [ ] Image file names follow `<page-name>-01.webp` with a zero-padded sequence matching order on the page.
- [ ] Desktop screenshots are 1512px wide. Browser extension screenshots are 400x600px.
- [ ] Code longer than a few lines lives in `docs/.snippets/code/<path-matching-doc-structure>/`, not inline.
- [ ] Informative images have descriptive alt text. Decorative images use empty `alt=""`.

## Structure

- [ ] The page is one type: concept, how-to guide, tutorial, or reference. It does not drift between two.
- [ ] There is exactly one H1, and headings descend without skipping levels.
- [ ] Task headings are imperative: "Create an Instance", not "Creating an Instance".
- [ ] Concept headings are noun phrases and do not start with an `-ing` verb.
- [ ] No numbers in headings.
- [ ] No subheading sits directly above a list that a lead-in sentence already introduces.
- [ ] Guides and tutorials have a prerequisites section that is complete enough for someone outside your team.
- [ ] Guides and tutorials have a verification section showing what success looks like.
- [ ] Concepts explained at length link out instead of being duplicated inline.

## Language

- [ ] No banned phrases: delve into, dive into, leverage, utilize, seamless, robust, powerful, cutting-edge, simply, just, easily, obviously, it's important to note that, it's worth noting that, in summary, in conclusion, feel free to, under the hood, in today's world, currently, at the time of writing, etc.
- [ ] No step is described as easy, simple, or quick.
- [ ] No time-anchored language. The page reads correctly a year from now.
- [ ] No first person. The reader is addressed as "you". No "we", "our", or "let's" outside informal tutorials.
- [ ] Active voice in instructional content.
- [ ] Contractions used sparingly, and expanded in reference and conceptual pages.
- [ ] Every acronym is defined on first use.
- [ ] No directional language: "above", "below", "the following section".
- [ ] Numbers zero through nine spelled out in prose. Digits for 10 and above, and always for versions, measurements, CLI flags, and table contents.

## Formatting

- [ ] Bold appears only on UI element names and on description-list terms. Nowhere else.
- [ ] Emphasis uses `_italics_` on a single word or phrase, or an admonition for something important.
- [ ] No emoji anywhere, including in callouts and comparisons. `Do:` and `Do not:` are text labels.
- [ ] At most one em dash per sentence, written as `—`, never as `--`. En dashes only for numeric ranges.
- [ ] Oxford commas throughout.
- [ ] No exclamation marks.
- [ ] Double quotes in prose, with commas and periods inside them.
- [ ] Chicago title case in titles and headings.
- [ ] Every code block has a language shortcode.
- [ ] Every code identifier in prose is backticked, on every mention, including inside tables.
- [ ] List punctuation is consistent: every item ends with a period, or none do.
- [ ] Description lists use `**Term**: Description.` and no list mixes that format with free-form bullets.
- [ ] List items share a grammatical form: all verb phrases, or all noun phrases.
- [ ] Numbered lists are used only for sequences. Bulleted lists for everything else.
- [ ] Tables are formatted and their headers and values are centered.
- [ ] Link text is descriptive and uses the target page's title. No "here", "this", "read more", or "learn more".

## Before You Submit

- [ ] Every template comment and bracketed instruction is deleted.
- [ ] The PR description says what changed and why, and links the issue or launch if one exists.
- [ ] The PR indicates your review preference using the PR template.
- [ ] **Allow edits from maintainers** is checked, so small fixes do not need a round trip.
- [ ] If the change is release-blocking, the PR description says so and names the date.

## If You Drafted With an AI Agent

Everything in the Accuracy section applies twice over, and these are the failure modes worth a second pass:

- [ ] Bold has not been sprinkled through the prose for emphasis.
- [ ] Em dashes are not doing the work of commas and periods throughout.
- [ ] Backticks have not been dropped on the second and third mention of an identifier.
- [ ] Banned filler phrases have not survived the edit.
- [ ] Lists are not a mix of punctuated and unpunctuated items.
- [ ] No confident claim about behaviour that you have not independently verified.
- [ ] No API, method, parameter, or flag that you have not confirmed exists.

Point the agent at [`AGENTS.md`](https://github.com/polkadot-developers/polkadot-docs/blob/master/AGENTS.md) in the style guide repository before drafting. It front-loads these rules.
