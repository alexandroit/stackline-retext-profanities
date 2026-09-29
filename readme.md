# @stackline/retext-profanities

> retext plugin to check for profane and vulgar wording.

[![npm version](https://img.shields.io/npm/v/@stackline/retext-profanities.svg?style=flat-square)](https://www.npmjs.com/package/@stackline/retext-profanities)
[![license](https://img.shields.io/npm/l/@stackline/retext-profanities.svg?style=flat-square)](https://github.com/alexandroit/stackline-retext-profanities)
[![GitHub repository](https://img.shields.io/badge/GitHub-alexandroit%2Fstackline-retext-profanities-181717?style=flat-square&logo=github)](https://github.com/alexandroit/stackline-retext-profanities)
[![Docs](https://img.shields.io/badge/docs-alexandro.net-0f766e?style=flat-square)](https://alexandro.net/docs/vanilla/retext-profanities/)
[![Reddit community](https://img.shields.io/badge/community-r%2FStackline-ff4500?style=flat-square&logo=reddit&logoColor=white)](https://www.reddit.com/r/Stackline/)

**[Documentation](https://alexandro.net/docs/vanilla/retext-profanities/)** | **[npm](https://www.npmjs.com/package/@stackline/retext-profanities)** | **[Issues](https://github.com/alexandroit/stackline-retext-profanities/issues)** | **[Repository](https://github.com/alexandroit/stackline-retext-profanities)**

**Current package version:** `1.0.1`

---

## Why this package?

`@stackline/retext-profanities` is the Stackline-maintained distribution of `retext-profanities@7.2.2`. It is an independent continuation of [retext-profanities](https://github.com/retextjs/retext-profanities); original authors and licenses remain credited below.

## Compatibility

| Item | Value |
| :--- | :--- |
| Package | `@stackline/retext-profanities@1.0.1` |
| API target | `retext-profanities@7.2.2` |
| Supported Node.js | `See supported framework requirements` |
| License | `MIT` |
| Module type | `module` |
| Main entry | `index.js` |
| Types | `index.d.ts` |
| Runtime dependencies | `cuss, unified, pluralize, quotation, @types/nlcst, nlcst-search, nlcst-to-string, unist-util-position` |

## Installation

```bash
npm install @stackline/retext-profanities
```

Preserve existing imports and plugin resolution with an npm alias:

```bash
npm install retext-profanities@npm:@stackline/retext-profanities
```

## Usage and API reference

### retext-profanities


**[retext][]** plugin to check for possible profane and vulgar wording.

## Contents

*   [What is this?](#what-is-this)
*   [When should I use this?](#when-should-i-use-this)
*   [Install](#install)
*   [Use](#use)
*   [API](#api)
    *   [`unified().use(retextProfanities[, options])`](#unifieduseretextprofanities-options)
*   [Rules](#rules)
*   [Messages](#messages)
*   [Types](#types)
*   [Compatibility](#compatibility)
*   [Related](#related)
*   [Contribute](#contribute)
*   [License](#license)

## What is this?

This package is a [unified][] ([retext][]) plugin to check for possible
[profane or otherwise vulgar][profanities] wording, in certain contexts.
It uses [`cuss`][cuss] for sureness.

## When should I use this?

You can opt-into this plugin when you’re dealing with your own text and want to
check for potential mistakes.

## Install

This package is [ESM only][esm].
In Node.js (version 14.14+, 16.0+), install with [npm][]:

```sh
npm install @stackline/retext-profanities
```

In Deno with [`esm.sh`][esmsh]:

```js
import retextProfanities from 'https://esm.sh/retext-profanities@7'
```

In browsers with [`esm.sh`][esmsh]:

```html
<script type="module">
  import retextProfanities from 'https://esm.sh/retext-profanities@7?bundle'
</script>
```

## Use

Say our document `example.txt` contains:

```txt
He’s pretty set on beating your butt for sheriff.
```

…and our module `example.js` looks as follows:

```js
import {read} from 'to-vfile'
import {reporter} from 'vfile-reporter'
import {unified} from 'unified'
import retextEnglish from 'retext-english'
import retextProfanities from '@stackline/retext-profanities'
import retextStringify from 'retext-stringify'

const file = await unified()
  .use(retextEnglish)
  .use(retextProfanities)
  .use(retextStringify)
  .process(await read('example.txt'))

console.error(reporter(file))
```

…now running `node example.js` yields:

```txt
example.txt
  1:33-1:37  warning  Be careful with “butt”, it’s profane in some cases  butt  retext-profanities

⚠ 1 warning
```

## API

This package exports no identifiers.
The default export is `retextProfanities`.

### `unified().use(retextProfanities[, options])`

Check for possible profane and vulgar wording.

##### `options`

Configuration (optional).

###### `options.ignore`

Phrases *not* to warn about (`Array<string>`, default: `[]`).

###### `options.sureness`

Minimum *sureness* to warn about, see [`cuss`][cuss] (`number`, default: `0`).

## Rules

See [`rules.md`][rules] for a list of rules.

Note that Latin-script Arabic (`retext-profanities/ar-latn`), French
(`retext-profanities/fr`), Spanish (`retext-profanities/es`), Italian
(`retext-profanities/it`), and Portuguese (Brazilian) (`retext-profanities/pt`)
are also supported.

## Messages

See [`rules.md`][rules] for a list of rules and how rules work.

Each message is emitted as a [`VFileMessage`][vfile-message] on `file`, with
the following fields:

###### `message.source`

Name of this plugin (`'@stackline/retext-profanities'`).

###### `message.ruleId`

See `id` in [`rules.md`][rules].

###### `message.profanitySeverity`

[Cuss][] sureness (`number`).

###### `message.actual`

Profane phrase (`string`).

###### `message.expected`

Empty array to signal that `actual` should be removed or changed (`[]`).

## Types

This package is fully typed with [TypeScript][].
It exports the additional type `Options`.

## Compatibility

Projects maintained by the unified collective are compatible with all maintained
versions of Node.js.
As of now, that is Node.js 14.14+ and 16.0+.
Our projects sometimes work with older versions, but this is not guaranteed.
It also works in Deno and modern browsers.

## Related

*   [`retext-equality`](https://github.com/retextjs/retext-equality)
    — check possible insensitive, inconsiderate language
*   [`retext-passive`](https://github.com/retextjs/retext-passive)
    — check passive voice
*   [`retext-simplify`](https://github.com/retextjs/retext-simplify)
    — check phrases for simpler alternatives

## Contribute

See [`contributing.md`][contributing] in [`retextjs/.github`][health] for ways
to get started.
See [`support.md`][support] for ways to get help.

This project has a [code of conduct][coc].
By interacting with this repository, organization, or community you agree to
abide by its terms.

## License

[MIT][license] © [Titus Wormer][author]



[build-badge]: https://github.com/retextjs/retext-profanities/workflows/main/badge.svg

[build]: https://github.com/retextjs/retext-profanities/actions

[coverage-badge]: https://img.shields.io/codecov/c/github/retextjs/retext-profanities.svg

[coverage]: https://codecov.io/github/retextjs/retext-profanities

[downloads-badge]: https://img.shields.io/npm/dm/retext-profanities.svg

[downloads]: https://www.npmjs.com/package/retext-profanities

[size-badge]: https://img.shields.io/bundlephobia/minzip/retext-profanities.svg

[size]: https://bundlephobia.com/result?p=retext-profanities

[sponsors-badge]: https://opencollective.com/unified/sponsors/badge.svg

[backers-badge]: https://opencollective.com/unified/backers/badge.svg

[collective]: https://opencollective.com/unified

[chat-badge]: https://img.shields.io/badge/chat-discussions-success.svg

[chat]: https://github.com/retextjs/retext/discussions

[npm]: https://docs.npmjs.com/cli/install

[esm]: https://gist.github.com/sindresorhus/a39789f98801d908bbc7ff3ecc99d99c

[esmsh]: https://esm.sh

[typescript]: https://www.typescriptlang.org

[health]: https://github.com/retextjs/.github

[contributing]: https://github.com/retextjs/.github/blob/main/contributing.md

[support]: https://github.com/retextjs/.github/blob/main/support.md

[coc]: https://github.com/retextjs/.github/blob/main/code-of-conduct.md

[license]: license

[author]: https://wooorm.com

[unified]: https://github.com/unifiedjs/unified

[retext]: https://github.com/retextjs/retext

[vfile-message]: https://github.com/vfile/vfile-message

[profanities]: https://github.com/words/profanities

[cuss]: https://github.com/words/cuss

[rules]: rules.md

## Credits and original authors

- Original project: [retext-profanities](https://github.com/retextjs/retext-profanities).
- Titus Wormer.
- Sylvan Swierkosz.
- Mathieu Jolivet.
- Otacilio Saraiva Maia Neto.
- Copyright (c) 2016 Titus Wormer <tituswormer@gmail.com>.
- Stackline maintenance: [Alexandro Paixao Marques](https://www.linkedin.com/in/aleinfo/) and [Stackline contributors](https://github.com/alexandroit).

Original copyright, license notices and contributor acknowledgements remain part of this distribution. Stackline maintenance does not replace authorship of the original work.

## Community and Links

- [Stackline website](https://alexandro.net/)
- [GitHub projects](https://github.com/alexandroit)
- [npm packages](https://www.npmjs.com/~alex360qc)
- [Reddit community — r/Stackline](https://www.reddit.com/r/Stackline/)
- [Maintainer LinkedIn](https://www.linkedin.com/in/aleinfo/)

Use this repository's issue tracker for reproducible bugs and feature requests. Join r/Stackline for examples, usage questions and release discussions.
