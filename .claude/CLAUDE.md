# Maintenance notes — Alexxfromgit/Alexxfromgit (GitHub profile README)

Internal notes for `README.md` and `assets/`, kept out of those files themselves so visitors browsing the raw source don't see maintenance commentary.

## External widget dependencies

`README.md` renders several sections via third-party badge/widget services with no local fallback. If any of these go down or get rate-limited, the affected section shows a broken image with no fallback and nothing flags it:

- Animated tagline: `readme-typing-svg.demolab.com`
- Profile badges row (profile views, followers, stars, repo-count): `komarev.com`, `img.shields.io`
- "GitHub in Numbers": `github-profile-summary-cards.vercel.app`, `streak-stats.demolab.com`
- "Thought of the Day": `quotes-github-readme.vercel.app`
- Footer banner: `capsule-render.vercel.app`

No self-hosted replacement or refresh workflow exists for any of these.

The trophy (`github-profile-trophy.vercel.app`) and contribution-graph (`github-readme-activity-graph.vercel.app`) widgets, along with the hand-typed Achievements table, were removed on 2026-10-04. Both widget hosts had been returning `HTTP 402 DEPLOYMENT_DISABLED` since at least 2026-08-29, and no trustworthy self-host option existed.

## Tech Stack

The Tech Stack badges are hand-curated. They were last rebuilt on 2026-10-04 from the repos with real commit activity in the preceding 12 months: .NET/MAUI/WinUI apps, MCP servers, native iOS (SwiftUI) and Android (Compose) apps, Cloudflare Workers sites, Java/.NET test frameworks, and Rust. Many older repos show a 2026-05-09/10 `pushedAt` that is only a bulk metadata touch-up, not real work. Some tools have no shields.io logo (PowerShell, TestNG, NUnit, FlaUI, WinAppDriver, SpecFlow, REST Assured, WireMock, Allure, Multi-Agent Pipelines, COM Automation), so their badges are text-only on purpose. The About Me profile table repeats a subset of these as smaller `flat-square` badges, so update both together.

## Featured Projects showcase

The Featured Projects image grid uses local social-preview JPGs in `assets/projects/`, hand-wired to repo URLs in `README.md`. Adding a repo means committing its preview image and adding a card manually. Each group ends with a `colspan="2"` card at `width="50%"` when it has an odd number of items, so it stays centered at the same size as the others.

## Hero banner CJK glyph risk

`assets/hero-banner.svg` renders its main title as CJK text (亚历山大大帝) with a font stack of CJK-capable fonts ending in the generic `serif` fallback. On a viewer with none of the listed fonts installed, the glyphs can render as blank boxes — the generic fallback only guarantees *some* font is picked, not CJK glyph coverage. A full fix would require embedding or outlining a CJK font into the SVG.
