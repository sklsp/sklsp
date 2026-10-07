# Jay de Lauw (sklsp)

Rotterdam. Part-time IT student at Avans (2026-2030), working at KPN, aiming for an AI Engineer role. I build AI products that ship, with evals to prove they work and tests to keep them honest.

**Portfolio: [delauw.vercel.app](https://delauw.vercel.app)**, my web design studio and products, built as one scroll-driven 3D flight (three.js, no framework).

## Building now

**[Sparton](https://github.com/sklsp/Sparton)** (public): competitor intelligence for small e-commerce sellers: add your shop URL and it discovers who you actually compete against, crawls them on a schedule, diffs catalogs week over week and writes a plain-English report with evidence links. The hard part solved: the numbers are computed by a diff engine and the AI only writes the summary. It never invents a price.

**Iris** (private): a voice agent that runs my machine. It listens for a wake word, reads the screen through Windows UI Automation and asks before it changes anything. The hard part solved: the risk tiers live in code, not in the prompt, so a clever prompt cannot talk it into a destructive action. Fully local: no cloud, no cost per command.

**Vistora** (private): AI property walkthrough films from listing photos, 16:9 plus a vertical cut. The hard part solved: video models invent things, so every clip is anchored to a real photo every 4-8 s and structurally QA'd before a human sees it.

## Under the hood

- **fidelity** (private): a CPU-only OpenCV + NumPy check that flags structural changes AI models make to property photos; ~0.4 s per photo, eval on 400 pairs: 3% false alarms on benign edits, 96% of tampers detected.
- **shopfeed** (private): exact webshop catalogs from Shopify/WooCommerce/Lightspeed public JSON feeds with a schema.org JSON-LD fallback; no LLM calls and a fraction of the requests of HTML scraping. The fetcher is SSRF-safe: public addresses only, re-checked on every redirect hop including DNS rebinding.
- **vistora-render** (private): the walkthrough engine behind Vistora: an append-only cost ledger with a hard cap per order, failed clips re-rendered within budget, and one price table for all models ($0.10-$0.90/s; a 36 s film is $3.60-$32.40 before re-renders).

## How I work

- **Evals before claims.** fidelity ships with an eval of 400 pairs (benign edits plus four tamper types at three sizes); one padding fix cut false alarms from 25% to 4%.
- **Tests that exercise the real thing.** Sparton: 581 tests pass, including 29 driving a real browser through signup, the product loop and tenant isolation.
- **Cost and security are first-class constraints.** Hard budget caps with an append-only ledger; crawlers can't be pointed inward. Public addresses only on every redirect hop, DNS rebinding caught, bodies streamed and capped at 20 MB.

## Stack

Python · FastAPI · PostgreSQL · Redis · Docker · Playwright · OpenCV + NumPy · ffmpeg · Stripe · LLM APIs (OpenRouter) · Veo 3.1 / Seedance 2.5

## Contact

- LinkedIn: https://www.linkedin.com/in/jay-de-lauw-653915231/
- Email: jaydelauw@gmail.com
