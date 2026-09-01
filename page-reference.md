<!--
REFERENCE PAGE TEMPLATE

Use this when the reader already knows what they want and needs an exact value:
a method signature, a parameter name, an extrinsic, an error code, a CLI flag, a
configuration key.

Reference pages are consulted, not read. Optimize for scanning: tables over
prose, consistent ordering, exhaustive coverage. A reference page that omits
three of twelve parameters is worse than no reference page, because the reader
cannot tell that it is incomplete.

Where the source of truth is generated (rustdoc, an OpenAPI spec, a type
definition), link to it rather than transcribing it. Hand-copied signatures
drift within one release.

Delete this comment block and every other comment in the file before opening
the PR.

Save to:   docs/<section>/<subsection>/<page-name>.md
Snippets:  docs/.snippets/code/<section>/<subsection>/<page-name>/
-->
---
title: <!-- 60 characters or fewer. Name the thing: "Bundle Pallet Reference". -->
description: <!-- 120 to 160 characters. -->
categories: <!-- Comma-separated. Only values from categories_info in llms_config.json. -->
---

# <!-- H1. Noun phrase naming the interface. -->

## Introduction

<!--
Short. One or two paragraphs at most, and the style guide permits omitting the
introduction entirely on some reference pages.

Cover only: what this interface is for, which version or runtime it applies to,
and where the authoritative source lives. Link to the concept page for anyone
who arrived without context.
-->

## <!-- Grouping heading, e.g. "Extrinsics", "Methods", "Configuration Keys", "CLI Flags". -->

<!--
One subsection per item, in a consistent order. Alphabetical is defensible;
so is grouping by task. Pick one and hold to it for the whole page.
-->

### `INSERT_ITEM_NAME`

<!--
Signature first, in a code block with a language shortcode:

```rust
fn INSERT_ITEM_NAME(origin: OriginFor<T>, INSERT_PARAM: INSERT_TYPE) -> DispatchResult
```

Then one or two sentences on what it does. Then the parameters as a table.

Backtick every identifier on every mention, including in table cells. Use the
exact casing from the source code and keep it identical everywhere on the page.

|      Parameter      |    Type    | Required |                Description                |
|:-------------------:|:----------:|:--------:|:-----------------------------------------:|
| `INSERT_PARAM_NAME` | `InsertTy` |   Yes    |                                           |

Follow with what it returns, what it emits, and what it costs where relevant:

- **Returns**: Description of the return value.
- **Events**: The events emitted on success.
- **Errors**: The failure conditions, linking to the errors section.
- **Weight or fee**: Cost characteristics, if the reader needs them to plan.

An example is worth including when the parameter shapes are non-obvious:

```js
--8<-- 'code/<section>/<subsection>/<page-name>/INSERT_ITEM_NAME.js'
```
-->

### `INSERT_SECOND_ITEM_NAME`

<!-- Same structure. Do not vary the shape between entries on one page. -->

## Errors

<!--
Every error the interface can return, with the literal string the reader will
see. This is what gets pasted into a search engine, so exact text matters more
than elegant phrasing.

|         Error         |             Cause             |            Resolution           |
|:---------------------:|:-----------------------------:|:-------------------------------:|
| `InsertErrorVariant`  |                               |                                 |
-->

## Limits and Defaults

<!--
Hard numbers: maximum sizes, timeouts, retry counts, default values, expiry
periods. Readers hunt for these and rarely find them, so give them a predictable
home.

|       Parameter       |  Default  |  Maximum  |               Notes               |
|:---------------------:|:---------:|:---------:|:---------------------------------:|
|                       |           |           |                                   |

If a value differs per network or per runtime version, say which is which
instead of documenting only one.
-->

## Where to Go Next

<!--
Link to the concept page, the guide that uses this interface, and the
authoritative generated source if one exists.
-->
