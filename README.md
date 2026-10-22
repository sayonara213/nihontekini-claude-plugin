# Nihontekini plugin for Claude

Connects Claude to [Nihontekini](https://github.com/sayonara213/nihontekini-main), the iOS
app for learning Japanese with Anki-style flashcards and FSRS spaced repetition. Claude can
fill your decks with words, fix cards, check your progress and quiz you on the words you keep
forgetting. Changes reach the phone on its next sync.

## What's inside

| Path | What it is |
|---|---|
| `.claude-plugin/plugin.json` | Plugin manifest |
| `.claude-plugin/marketplace.json` | A one-plugin marketplace, so the repo can be added with `/plugin marketplace add` |
| `.mcp.json` | The Nihontekini remote MCP server (Streamable HTTP, OAuth sign-in) |
| `skills/build-deck` | Add cards from a topic, JLPT level, text, lyrics or a photo |
| `skills/quiz-me` | Recorded quizzes on weak words, and unrecorded practice quizzes |
| `skills/fix-cards` | Edit, move, suspend or delete cards |
| `skills/progress-check` | A short progress summary with one next step |
| `skills/plan-and-limits` | Free plan allowance, Premium, and quota refusals |

## Install (Claude Code)

```text
/plugin marketplace add sayonara213/nihontekini-claude-plugin
/plugin install nihontekini@nihontekini
```

Then run `/mcp`, pick **nihontekini** and sign in in the browser (email code or Sign in with
Apple). You approve the connection once; revoke it any time in the app under
**Me > AI agents**.

To try a local checkout instead: `claude --plugin-dir ./nihontekini-claude-plugin`, or
`/plugin marketplace add ./nihontekini-claude-plugin`.

Validate after a change with `claude plugin validate .`

## Plans

Studying your own cards is always free. On the free plan, AI agents can add 50 cards and make
3 quizzes a month. Premium, bought in the iOS app under Me > Premium, removes those limits.

## Try it

- "Add 20 N5 food words to a deck called Kitchen"
- "Quiz me on my weak words"
- "How am I doing this week?"
- "The reading of 今日 in my cards is wrong, fix it"
- "I already know ありがとう, stop showing it"
- "How many cards can I still add this month?"

## Server

The MCP server lives in `apps/api/src/mcp/` of nihontekini-main. If the API moves to another
host, change the `url` in `.mcp.json`.
