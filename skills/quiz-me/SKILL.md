---
name: quiz-me
description: Quiz the user on their Japanese flashcards from Nihontekini. Use when they say "quiz me", "test me", "practice my weak words", "drill me on what I learned this week", or want to check whether they remember their words.
---

# Quiz me

Two modes. Use the **recorded quiz** unless the user asks for something else, such as
"what I learned this week", or the free plan has no quizzes left.

## Recorded quiz (saved to the app)

1. Call `make_quiz` with `size` (default 10, at most 30) and an optional `deck_id`.
   It picks their weakest words and mixes meaning, word and reading questions, each with
   four options and its answer. The quiz shows in the app's test history.
2. Ask **one question at a time**. Show the prompt and the options numbered 1 to 4. Never
   show the answer, and never hint at it, before they pick. When the question tests the
   reading, don't show the reading or romaji of the word.
3. After each pick, say right or wrong, give the correct answer, and add one short line of
   explanation (a mnemonic, the kanji's meaning, or how it is used).
4. At the end, call `record_quiz_answers` once with the `quiz_id` and every answered
   question as `{ card_id, picked }`, where `picked` is the option text, number or letter
   they chose. Questions they skipped are left out.
5. Show the score from the result and list the words they missed, each as
   word (reading, romaji): meaning.

If they stop part way, still record the questions they answered.

On the free plan, `make_quiz` counts against the monthly allowance and its result has
`freePlan.quizzesLeftThisMonth`. If `make_quiz` is refused because the allowance is used
up, don't retry. Say so in one or two sentences (see `plan-and-limits`) and offer the
practice quiz below, which doesn't count.

## Practice quiz (not recorded)

For "test me on what I learned this week", a specific deck, or when quizzes are used up:

1. Call `get_learned_words` (status `learning` or `all`, optional `deck_id`) or
   `get_weak_words`.
2. Make the questions yourself from those words, in the same one-at-a-time style. Mix
   "what does X mean", "which word means Y" and "how do you read X". Build wrong options
   from their other words so they are plausible.
3. At the end, give the score and the missed words. Tell them this one isn't saved to the
   app; nothing is sent to `record_quiz_answers`.

## Rules

- Never invent a `quiz_id` or `card_id`. Use the ones `make_quiz` returned.
- If they have no learned or weak words yet, say so and offer to add some cards first
  (`build-deck`).
- Outside reading questions, write Japanese with reading and romaji, e.g.
  猫 (ねこ, neko). Answer in the user's language.
