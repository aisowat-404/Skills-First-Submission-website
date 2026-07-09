# AI Agent Course Builder

A small "virtual employee" — three Claude Code subagents (`architect`, `qa`, and a `CLAUDE.md` driver) that run the Skills-First course-design workflow automatically, with a human approval gate. This repo contains the pitch/submission website plus the agent prompt files.

**Live site:** _add your GitHub Pages URL here once deployed (see below)_
**Demo video:** https://youtu.be/Hh-HlS4Xx-E
**Final demo doc:** https://docs.google.com/document/d/1Gbl65Dt_OJJ50i1H2GknfOnizN_IeUwdvwc9dhOunBE/edit?usp=sharing

## What's inside

```
AI-agent-course-builder/
├── index.html              # the submission website (single self-contained file)
├── CLAUDE.md                # orchestrator: runs architect ↔ qa loop, stops at human gates
├── .claude/agents/
│   ├── architect.md         # drafts each Skills-First step + self-check evidence
│   └── qa.md                # independent reviewer, audits against SKILL.md
├── output/                  # run artifacts land here (step-N-architect.md, step-N-qa.md, run-log.md)
└── skills/skills-first/
    └── SKILL.md             # ⚠️ not included yet — see "Missing piece" below
```

## ⚠️ Missing piece: `skills/skills-first/SKILL.md`

`architect.md` and `qa.md` both treat `skills/skills-first/SKILL.md` as their only source of rules — the 7-step process, the self-check tables, the forbidden patterns. That file isn't in this repo yet. The agents will not run correctly until you add it at:

```
skills/skills-first/SKILL.md
skills/skills-first/references/   (if your skill uses reference docs)
```

Drop in your original file before running the agent system. The website (`index.html`) works standalone regardless — it doesn't need `SKILL.md` to render or deploy.

## Running the agent system

1. Install [Claude Code](https://claude.com/product/claude-code) and sign in.
2. Clone this repo and open the folder.
3. Add your `skills/skills-first/SKILL.md` (see above).
4. Start Claude Code in the folder and send a trigger message, e.g.:
   ```
   Build a course on AI Literacy for non-technical marketing staff.
   ```
5. The driver (`CLAUDE.md`) runs `architect` → `qa` for Steps 1–4, retrying failed steps up to twice, then stops at a human approval gate before continuing to Steps 5–8.

## Deploying the website with GitHub Pages

This repo is already laid out for GitHub Pages to serve `index.html` straight from the repo root.

1. Create a new GitHub repository (or use an existing empty one).
2. From inside this folder, run:
   ```
   git init
   git add .
   git commit -m "Initial commit — AI Agent Course Builder"
   git branch -M main
   git remote add origin https://github.com/<your-username>/<your-repo>.git
   git push -u origin main
   ```
3. On GitHub: go to **Settings → Pages**.
4. Under **Build and deployment → Source**, choose **Deploy from a branch**.
5. Set **Branch** to `main` and folder to `/ (root)`, then **Save**.
6. Wait a minute, then your site is live at:
   ```
   https://<your-username>.github.io/<your-repo>/
   ```
7. Come back and update the "Live site" link at the top of this README.

## Notes

- `index.html` is fully self-contained (inline CSS/JS) except for one external stylesheet (Tabler Icons via jsDelivr CDN) — no build step needed.
- The video link and effort/time numbers on the page are already filled in; edit the `VIDEO_URL` constant and the `rows`/`modes` objects near the bottom of `index.html` if those change.
