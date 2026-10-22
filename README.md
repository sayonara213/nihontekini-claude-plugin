# Nihontekini plugin for Claude

Lets Claude work with your [Nihontekini](https://nihontekini.app) flashcards. Ask Claude to
fill your decks with Japanese words, fix cards, check how you are doing, or quiz you on the
words you keep forgetting. Changes reach your phone the next time the app syncs.

> **Early access.** The Nihontekini iPhone app is not on the App Store yet; it is in testing
> and coming soon. The plugin and its server already work: you can connect, build decks and
> take quizzes in Claude today, and your cards are waiting in your account when the app comes
> out. See [nihontekini.app](https://nihontekini.app) for the launch.

## About Nihontekini

Nihontekini (日本的に, にほんてきに, nihonteki ni, "the Japanese way") is an iPhone app for learning
Japanese with Anki-style flashcards and FSRS spaced repetition. Each card has the word, its
reading, English meanings, an explanation of nuance and usage, example sentences with furigana,
and tags. Readings, meanings and examples you leave out are filled in from the JMdict
dictionary. There are predefined JLPT decks and your own decks; Claude works with both.

## What you can ask Claude

| Skill | Use it for | Try |
|---|---|---|
| `build-deck` | Add cards from a topic, JLPT level, pasted text, song lyrics or a photo of a menu or sign | "Add 20 N5 food words to a deck called Kitchen" |
| `quiz-me` | A multiple-choice quiz on your weakest words, one question at a time, saved to the app. Or a practice quiz on what you learned this week | "Quiz me on my weak words" |
| `fix-cards` | Fix a reading or meaning, move cards between decks, suspend words you already know, delete cards (Claude asks first) | "I already know ありがとう, stop showing it" |
| `progress-check` | A short summary: words started and known, reviews due, your weakest words, one next step | "How am I doing this week?" |
| `plan-and-limits` | What is left of the free plan this month and what Premium adds | "How many cards can I still add this month?" |

## Install

**claude.ai, the desktop app and mobile:** go to **Customize > Plugins > Add > Add
marketplace** and enter `sayonara213/nihontekini-claude-plugin`, then add Nihontekini. Open the
plugin's **Connectors** tab and connect it once. The plugin then works in chat on web, desktop
and mobile, in Cowork and in Claude Code.

**Claude Code only:**

```text
/plugin marketplace add sayonara213/nihontekini-claude-plugin
/plugin install nihontekini@nihontekini
```

Then run `/mcp`, pick **nihontekini** and sign in.

Either way, you sign in once in the browser with your email and a one-time code, then approve
the connection. If you don't have an account yet, signing in creates one. You can revoke the
connection any time in the app under **Me > AI agents**.

## Plans

Studying your own cards is always free. On the free plan, AI agents such as Claude can add 50
cards and make 3 quizzes a month, and the allowance resets on the 1st (UTC). Premium removes
those limits, unlocks the predefined JLPT N4 to N1 decks and makes the in-app Test me
unlimited. Premium is bought only in the iPhone app, under **Me > Premium**; Claude can tell
you what is left but can't buy or change your plan.

## Data

The plugin has no code of its own. It is skills (instructions for Claude) and one remote MCP
connector, `https://api.nihontekini.app/mcp`, run by Nihontekini. Through it, Claude reads and
changes your Nihontekini data: decks and cards, review history and progress, quizzes and your
answers, and your plan and how much of the free monthly allowance is left. It sends nothing
anywhere else. See the [privacy policy](https://nihontekini.app/privacy) and
[terms](https://nihontekini.app/terms).

## Support

Questions and bug reports: [nihontekini.app/contact](https://nihontekini.app/contact).

## For developers

| Path | What it is |
|---|---|
| `.claude-plugin/plugin.json` | Plugin manifest |
| `.claude-plugin/marketplace.json` | A one-plugin marketplace, so the repo can be added as a marketplace |
| `.mcp.json` | The Nihontekini remote MCP server (Streamable HTTP, OAuth sign-in) |
| `skills/` | The five skills above |
| `assets/icon.png` | Listing icon |

Validate after a change with `claude plugin validate .` and raise `version` in `plugin.json`
with every release. To try a local checkout: `claude --plugin-dir ./nihontekini-claude-plugin`.

The MCP server lives in `apps/api/src/mcp/` of
[nihontekini-main](https://github.com/sayonara213/nihontekini-main).
