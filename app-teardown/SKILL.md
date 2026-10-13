---
name: app-teardown
description: Use when the user wants a teardown of their app project — screenshot every screen, lay each flow out on a /design canvas, and critique it for UX, conversion, retention and product.
---

# App teardown

Run a product teardown of the app in this repo: capture every screen as it actually renders, critique each screen and flow the way a senior product designer tears down a competitor, then lay each flow out on a /design canvas with the critique beside the screens. The screenshots are the evidence — every finding points at something visible in one.

This skill never edits app code. It reads, runs, captures and reports. All output goes in `docs/teardown/`.

## 1. Understand the product

Read the README, anything in `docs/` (PRD.md, DEFINE.md, DESIGN.md if present), the package manifest, and the pricing or paywall code. Pin down who it's for, the job it does for them, and how it makes money. If any of the three can't be found, ask the user once before going on — critique without the job is decoration.

Done when: `docs/teardown/product.md` states audience, job and business model, each sourced to a file or to the user.

## 2. Map every screen

Inventory screens from the code, not by clicking around: routes (Next.js app/pages, React Router, Remix, SvelteKit), screens and navigators (Expo Router, React Navigation), SwiftUI/UIKit views, plus modals, sheets, dialogs and paywalls. Group them into **flows** — the sequence a user walks to get one thing done (first-run onboarding, sign-up/sign-in, the core loop, create/edit, upgrade, settings/account, cancel). A screen can sit in more than one flow.

For each screen, list the states worth capturing: empty, populated, loading, error, first-run vs returning, free vs paid.

Done when: `docs/teardown/screen-map.md` lists every flow with its screens in order and their states, and every route or screen file in the code is either in a flow or under "Not captured" with a reason.

## 3. Capture

Run the app locally and screenshot every screen and state in the map.

- **Web** — start the dev server and drive it with Playwright (install it if missing). Capture at 390×844 and 1440×900 unless the app is clearly mobile-only or desktop-only; full-page for screens that scroll.
- **iOS / Expo native** — boot the simulator, navigate by deep link where possible, capture with `xcrun simctl io booted screenshot`. Screens you can't drive to go on the "Not captured" list for the user to grab by hand.
- **Auth and data** — use test accounts and data from the project's seed or fixture files, or create a throwaway account on localhost. Never real credentials, never production services. Seed enough data that populated states look like real use.

Save as `docs/teardown/screens/<flow>/<NN>-<screen>-<state>.png`, compressed to ≤300 KB each so canvases stay light.

Done when: every screen and state in `screen-map.md` has a file or a logged reason it doesn't, and you've opened a sample from every flow to confirm it rendered — no blank page, error overlay, or dev toolbar.

## 4. Critique

Look at every screenshot. Review each screen, then each flow end to end, then the product as a whole, through all four lenses (see **Lenses** below).

Each finding records:

- **Where** — flow › screen › element
- **Lens** — UX, Conversion, Retention or Product
- **Problem** — what the user experiences, not what the code does
- **Recommendation** — the specific change, buildable as written
- **Severity** — Critical (blocks the job or revenue) / Major / Minor / Polish
- **Effort** — S / M / L

Rules:

- **Point at pixels.** Every finding cites something visible in a screenshot. A finding about something missing names where it should be.
- **One problem per finding.** The same problem on several screens is one pattern finding listing every location.
- **No generic best practice.** If a recommendation would apply to any app, make it about this one or cut it.
- **Name what's working** in each flow, briefly, so the fixes don't break it.

Done when: every screen has been reviewed against all four lenses (a screen with no findings says so) and every flow has a verdict: steps to value, where users will drop, what to fix first.

## 5. Lay out each flow on a canvas

Run `/design` once per flow. The brief:

- One artboard per screen, sized to its capture viewport, in flow order left to right, labelled `<NN> · <screen name>`.
- Alternate states stacked beneath their screen.
- The screenshot placed as the artboard's content, unaltered. This is a wall of evidence, not a redesign.
- Beside each screen, a note card with that screen's findings, severity-tagged, Critical first.
- A final artboard summarising the flow: verdict, what's working, top fixes.

Done when: every flow has a canvas, and each canvas link is recorded in `screen-map.md`.

## 6. Report

Write `docs/teardown/REPORT.md`:

1. **Verdict** — three sentences on the product's biggest opportunity.
2. **Top 10** — findings ranked by impact on the job and the business, against effort.
3. **Per flow** — canvas link, verdict, findings table.
4. **Product recommendations** — positioning, magic moment, retention loop, monetisation.
5. **Not captured** — screens you couldn't reach and why.

Done when: REPORT.md has every section, and your reply to the user gives the verdict, the top 3 fixes, and the canvas links.

## Lenses

**UX** — Can the user tell where they are, what to do next, and what just happened? Hierarchy, copy clarity, feedback, empty/error/loading states, friction (taps, fields, decisions), consistency, accessibility basics (contrast, tap targets, text size).

**Conversion** — How fast does a new user reach value, and is anything asked of them before they get it? Time-to-value, sign-up wall placement, paywall timing and framing, plan clarity, CTA strength, trust signals, form friction.

**Retention** — Why would they come back tomorrow? The trigger to return, data or progress that accumulates, the core loop's payoff, notification and email hooks, what a returning user sees first, empty states that lead into the loop instead of dead-ending.

**Product** — Is this the right product for the job? Positioning visible in the product itself, the magic moment reachable in the first session, features earning their place or diluting the core, differentiation from the obvious alternative, the business model fitting how the product is actually used.
