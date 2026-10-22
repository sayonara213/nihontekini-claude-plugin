---
name: progress-check
description: Summarize the user's Japanese study progress in Nihontekini. Use when they ask "how am I doing", "what's my progress this week", "how many reviews are due", or which words they keep forgetting.
---

# Progress check

1. Call `get_progress` (words started and known, reviews due now, reviews in the last
   7 days) and `get_weak_words` with a `limit` of about 5.
2. Write a short, encouraging summary, about four lines:
   - Words started and known, and the reviews done this week.
   - Reviews due now.
   - Their five weakest words, each as word (reading, romaji): meaning.
   - One concrete next step, e.g. "12 reviews are due; open the app and clear them", or
     "want me to quiz you on these five?" (see `quiz-me`).
3. On the free plan, call `get_plan` and add one line on what is left this month
   (cards and quizzes) and when it resets. Don't mention Premium here unless they ask.

If they have no cards yet, say so and offer to build a first deck (`build-deck`).
Keep tool output out of the chat; summarize it. Answer in the user's language.
