# Sales Navigator: Architecture

## The short version

Sales Navigator is **Claude Code running in this folder**, with a few plain-text files that tell it how to be a sales assistant.

- No server, no database, no website to host.
- No API key. It uses your **Claude Pro account** because Claude Code signs in with it.
- Everything the tool "knows" lives in Markdown files you can edit yourself.

To use it, open a terminal in this folder and run:

```bash
claude
```

Then type `/sales-call` and Claude walks you through the call.

## How it fits together

```text
 You (on a call or writing an email)
        │
        ▼
 Terminal: `claude`  ──signs in with──▶  Your Claude Pro account
        │
        │ reads automatically
        ▼
 CLAUDE.md                  ← who it is and the rules it must follow
 .claude/skills/sales-call/ ← the step-by-step call script
 knowledge/products.md      ← the 5 products and when to suggest each
 knowledge/stories.md       ← approved customer stories with links
        │
        ▼
 Claude asks the questions → you type answers →
 it suggests one product, 1–3 stories, and a draft follow-up email
```

## The files

| File | What it's for | Who edits it |
| --- | --- | --- |
| `REQUIREMENTS.md` | What the tool should do (already written) | You |
| `ARCHITECTURE.md` | This file: how it's built | You |
| `CLAUDE.md` | The rules. Claude Code reads this every time it starts in this folder. | You |
| `.claude/skills/sales-call/SKILL.md` | The call script: the 12 questions, then suggestion, stories and email. Running `/sales-call` starts it. | You |
| `knowledge/products.md` | The product table from the requirements, plus any extra detail (pricing notes, limits, talking points). | You |
| `knowledge/stories.md` | The only customer stories Claude may use: company, industry, what they did, headline result, link. | You |

### What goes in `CLAUDE.md`

A few short rules, in plain English:

- You are Sales Navigator, a helper for InfluxData salespeople.
- Always suggest exactly **one** database product. Add Telegraf or Telegraf Enterprise only when the customer needs to collect data.
- Only use products from `knowledge/products.md`.
- Only use customer stories from `knowledge/stories.md`. Never make one up. If nothing fits, say so.
- Keep answers short. The salesperson may be on a live call.
- Follow-up emails are drafts. Remind the salesperson to review before sending.

### What goes in the skill

The skill is the call script, one step at a time:

1. Ask the 12 questions from `REQUIREMENTS.md`, in order, a few at a time. Let the salesperson skip any question.
2. Name one product and give the reason in one or two sentences.
3. Show 1–3 matching stories from `knowledge/stories.md`, each with a link.
4. Write a short follow-up email the salesperson can copy.

There's also a fast path: the salesperson can paste a paragraph of notes (like the battery storage example in the requirements) and skip straight to the suggestion.

## Why this design

- **Simplest thing that works.** Claude Code is already a chatbot. We only add instructions and facts.
- **Uses your Pro plan.** Claude Code is included with Claude Pro, so there's no separate API bill.
- **Easy to change.** New product or new customer story? Edit a Markdown file. No code to rebuild.
- **Stays accurate.** Claude only picks from lists you control, so it won't invent products or customers.

## Security and privacy

- **Sign-in:** The requirements say only InfluxData employees may use it. Because it only runs on your laptop, under your Claude login, your laptop login *is* the sign-in. If teammates want to use it later, each person clones the repo and signs in with their own Claude account.
- **Customer data:** Whatever you type is sent to Claude under your account. Share what you need for the suggestion (industry, size, needs). Leave out things like passwords, contract numbers or personal details.
- **Notes:** Nothing is saved unless you ask. If you want to keep call notes, save them in a `notes/` folder and add `notes/` to `.gitignore` so customer details never get pushed to GitHub.

## Keeping it up to date

- **New customer story:** Add a row to `knowledge/stories.md`. Copy the link from the InfluxData [Customers](https://www.influxdata.com/customers/), [Partners](https://www.influxdata.com/partners/) or [Blog](https://www.influxdata.com/blog/) pages.
- **Product change:** Edit `knowledge/products.md`.
- **New or changed question:** Edit the skill file and `REQUIREMENTS.md` together.

You can also ask Claude to do these edits for you, for example: *"Read the Seadrill customer page and add it to stories.md."*

## Later, only if you need it

These are **not** part of the first version:

- **A web page instead of the terminal**, if you want something nicer to look at during calls. This would be a small local web page that passes your questions to Claude Code behind the scenes.
- **Saving call history** to a local file per customer.
- **Sharing with the team.** This one is a bigger change: a team tool should use a company API account, not a personal Pro plan.

## Build order

1. Create `knowledge/products.md` and `knowledge/stories.md` from the tables in `REQUIREMENTS.md`.
2. Write `CLAUDE.md` with the rules above.
3. Write `.claude/skills/sales-call/SKILL.md` with the call script.
4. Test it with the battery storage example from the requirements. Check it suggests Cloud Dedicated + Telegraf and shows Seadrill.
5. Try it on a real (or practice) call and adjust the wording.
