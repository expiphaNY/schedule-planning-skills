---
name: deadline-backplanner
description: Plans backwards from a due date. Splits an assignment, essay, problem set, project or presentation into 3–6 milestones, gives each one its own dated task, leaves a buffer before the deadline, pads the user's time estimate by about 1.5×, and books working sessions for the big milestones in free time. Use when the user says something is due on a date, asks to plan a project or assignment, or wants to break a deliverable into steps before a deadline.
license: MIT
---

# Deadline Backplanner

## Purpose
Turn one deliverable and its due date into a short chain of dated milestones, planned backwards from the deadline, so the work is spread out and finishes early instead of the night before. People underestimate how long work takes, so every estimate gets padded and the plan ends with a buffer.

## 1. Gather the facts first
Read the calendar and the conversation before you ask anything. You need:

| Fact | If the user did not say |
|---|---|
| The deliverable and its course or project | Use what they wrote as the title. |
| Due date (and time, if any) | Ask. |
| Type: essay, problem set, project or presentation | Infer it from the wording. Ask only if it could be two types. |
| Rough size: pages, questions, or hours they expect it to take | Ask. |

**Ask with the `ask_user` tool** (or your app's equivalent question tool) only for a fact above that is missing or unclear. Put every open point into **one** `ask_user` call: at most 3 questions, 2–3 concrete options each, most likely first. Example:

> **How big is the HIST 210 essay?** → "Short: 1–3 pages, about 4 hours" · "Medium: 4–7 pages, about 8 hours" · "Long: 8+ pages, 12+ hours"

Also ask before you overlap an existing event or put more than 3 hours of work in one day. Do not ask about things this skill already decides.

## 2. Planning framework
1. **Milestones by type.** Use 3–6 milestones, always ending with Submit. Merge steps for small items, split Draft for large ones.

   | Type | Milestones |
   |---|---|
   | Essay | Research → Outline → First draft → Revise → Final edit → Submit |
   | Problem set | Read and sort the questions → First pass → Hard questions → Check answers → Submit |
   | Project | Scope and plan → Build part 1 → Build part 2 → Test and fix → Write-up → Submit |
   | Presentation | Research → Outline and slides → Script → Rehearse → Submit or present |

2. **Pad the estimate.** Split the user's time estimate across the milestones, then multiply each share by about 1.5. If they said 6 hours, plan about 9.
3. **Work backwards.** Put Submit on the due date. Before it, leave a **buffer**: one empty day for anything over a day's work, or a few empty hours on the due day for small items. Then place the other milestones in reverse order, each on an earlier day.
4. **One milestone per day.** Never put two milestones on the same day. If there are not enough days, merge milestones rather than stacking them, and say so.
5. **Too late to fit?** If the padded work cannot fit before the due date, keep the order and the buffer, shorten the middle milestones, and tell the user plainly how tight it is.
6. **Fit the real calendar.** Never overlap classes or existing events. Use `list_calendar_items` to find free time. Keep 10 minutes around each working session, nothing before 08:00 or after 23:00, and at most 3 hours of work per day unless the user agrees.

## 3. Item format
- **One task per milestone**, due on that milestone's day. Title: `<course or project>: <milestone>`, e.g. `HIST 210: First draft`. The Submit task is due on the real due date.
- **A working session for each big milestone** (1 hour or more of padded work): an **event** in a free slot on the same day as its task. Title: `Work: <course or project> <milestone>`. Description: one sentence on what to finish, e.g. "Write the full first draft from the outline; rough is fine."
- Small milestones get a task only.
- Do not delete anything. To change a plan, move or edit the items instead.

## 4. When you are done
Reply with a short list in date order: each milestone, whether it is a task, and any working session with its time. Then one line saying which days are the buffer, and one line saying nothing overlapped (or what you had to merge or shorten). Keep it brief. Example:

> **Essay: HIST 210, due Fri Nov 13**
> - Wed 4 – Outline (task) + "Work: HIST 210 outline", 4:00–5:00 pm
> - Fri 6 – First draft (task) + "Work: HIST 210 first draft", 2:00–4:00 pm
> - Mon 9 – Revise (task) + "Work: HIST 210 revise", 3:00–4:30 pm
> - Wed 11 – Final edit (task)
> - Fri 13 – Submit (task, due)
>
> Thu 12 is left empty as a buffer. Nothing overlapped.
