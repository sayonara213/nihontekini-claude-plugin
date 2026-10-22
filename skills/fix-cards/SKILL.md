---
name: fix-cards
description: Fix, move, suspend or delete the user's Nihontekini flashcards. Use when they say a card's reading, meaning or example is wrong, want cards moved between decks, want duplicates cleaned up, or say "I already know this", "stop showing me X" or "delete these cards".
---

# Fix cards

## Find the card first

Call `find_cards` with the word, reading or meaning (and `deck_id` if they named a deck)
to get each `card_id`. If several cards match, show them briefly and ask which one. Never
guess or invent a `card_id`.

`own: false` marks a card from a predefined deck (JLPT and others). Those can't be edited
or deleted, only suspended.

## What to call

| The user wants | Call | Notes |
|---|---|---|
| Fix a reading, meaning, explanation, examples or tags | `edit_card` | Only the fields you pass change. An empty `reading` or `explanation` clears it. Progress is kept. |
| Move a card to another of their decks | `edit_card` with `deck_id` | Get the target from `list_decks` (`own: true`). |
| "I know this", "skip this", "stop showing it" | `suspend_cards` | Keeps the progress. Works on predefined cards. |
| Bring a suspended card back | `suspend_cards` with `suspended: false` | |
| Remove cards for good | `delete_cards` | See below. |

Use `suspend_cards`, not `delete_cards`, when they mean "I don't want to study this".

## Before deleting

`delete_cards` removes the cards and their learning progress, and it can't be undone.
List exactly which cards will go (word, reading, deck) and wait for a clear yes. Only
their own cards can be deleted; offer to suspend predefined ones instead. For "delete all
my cards", confirm the deck and the count first, and never touch predefined decks. At
most 200 ids per call.

## Duplicates

Find them with `find_cards`, show the pairs, and ask which to keep. Keep the one with more
progress unless the user says otherwise. Suspend or delete the other once they agree.

## Card rules

- `meaning` is English glosses only: `["to study", "diligence"]`. No romaji, kana,
  reading, part of speech or notes; those go in `reading` (kana only) or `explanation`.
- Example `reading` uses Anki-style furigana:
  `"日本語[にほんご]を 勉強[べんきょう]しています。"`

Say what changed in a line or two, and that the app shows it after it syncs. In the chat,
write Japanese with reading and romaji, e.g. 今日 (きょう, kyō).
