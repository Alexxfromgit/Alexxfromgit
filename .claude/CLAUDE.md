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

## Achievements table

The Achievements table (`<h2 id="achievements">`) is hand-typed HTML, not a live badge — GitHub has no public API for profile achievements. Update it manually as new achievements are earned; nothing will flag it as stale.

## Hero banner CJK glyph risk

`assets/hero-banner.svg` renders its main title as CJK text (亚历山大大帝) with a font stack of CJK-capable fonts ending in the generic `serif` fallback. On a viewer with none of the listed fonts installed, the glyphs can render as blank boxes — the generic fallback only guarantees *some* font is picked, not CJK glyph coverage. A full fix would require embedding or outlining a CJK font into the SVG.
