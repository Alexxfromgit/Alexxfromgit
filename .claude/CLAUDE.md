# Maintenance notes — Alexxfromgit/Alexxfromgit (GitHub profile README)

Internal notes for `README.md` and `assets/`, kept out of those files themselves so visitors browsing the raw source don't see maintenance commentary.

## External widget dependencies

`README.md` renders several sections via third-party badge/widget services with no local fallback. If any of these go down or get rate-limited, the affected section shows a broken image with no fallback and nothing flags it:

- Animated tagline: `readme-typing-svg.demolab.com`
- Profile badges row (profile views, followers, stars, repo-count): `komarev.com`, `img.shields.io`
- "GitHub in Numbers": `github-profile-summary-cards.vercel.app`, `streak-stats.demolab.com`, `github-profile-trophy.vercel.app`, `github-readme-activity-graph.vercel.app`
- "Thought of the Day": `quotes-github-readme.vercel.app`
- Footer banner: `capsule-render.vercel.app`

No self-hosted replacement or refresh workflow exists for any of these.

**Known outage (as of 2026-08-29):** `github-profile-trophy.vercel.app` and `github-readme-activity-graph.vercel.app` both return `HTTP 402 Payment Required` / `DEPLOYMENT_DISABLED` — the maintainers' Vercel deployments have been disabled (likely a free-tier usage quota issue), independent of this repo or GitHub account. `streak-stats.demolab.com` tested fine directly; if it also shows broken in the rendered profile, it's more likely a transient GitHub image-proxy (camo) cache issue than the service being down.

Investigated self-hosting these two as a fix: no official self-host GitHub Action exists from either maintainer. The only trophy self-host Action found is on an **unmerged branch of an unofficial third-party fork** (`Erik-Donath/github-profile-trophy@feature/generate-svg`) — using it means trusting unreviewed code in CI, so it was not wired in. For the activity graph, self-hosting would require deploying the maintainer's server to your own infra (Vercel/Heroku), or writing a custom GraphQL-based chart generator from scratch — also not done.

**Decision:** leave both pointed at the live (currently down) hosted URLs and wait for the upstream outage to resolve, rather than take on the fork-trust risk or build custom replacement tooling. Revisit if the outage persists long-term.

## Achievements table

The Achievements table (`<h2 id="achievements">`) is hand-typed HTML, not a live badge — GitHub has no public API for profile achievements. Update it manually as new achievements are earned; nothing will flag it as stale.

## Hero banner CJK glyph risk

`assets/hero-banner.svg` renders its main title as CJK text (亚历山大大帝) with a font stack of CJK-capable fonts ending in the generic `serif` fallback. On a viewer with none of the listed fonts installed, the glyphs can render as blank boxes — the generic fallback only guarantees *some* font is picked, not CJK glyph coverage. A full fix would require embedding or outlining a CJK font into the SVG.
