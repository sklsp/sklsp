# Jay de Lauw (sklsp)

Rotterdam. Part-time IT student at Avans (2026-2030), working at KPN, aiming for an AI Engineer role. I build AI products that ship, with evals to prove they work and tests to keep them honest.

**Portfolio: [studiobijblijver.com](https://studiobijblijver.com)**, my web design studio and products, built as one scroll-driven 3D flight (three.js, no framework).

## Building now

**[Iris](https://github.com/sklsp/iris)** (public, MIT): a local voice agent for Windows that builds the skills it is missing. It listens for a wake word, answers in one natural voice for Dutch and English that starts about 0.3 s after the answer is ready, reads the screen through Windows UI Automation and web pages in your own browser through the DevTools Protocol (and looks at a screenshot with a vision model when an app exposes nothing), and asks before it changes anything. When no tool can do what you ask, a coding agent writes a new skill with tests, and Iris only runs it after you approve exactly that code. The hard part solved: the risk tiers live in code, not in the prompt, so a clever prompt or a planted instruction on a web page cannot talk it into paying, sending or deleting. An eval of over 200 tasks against the real model, safety traps included: 98.0% pass, 0 forbidden actions. Fully local: no cloud, no cost per command.

**[Sparton](https://github.com/sklsp/Sparton)** (public): competitor intelligence for small e-commerce sellers: add your shop URL and it discovers who you actually compete against, crawls them on a schedule, diffs catalogs week over week and writes a plain-English report with evidence links. The hard part solved: the numbers are computed by a diff engine and the AI only writes the summary. It never invents a price.

**leadscan** (private): finds local businesses that need a better website, and runs the sales side of my web studio. It pulls businesses from OpenStreetMap, finds their website through the Google Places API (matched on name and distance, so a namesake across town is not a hit), tests every site (https, mobile, speed, copyright year, CMS version) and has a local vision model in LM Studio rate the design from desktop and phone screenshots as structured JSON. The hard part solved: every score explains itself. Each point comes from one weights table, the dashboard shows the three heaviest factors, and every model verdict is labelled "AI impression" next to the screenshot it judged, so a person can check it. A FastAPI dashboard runs the whole flow: scans with a cost estimate up front and live progress, a CRM pipeline, quotes, and invoices with an unbroken numbering and credit invoices instead of edits, plus an offline demo mode on a copy of real scans. 516 tests; Google calls stop at a monthly budget under the free tier.

**Vistora** (private): AI property walkthrough films from listing photos, 16:9 plus a vertical cut. The hard part solved: video models invent things, so every clip is anchored to a real photo every 4-8 s and structurally QA'd before a human sees it.

## Under the hood

- **fidelity** (private): a CPU-only OpenCV + NumPy check that flags structural changes AI models make to property photos; ~0.4 s per photo, eval on 400 pairs: 3% false alarms on benign edits, 96% of tampers detected.
- **shopfeed** (private): exact webshop catalogs from Shopify/WooCommerce/Lightspeed public JSON feeds with a schema.org JSON-LD fallback; no LLM calls and a fraction of the requests of HTML scraping. The fetcher is SSRF-safe: public addresses only, re-checked on every redirect hop including DNS rebinding.
- **vistora-render** (private): the walkthrough engine behind Vistora: an append-only cost ledger with a hard cap per order, failed clips re-rendered within budget, and one price table for all models ($0.10-$0.90/s; a 36 s film is $3.60-$32.40 before re-renders).

## How I work

- **Evals before claims.** fidelity ships with an eval of 400 pairs (benign edits plus four tamper types at three sizes); one padding fix cut false alarms from 25% to 4%. Iris publishes its eval in the README: over 200 tasks, three runs each, with traps for paying, sending and planted instructions.
- **Profile before optimizing.** Iris's voice made speech at 0.58 times real time on an RTX 3060. Timing each part of a step showed 72% going to attention over a cache of 8192 positions that held a few hundred; sizing it to fit made speech 3.4 times faster, and every answer now starts in 0.3 s.
- **Model output stays checkable.** leadscan never shows a vision-model verdict on its own: it is labelled as an AI impression and sits next to the screenshot it judged.
- **Tests that exercise the real thing.** Sparton: 549 tests pass in CI, including 33 driving a real browser through signup, the product loop and tenant isolation.
- **Cost and security are first-class constraints.** Hard budget caps with an append-only ledger; crawlers can't be pointed inward. Public addresses only on every redirect hop, DNS rebinding caught, bodies streamed and capped at 20 MB.

## Stack

Python · FastAPI · Jinja2 · PostgreSQL · Redis · Docker · Playwright · OpenCV + NumPy · ffmpeg · Stripe · LLM APIs (OpenRouter) · local vision models (LM Studio) · Veo 3.1 / Seedance 2.5

## Contact

- LinkedIn: https://www.linkedin.com/in/jay-de-lauw-653915231/
- Email: jaydelauw@gmail.com
