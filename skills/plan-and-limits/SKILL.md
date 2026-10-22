---
name: plan-and-limits
description: Explain the user's Nihontekini plan, free-plan limits and Premium. Use when they ask "how many cards can I still add", "do I have Premium", "what does Premium give me" or "buy me Premium", and whenever add_cards or make_quiz is refused because the free allowance is used up.
---

# Plan and limits

## The plans

Studying their own cards in the app is always free. The free plan limits what AI agents can
do each calendar month (UTC): 50 cards added and 3 quizzes made. Deleted cards still count.
Premium removes those limits, unlocks the predefined JLPT N4 to N1 decks, and makes the
in-app Test me unlimited. Premium is bought only by the user, in the Nihontekini iOS app
under **Me > Premium**. You can't buy, start or manage it for them.

## What to do

1. Call `get_plan`. It returns `plan` (`free` or `premium`), `agentLimits` (`cardsLeft`,
   `cardsPerMonth`, `quizzesLeft`, `quizzesPerMonth`, `resetsOn`) or `"none"` on Premium,
   and on the free plan `premiumUnlocks` and `howToUpgrade`.
2. Answer in two or three sentences: what is left, when it resets (`resetsOn`), and, if
   they asked or hit the limit, what Premium unlocks and that upgrading happens in the app
   under Me > Premium.
3. When a limit is the reason you can't do something, offer the free alternatives: add the
   rest after the reset, add cards by hand in the app, use a practice quiz (`quiz-me`), or
   use Test me in the app.

## When a tool refuses

`add_cards` and `make_quiz` return an error with a plain-English message when the allowance
would be exceeded. Nothing was added; it's all or nothing. If the message says
"add at most N cards now", you may offer to add the N most useful cards instead.

- Pass the message on plainly. Don't retry the same call, and don't split a batch to slip
  under the limit.
- Don't pretend it worked, and don't say you can upgrade them.

## Tone

Mention Premium once, when it's relevant, and don't repeat the upsell later in the
conversation once they've seen it. No pressure, no urgency, no "only today". If they say
"buy me Premium", explain that only they can, in the app under Me > Premium.
