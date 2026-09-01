# Documentation Templates

Starting points for contributing to [`polkadot-docs`](https://github.com/polkadot-developers/polkadot-docs). Copy the template you need into the right directory, rename it to kebab-case, and fill it in.

These templates encode the rules from [`CONTRIBUTING.md`](https://github.com/polkadot-developers/polkadot-docs/blob/master/CONTRIBUTING.md) and the [documentation style guide](https://github.com/papermoonio/documentation-style-guide) so you do not have to read both before writing a page. They are not a substitute for either, but starting from one will get you through review much faster.

## Which Template Do I Need

| You want to                                              | Use                                                                | Ask first?              |
| -------------------------------------------------------- | ------------------------------------------------------------------ | ----------------------- |
| Explain what something is, why it exists, how it works   | [`page-concept.md`](page-concept.md)                               | No, if placement is obvious |
| Show how to accomplish one specific task                  | [`page-how-to-guide.md`](page-how-to-guide.md)                     | No, if placement is obvious |
| Walk a reader end to end through building something       | [`page-tutorial.md`](page-tutorial.md)                             | Recommended             |
| Document parameters, methods, extrinsics, errors, or CLI  | [`page-reference.md`](page-reference.md)                           | No                      |
| Create a whole new section of the docs                    | [`section-index.md`](section-index.md)                             | Yes                     |
| Plan documentation for a new product or a launch          | [`documentation-plan.md`](documentation-plan.md)                   | Yes, 4 to 6 weeks ahead |
| Check your work before requesting review                  | [`pr-self-review-checklist.md`](pr-self-review-checklist.md)       | n/a                     |

"Ask first" means send a short message in [#docs-channel] before you write, so placement gets settled while it is still cheap to change. Misplaced content is the most expensive thing to fix after the fact.

If you are unsure whether a page is a concept, a guide, or a tutorial, the distinction is what the reader is doing while reading it:

- **Concept**: The reader is trying to understand something before deciding to use it.
- **How-to guide**: The reader has a specific task and wants the shortest correct path through it.
- **Tutorial**: The reader is learning by building, and follows every step in order.
- **Reference**: The reader knows what they want and needs an exact value, signature, or name.

Mixing two of these on one page is the most common structural problem in review. A guide that stops to explain architecture for four paragraphs should link to a concept page instead.

## How to Use a Template

1. Copy the file into the appropriate directory under `docs/`:

    ```bash
    cp docs-templates/page-how-to-guide.md docs/<section>/<subsection>/<page-name>.md
    ```

2. Rename it in kebab-case, lowercase, no spaces or special characters. The file name should describe the content: `submit-a-transaction.md`, not `guide2.md`.

3. Fill in the frontmatter. All three required fields must be present or the build is incomplete:

    - `title`: 60 characters or fewer.
    - `description`: 120 to 160 characters.
    - `categories`: Comma-separated, using only values defined in `categories_info` in `llms_config.json` at the repository root.

4. Delete every HTML comment (`<!-- ... -->`) and every bracketed instruction as you go. Leftover template scaffolding in a PR is the fastest way to get a review round trip.

5. Add the page to `.nav.yml` in the same directory:

    ```yaml
    - 'Your Page Display Name': 'your-file-name.md'
    ```

6. Build locally and read your page in the browser. Instructions are in the [README](https://github.com/polkadot-developers/polkadot-docs/blob/master/README.md#run-polkadot-docs-locally). Broken snippet paths and image paths do not surface any other way.

7. Work through [`pr-self-review-checklist.md`](pr-self-review-checklist.md), then open the PR and request review from `@bucanero`.

## Conventions That Apply to Every Page

**Assets mirror the docs structure.** A page at `docs/<section>/<subsection>/<page-name>.md` keeps its assets at:

```text
docs/images/<section>/<subsection>/<page-name>/
docs/.snippets/code/<section>/<subsection>/<page-name>/
```

**Images** are `.webp`, named `<page-name>-01.webp` with a zero-padded sequence reflecting order on the page. Desktop screenshots are 1512px wide; browser extension screenshots are 400x600px.

**Code lives in snippets, not inline**, whenever it is more than a couple of lines or is reused. Store it under `docs/.snippets/code/` and transclude it:

```text
--8<-- 'code/<subdirectory>/<snippet-file-name>.js'
```

This keeps code testable and lets one fix propagate to every page that uses it.

**Every code block gets a language shortcode** so syntax highlighting works: ` ```js `, ` ```rust `, ` ```bash `, ` ```json `.

**Placeholders for values the reader must supply** use the `INSERT_` convention in uppercase snake_case, and describe the value:

```js
const contractAddress = 'INSERT_CONTRACT_ADDRESS';
```

Not `INSERT_CONTRACT_ADDRESS_HERE`, not `INSERT-CONTRACT-ADDRESS`, not `YOUR_ADDRESS`.

**Terminal output** uses a termynal block, showing the command, the output, and a blank prompt at the end if the command returns control to the shell:

```html
<div class="termynal" data-termynal>
    <span data-ty="input"><span class="file-path"></span>INSERT_COMMAND</span>
    <span data-ty>INSERT_OUTPUT</span>
    <span data-ty="input"><span class="file-path"></span></span>
</div>
```

**Callouts** are `!!! note`, `!!! tip`, and `!!! warning`. Content is indented four spaces under the marker. Use a callout instead of bolding a sentence to make it stand out.

## The Style Rules Most Often Missed

Full detail is in the [style guide](https://github.com/papermoonio/documentation-style-guide). These are the ones that generate the most review comments:

- **Bold is only for UI element names and description-list terms.** Not for emphasis. Use `_italics_` for a single word, or a callout for something genuinely important.
- **No emoji anywhere.** Use the text labels `Do:` and `Do not:` for comparisons.
- **No first person.** Address the reader as "you". Avoid "we", "our", and "let's" outside informal tutorials.
- **Write timeless docs.** No "currently", no "at the time of writing", no "recently".
- **No filler or marketing language.** The banned list includes: delve into, leverage, utilize, seamless, robust, powerful, simply, just, easily, obviously, it's important to note that, in conclusion, feel free to, under the hood, etc.
- **Never describe a step as easy.** Delete "simply" and "just" from instructions.
- **Backtick every code identifier, every time it appears.** Function names, types, variables, file paths. Dropping backticks on the second mention is a consistent review flag.
- **One em dash per sentence at most,** and use the real `—` character, not `--`.
- **List punctuation is all-or-nothing.** Either every item ends with a period or none do. Never mix.
- **Task headings are imperative:** "Create an Instance", not "Creating an Instance". Concept headings are noun phrases: "Blockchain Consensus Mechanisms", not "Understanding Consensus".
- **Descriptive link text.** Use the target page's title. Never "here", "this", "read more", or "learn more".

If a rule here conflicts with the style guide, the style guide wins. If neither covers your case, default to the [Google developer documentation style guide](https://developers.google.com/style).

## Authoring With an AI Agent

If you draft with an LLM, point it at the style guide's [`AGENTS.md`](https://github.com/polkadot-developers/polkadot-docs/blob/master/AGENTS.md) first. It front-loads the rules that generated output violates most often: bold misuse, em dash over-use, banned phrases, list punctuation, and dropped backticks.

An AI draft still needs a human who knows the product to verify every claim, every identifier, and every code example before the PR is opened. Review catches style problems. It does not catch a plausible-sounding claim about behaviour that does not exist.
