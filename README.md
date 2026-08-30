# LegionForge Token Optimizer

An evidence-led set of rules, measurements, and automation patterns for reducing unnecessary AI context and compute while preserving outcome quality.

> **Attribution notice:** The portable context governor and Codex skill are
> adaptations of Nate B. Jones's two videos, his cited references, and the
> additional primary and project sources listed in
> [`docs/ATTRIBUTIONS.md`](docs/ATTRIBUTIONS.md). LegionForge did not create
> these ideas independently; this repository documents, adapts, and proposes
> controls based on that source material.

Start with the [token-management policy](docs/TOKEN-MANAGEMENT-POLICY.md) and the machine-readable [policy defaults](docs/token-policy.yaml).

See the [source register](docs/ATTRIBUTIONS.md) for the two Nate B. Jones
videos, their authorship, and the other references informing this project.

## Design principle

Optimize for useful work per unit of compute, not the smallest token count. A reduction is successful only when quality, retries, review time, and repeat work do not regress.

## Provenance

The initial policy and skill are distilled from Nate B. Jones's two videos and
their cited references, with additional research sources recorded in the
[attribution and source register](docs/ATTRIBUTIONS.md). Claims are labeled as
source-backed, transferred practice, or a LegionForge project decision.

## Support and contact

LegionForge is open-source, local-first, and security-native. If this project
is useful, support can help fund maintenance and infrastructure through
[Ko-fi](https://ko-fi.com/jp_cruz) or [Patreon](https://patreon.com/cw/JPCruz).
Support does not purchase priority support, guaranteed features, a delivery
schedule, ownership, or additional license rights. See the official
[LegionForge donations page](https://legionforge.org/donations/) for current
terms.

For security disclosures, email [security@legionforge.org](mailto:security@legionforge.org)
and follow [SECURITY.md](SECURITY.md). For general contact, email
[info@legionforge.org](mailto:info@legionforge.org).

## License

This repository is available under the [Apache License 2.0](LICENSE) or the
[MIT License](LICENSE-MIT), at your option. Copyright (c) 2026 LegionForge.org.
