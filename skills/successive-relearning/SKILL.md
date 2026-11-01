---
name: successive-relearning
description: Plans study time with successive relearning. Splits each course into short retrieval-practice blocks spread over different days, adds a short same-day relearn-to-criterion block for anything not yet recalled, and sets how many blocks to schedule from course difficulty. Use when the user asks to plan studying, make a study schedule, prepare for an exam, midterm or quiz, or spread review across the week.
license: MIT
---

# Successive Relearning Scheduler

## Purpose
Put the user's study time on their calendar using successive relearning: practise recalling the material until every item is right once (the **criterion**), then come back on later, spaced days and relearn it to criterion again. Spacing plus repeated retrieval beats one long session for the same total time.

## 1. Gather the facts first
Read the calendar and the conversation before you ask anything. You need:

| Fact | If the user did not say |
|---|---|
| Courses and topics | Ask. |
| Difficulty of each course for this user | Ask. Never guess it from the course name. |
| Exam or due date | Plan the next 7 days. |
| When they like to study | Free time between 09:00 and 21:00. |

**Ask with the `ask_user` tool** (or your app's equivalent question tool) whenever difficulty is unknown, a fact above is unclear, or two readings of the request would give different schedules. Put every open point into **one** `ask_user` call: at most 3 questions, 2–3 concrete options each, most likely first. Example:

> **How hard is MATH 135 for you?** → "Hard: 4 blocks a week" · "Moderate: 3 blocks a week" · "Light: 2 blocks a week"

Also ask before you move or delete an existing event, overlap anything, or put more than 3 hours of study in one day. Do not ask about things this skill already decides.

## 2. Scheduling framework
1. **Spacing rule.** Never one long block per topic. Split it into 25–50 minute blocks on different days. Example: two 45-minute blocks on Tuesday and Thursday, not one 90-minute block on Tuesday. Leave at least one day between blocks of the same topic.
2. **Difficulty sets the dose** (per course, per week):

   | Difficulty | Blocks | Length | Relearning sessions before the exam |
   |---|---|---|---|
   | Light | 2 | 30 min | 3 |
   | Moderate | 3 | 45 min | 4 |
   | Hard | 4 | 50 min | 5 |

3. **Expanding gaps.** The first block is initial learning to criterion. Later sessions come about 1, 3 and 7 days after it. If the exam is closer, shrink the gaps to fit and keep at least one day between sessions. The last session is 1–2 days before the exam, never the night before.
4. **Relearn-to-criterion block.** After each study block, add a 15–20 minute block later that same day, at least 2 hours after it ends, for items not yet recalled correctly. The user skips it if everything was right. Do not add one after a light course's blocks when the day is already full.
5. **Retrieval, not rereading.** Every block is self-testing: flashcards, practice problems, or writing out what they remember on a blank page, checking answers after each attempt, until every item is right once.
6. **Interleave.** Alternate courses through a day. Do not put two blocks of the same course back to back.
7. **Fit the real calendar.** Never overlap classes or existing events. Keep 10 minutes between blocks, nothing before 08:00 or after 23:00, and at most 3 hours of study per day unless the user agrees. If it does not all fit, keep the spacing and shorten or drop blocks, lowest-priority course first, then say what you cut.

## 3. Block format
- Make each block an **event** with a start time, not a to-do task.
- Title: `Study: <course> – <topic>` or `Relearn: <course> – <topic>`.
- Description: one sentence with the method and the criterion, e.g. "Retrieval practice: solve the 2.3 practice problems from memory until each one is right once."

## 4. When you are done
Reply with a short list grouped by day. Say which difficulty you used for each course and anything you shortened or cut. Keep it brief.
