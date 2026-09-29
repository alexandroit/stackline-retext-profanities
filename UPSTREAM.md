# Upstream and maintenance review

This package maintains `retext-profanities@7.2.2` under the independent `@stackline/retext-profanities` name.

- Source: https://github.com/retextjs/retext-profanities/tree/2003b36350743421e79ae8fc52fbbb4b483d71ac
- Public npm artifact integrity: `sha512-nwrR987v3m7+JQ8wyK8oE+adqS1aYUyHyf+k6omflI/8PL9Slbp/39YieTJJvrmR0udBe2iV7aURXW5/3Uj12w==`.
- Upstream issue evidence checked: 2026-09-29T00:22:07.622565+00:00.
- Original license and author notices are retained.
- The upstream published runtime files and declarations are hash-checked in `.stackline/upstream.json`. Any runtime fix is explicitly listed there.
- Functional upstream suites run against the source and extracted final package. Development tools were reduced to those used by validation; full source and runtime audits must pass.
- Only direct dependencies of the original Stackline portfolio are in this migration. This is not a claim that all transitive projects are maintained by Stackline.

## Issue triage

The queried open-issue list contained no issue entries. This does not establish that the upstream is abandoned or bug-free. No runtime bug fix is claimed for this initial maintenance release.

The evidence query fetched the latest 100 open and 30 closed issue/PR entries and removed PRs. Closed entries were collected for context; this report does not claim an exhaustive historic review.

## Release discipline

The source commit, passing CI and CodeQL, reviewed CI tarball hash, npm provenance, normal and aliased installs, and immutable GitHub release are checked before a release is complete. Published versions and tags are never replaced.
