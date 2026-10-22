---
name: build-deck
description: Add Japanese words to the user's Nihontekini flashcard decks. Use when they ask to add cards, make or extend a deck, or turn a topic, JLPT level, pasted text, song lyrics or a photo of a menu or sign into flashcards, e.g. "add 20 N5 food words to a deck called Kitchen".
---

# Build a deck

Adds cards to one of the user's own Nihontekini decks through the `nihontekini` MCP server.
The cards reach the phone on its next sync (pull to refresh in the app).

## Steps

1. **Pick the deck.** Call `list_decks`. Cards can only go into a deck with `own: true`.
   If the user named a deck that exists, use its `deck_id`. If they named a new one, pass
   `deck_name` and the server creates it. If they named none and they have more than one
   own deck, ask which one, or suggest a name and go ahead if the request makes it obvious.
2. **Choose the words.** From the topic, level, text or image, pick the words worth
   learning. For a large set, call `get_learned_words` (status `all`) and drop words they
   already have, so the list isn't wasted on duplicates.
3. **Check the allowance** before adding more than about 10 cards: call `get_plan`. On the
   free plan, `agentLimits.cardsLeft` is the most you can add this month. If the request is
   bigger, add the most useful words first, up to `cardsLeft`, and say how many you left
   out and why. Follow the `plan-and-limits` skill for the wording.
4. **Add.** Call `add_cards` with at most 200 cards per call. Only `term` is required.
5. **Report** in a few lines: how many were added, which were skipped because they were
   already in the deck, and, on the free plan, the `freePlan.cardsLeftThisMonth` from the
   result. Remind them the cards show up after the app syncs. Don't paste the raw result.

## Writing the cards

- **Leave `meaning` and `reading` out** when you are not sure; the server fills them from
  JMdict. Write them yourself only for slang, set phrases or words JMdict may not have, or
  when the user gave you the meaning they want.
- **`meaning` is English glosses only**, a string or a list:
  - Right: `["to study", "diligence"]`
  - Wrong: `["benkyō - to study"]`, `["to study (べんきょう)"]`, `["勉強: study"]`,
    `["(verb) to study"]`, `["lit. strong forcing"]`
  - No romaji, kana, reading, part of speech or notes. Nuance goes in `explanation`.
- **`reading`** is kana only, never romaji.
- **`type`** is `word`, `kanji`, `phrase` or `kana` when it isn't obvious.
- **`explanation`** (English) is where you add value: nuance, register (casual or polite),
  common mistakes, how it differs from a near synonym. Don't repeat the meaning there.
- **`examples`**: one or two short, natural sentences, `{ jp, reading, en }`. `reading` uses
  Anki-style furigana: a space before each word with kanji, its hiragana in brackets, e.g.
  `"日本語[にほんご]を 勉強[べんきょう]しています。"`
- **`tags`**: short, lowercase, e.g. `["n5", "food"]`.

## When things go wrong

- A quota refusal (`isError` with a message about the free plan): nothing was added. Don't
  retry or split the batch to get around it. Pass the message on, following
  `plan-and-limits`.
- An auth error: tell the user to sign in again with `/mcp` and pick Nihontekini.
- Never invent a `deck_id`. Get it from `list_decks` or the `add_cards` result.

## In the chat

When you show Japanese in the chat (not inside card fields), write the word with its
reading and romaji, e.g. 勉強 (べんきょう, benkyō). Answer in the user's language.
