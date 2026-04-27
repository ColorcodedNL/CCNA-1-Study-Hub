# CCNA 1 Study Hub

Independent study tools for the Cisco NetAcad Introduction to Networks v7.0 (ITNv7 / CCNA 1) curriculum. Everything runs in the browser, no server, no build step, no dependencies.

## What's inside

| File | Tool | What it does |
|------|------|--------------|
| `index.html` | Hub | Landing page with tool overview, progress stats, and resources |
| `quiz.html` | Final Exam Quiz | 143-question pool, randomized 60 per round, study/exam/retry modes, 1:15:00 timer |
| `trainer.html` | Packet Tracer Trainer | IOS CLI scenarios, VLSM addressing tables, and a full PTSA exam simulator |

The three HTML files share a consistent NetAcad-green design and a common `localStorage` key (`ccna1_hub_stats`) so the hub can show your progress across tools.

## Running it

**Locally:** open `index.html` in any modern browser.

**GitHub Pages:** push the repo, enable Pages on the `main` branch at `/ (root)`, and the hub is live at `https://<username>.github.io/<repo>/`.

## Features

### Quiz (`quiz.html`)

- Pool of 143 unique questions combining Practice Final + Final Exam content
- Each round randomly picks 60 questions with shuffled answer options
- Three modes:
  - **Study** — instant feedback with explanation after each answer
  - **Exam** — 1:15:00 timer, no feedback until the end, 70% pass threshold (42/60)
  - **Retry wrongs** — only the questions you got wrong previously
- Questions stay in English (to match the real exam), UI toggles NL/EN
- Flag questions for review, navigate with the chip bar, pause the timer

### Trainer (`trainer.html`)

- **CLI tab** — scenario-based IOS command practice with a working terminal emulator. Real IOS-style tab completion (only completes keywords, never parameter values), prefix matching across multiple tokens, and a `^` marker on syntax errors that mirrors the real router's output.
- **Adrestabel tab** — fill-in VLSM addressing tables with inline validation.
- **Examen tab** — full PTSA simulation with randomized variants across three phases:
  1. Address table (IPv4 + IPv6 + link-local)
  2. Router CLI configuration with credentials, SSH, and dual-stack interfaces
  3. Switch CLI configuration with management VLAN

  Each phase shows the relevant credentials and a compact address mini-table in the sidebar so you don't have to switch tabs while typing CLI commands.

### Hub (`index.html`)

- Summary of your last quiz score, quizzes completed, CLI scenarios done, and pending wrongs
- Links to both tools and external resources (NetAcad, Packet Tracer)
- Option to clear all local data

## Design notes

- **System fonts only.** No Google Fonts, no external CSS, no CDN dependencies. Pages render the same offline as online.
- **Single-file deliverables.** Each HTML file is self-contained: HTML + CSS + JS + base64-encoded Cisco device icons. No build step or bundler.
- **Compact icon storage.** Icons are stored once and referenced via placeholders that are expanded at render time, keeping `trainer.html` around 230 KB instead of bloating it with duplicated base64 strings.

## Privacy

No cookies, no analytics, no tracking, no third-party requests. The entire hub runs client-side with system fonts only, nothing is loaded from external CDNs or font services. Progress data and language preference are stored exclusively in the browser's `localStorage` under three keys:

- `ccna1_hub_stats` — session stats (scores, counters, timestamps)
- `ccna1_wrongs` — questions you got wrong, for the retry mode
- `ccna1_lang` — your chosen UI language

No data leaves the device. The "Reset all local data" link on the hub clears everything.

## Disclaimer

This is an independent study project created by a student for personal practice. Cisco, Networking Academy, NetAcad, CCNA, Packet Tracer, and IOS are trademarks of Cisco Systems, Inc. All course materials and trademarks remain the property of their respective owners. Question content is based on publicly available exam material and used for educational purposes only.

For the official curriculum, certification, and up-to-date material: [netacad.com](https://netacad.com).

## License

Code in this repository is released under the MIT License. Cisco-owned content (trademarks, curriculum references) is not covered by this license and remains the property of Cisco Systems, Inc.
