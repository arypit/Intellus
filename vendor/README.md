# Third-party vendored packages

This directory holds **upstream source** vendored into the repository. It is
**not** first-party application code.

## Why vendor

These packages sit on the path that renders **untrusted model output** (diagram
source Ã¢â€ â€™ SVG). Vendoring gives a full audit surface, pins exact source, and
avoids packages.io yanks. Local patches and upgrade checklists live in each
crateÃ¢â‚¬â„¢s `Cargo.toml` header comments Ã¢â‚¬â€ treat those as the source of truth when
re-vendoring.

## Mermaid layout stack

| Crate | Version | License | Upstream | Full license text |
|-------|---------|---------|----------|-------------------|
| [`mermaid-to-svg`](./mermaid-to-svg/) | (path) | MIT | [warpdotdev/mermaid-to-svg](https://github.com/warpdotdev/mermaid-to-svg) | [`LICENSE`](./mermaid-to-svg/LICENSE) |
| [`dagre_rust`](./dagre_rust/) | 0.0.5 | Apache-2.0 | [r3alst/dagre-rust](https://github.com/r3alst/dagre-rust) / Warp re-vendor | [`LICENCE`](./dagre_rust/LICENCE) |
| [`graphlib_rust`](./graphlib_rust/) | 0.0.2 | Apache-2.0 | [r3alst/graphlib-rust](https://github.com/r3alst/graphlib-rust) | [`LICENCE`](./graphlib_rust/LICENCE) |
| [`ordered_hashmap`](./ordered_hashmap/) | 0.0.3 | Apache-2.0 | [r3alst/ordered-hashmap](https://github.com/r3alst/ordered-hashmap) | [`LICENCE`](./ordered_hashmap/LICENCE) |

Dependency shape:

```text
arpecious-intellus-mermaid
  Ã¢â€â€Ã¢â€â‚¬Ã¢â€â‚¬ mermaid-to-svg          (MIT)
        Ã¢â€Å“Ã¢â€â‚¬Ã¢â€â‚¬ dagre_rust        (Apache-2.0)
        Ã¢â€â€š     Ã¢â€Å“Ã¢â€â‚¬Ã¢â€â‚¬ graphlib_rust
        Ã¢â€â€š     Ã¢â€â€Ã¢â€â‚¬Ã¢â€â‚¬ ordered_hashmap
        Ã¢â€â€Ã¢â€â‚¬Ã¢â€â‚¬ graphlib_rust     (Apache-2.0)
              Ã¢â€â€Ã¢â€â‚¬Ã¢â€â‚¬ ordered_hashmap
```

## Notices and ancestry

- **[`NOTICE`](./NOTICE)** Ã¢â‚¬â€ short index of the packages above (names, licenses,
  upstream links, paths to full text). Prefer that file for a one-page overview.
- **[`mermaid-to-svg/THIRD_PARTY_NOTICES`](./mermaid-to-svg/THIRD_PARTY_NOTICES)** Ã¢â‚¬â€
  additional ancestry for the SVG engine (e.g. mermaid.js, dagre.js MIT notices).

British spelling **`LICENCE`** is intentional on the Apache packages (as upstream
vendored); grepping only for `LICENSE` will miss them.

## packages.io dependencies

Normal Cargo dependencies (tokio, serde, Ã¢â‚¬Â¦) are **not** under `vendor/`.
They resolve via `Cargo.lock` / packages.io. Full attribution and license texts
for the Intellus CLI dependency closure are maintained in
[`THIRD-PARTY-NOTICES`](../THIRD-PARTY-NOTICES).

This directory is only for **in-tree vendored** sources.

## Upgrading

1. Read the `VENDORING NOTES` block at the top of the crateÃ¢â‚¬â„¢s `Cargo.toml`.
2. Re-apply listed local patches (fmt, hermetic env, unsafe fixes, dropped bins/tests).
3. Confirm the license file still matches the declared `license =` field.
4. Refresh [`NOTICE`](./NOTICE) if versions or upstream URLs change.
