# Design specs: week 1 build

**Work sample, Agueda Schwartz.** The first set of design specs I wrote for the pilot, April 3, 2026, for a UX researcher and a colleague who studies community dynamics to review, and for the Claude Code instance that built and ran the cohort's Slack workflows (the "cohort agent"). Each spec was written to be tested at the next live session. Names are removed; "MR" is the weekly management report and "MOKR" the mission, objectives and key results document, both from the partners' methodology.

---

## How to read this doc

Each spec describes one Slack automation to deploy into the live cohort. The cohort agent builds and deploys all four. I observe the results at the next session and in the week's async data (Google Docs comments, Slack activity, Drive submissions).

**Decision rule:** after the session, each feature gets KEEP, ITERATE or KILL against the criteria below. We don't need statistical significance; we need signal direction from a small cohort.

---

## Spec 1: Peer review scaffolding prompts

### What it does
Adds four scaffolding prompts to the existing Tuesday 6 PM peer review reminder, so people who don't review get a concrete framework for what to look for in a peer's report.

### Why we think this will work
- Most participants left no comments on reports. Two people did nearly all the reviewing.
- In the last session I said publicly that I'd felt both barriers myself: (1) not understanding the methodology well enough to critique it, (2) not knowing what useful feedback looks like.
- Two experienced members offered a four-prompt framework in that session, and the group validated it on the spot.
- A mentor in the group framed the confidence gap as shared: if one person is confused, they may be speaking for others.
- The UX researcher validated scaffolding as the right first intervention.

### How it works

**Monday AM, new preview message:**

> Heads up: peer review comments are due tomorrow (Tuesday) evening. This week we're trying something new. Check tomorrow's message for a quick framework to help you give useful feedback.

**Tuesday 6 PM:**

> :sparkles: **NEW: Peer review framework** :sparkles:
>
> Peer review reminder: comments on this week's management reports are due tonight.
>
> Your feedback matters. It's the main way people in this group get outside perspective on their blind spots. Even one comment changes the quality of someone's week.
>
> Not sure what to say? Try reviewing for:
> - *Clarity:* Is this person thinking clearly about their problem?
> - *Blind spots:* What might they not see from the inside?
> - *Distractions:* Are they drifting from their MOKR objectives?
> - *Resources:* Do you know a person, tool, or example that could help?
>
> Pick one report and try one bullet point. If someone else already left a comment, add a different perspective. You don't need to repeat what's been said.

**Two messages, not one.** Monday sets the expectation; Tuesday delivers the framework. The NEW marker signals this isn't the same reminder people have been ignoring.

### Success criteria (KEEP if any)
- At least one new commenter appears on reports, beyond the two current reviewers
- Total comment count rises from the previous week's baseline
- Any comment explicitly references one of the four prompts
- The most active reviewer's own report gets more than one comment (reciprocity)

### Kill criteria (KILL if all)
- Zero new commenters after one full cycle
- Total comment count flat or down
- Participants report ignoring the prompts ("I didn't read it", "I don't have time")

### Assumptions being tested
1. The main barrier is not knowing what to say (a review skill gap), not not understanding the documents (a methodology gap). If it's the second, prompts won't help.
2. Prompts inside a reminder will be read and acted on. Current reminders get low engagement, and a participant said older users batch or ignore Slack notifications entirely.
3. The four-prompt framework is the right scaffolding. It came from one session and hasn't been tested beyond that room.
4. The barrier is skill, not social. The community-dynamics colleague flagged that fear of critiquing peers could be the real blocker, in which case the fix is normalizing feedback in onboarding.

### Reviewer input
- **UX researcher:** the least risky of the four features. Open question: pair it with a model comment? Decide after seeing the week's data.
- **Community dynamics:** strengthen the "why this matters" line. The barrier may be onboarding, not review skill, so future cohorts may need better onboarding, not just a better reminder.

### Build notes for the cohort agent
- Build both messages: the Monday preview and the Tuesday framework.
- Replace the current generic Tuesday reminder; don't add a new one.
- Keep the tone peer-to-peer: "Not sure what to say?", not "Here is the peer review rubric."
- "Pick one report and try one bullet point" is intentional. It lowers the bar.
- Keep the NEW marker at first; it can come off once the format is established.

---

## Spec 2: Accountability nudges with names

### What it does
Two automated messages that name non-submitters and non-attendees:
1. **Tuesday AM:** who hasn't submitted a report to the Drive folder yet
2. **Wednesday PM, after the session:** who was absent without advance notice

### Why we think this will work
- Attendance and submissions had dropped, and the people not submitting were also not reviewing.
- In the last session the group asked for peer accountability, to the whole group rather than to one person.
- Our touchpoint map already ranked a non-submitter nudge as the first priority for automation.

### How it works

**Tuesday 9 AM:**

> MR check-in: Reports due today for this week's review cycle.
>
> :white_check_mark: Already submitted: [Name], [Name], [Name]
> Not yet: [Name], [Name]
>
> If you need more time, drop a note here so reviewers know when to expect yours.

**Wednesday 9 PM, after the session:**

> Session [N] wrap-up:
>
> :white_check_mark: Attended: [Name], [Name], [Name], [Name]
> Absent: [Name] (gave advance notice), [Name] (no notice)
>
> Showing up is how this group works. Your presence shapes the conversation even when you're not presenting. If you can't make it, a heads-up in the channel helps the group plan.
>
> Recording + notes shared via DM with those who gave advance notice.

**Implementation:** on Tuesday morning the agent checks the week's Drive folder against the participant list. On Wednesday I provide the attendance list, and the agent checks the channel for advance notices.

### Success criteria (KEEP if any)
- Submissions rise from the previous week
- At least one previously silent participant posts advance notice or submits
- Active members say the accountability feels right ("this is what we asked for")

### Kill criteria (KILL if any; this is the risky one)
- Any participant pushes back ("this feels like shaming") or messages me to complain
- A named participant disengages further after being named
- The group dynamic shifts from supportive to punitive

### Assumptions being tested
1. Being named publicly will motivate, not alienate. The people who asked for it were in the room; the people who would be named were not.
2. Non-submission is an accountability problem, not friction (too many steps) or unclear expectations.
3. This works beyond this cohort's culture. The UX researcher doubted it would.

### Reviewer input
- **UX researcher:** pushed back hard. For groups that don't share this cohort's culture, they didn't think it would work. In the product it must be a configurable group setting, not a default. For this cohort, worth testing because the group asked for it. The bot reports facts ("not yet submitted"), never judgment ("you're behind").
- **Community dynamics:** first instinct was concern about naming in public; agreed to test once they heard the group asked for it. Proposed a second version built on positive visibility: announce who did submit, like kudos in a fitness app. Both reviewers independently flagged that this depends on the group, which is the strongest signal that the product needs configurable accountability.

### Build notes for the cohort agent
- Tuesday: list the current week's report folder in Drive and compare filenames against the participant list.
- Wednesday: attendance comes from me. Don't try to detect it automatically.
- **Tone is everything.** "Not yet", not "missing". "Drop a note", not "explain yourself". I review the copy before it deploys.
- Lead with who did submit or attend, then who hasn't. Celebrate the behavior we want.
- Recording access is tiered: those who gave notice get it by DM; others can ask. It reinforces the norm without punishing.
- Log that this needs a group-level toggle in the product. Not building the toggle now.

---

## Spec 3: Targeted comment routing

### What it does
Adds a section to the Tuesday reminder that points people to reports with zero comments, so the ask becomes "read this one report", not "review everyone".

### Why we think this will work
- The most active reviewer's own report got one comment. The gap between giving and receiving review is a sustainability risk.
- Reviewing may feel overwhelming ("I have to read six reports?"). Routing reduces it to one.
- The UX researcher proposed this feature, seeing the reciprocity gap as a design problem, not just a participation problem.

### How it works

**Tuesday 6 PM, a visually separate section in the Spec 1 message:**

> ──────────────
> :eyes: **Reports that could use a fresh set of eyes:**
> - [Name]'s MR: 0 comments so far
> - [Name]'s MR: 0 comments so far
>
> [Link to Drive folder]

The divider and the emoji header make two distinct tasks in one message: how to review, and who needs it. One call to action serves both, so it isn't repeated here.

### Success criteria (KEEP if any)
- The named reports get at least one comment within 24 hours
- Comments spread out: the top reviewer's share drops below 70% of the total
- Someone says they reviewed a report because the bot pointed them there

### Kill criteria (KILL if all)
- Zero-comment reports stay at zero after being surfaced
- Participants feel called out ("why is my report flagged?")
- No measurable change in how comments are distributed

### Assumptions being tested
1. Part of the barrier is decision fatigue ("which one do I read?"), not just skill or time.
2. Surfacing zero-comment reports creates positive pressure to review, without negative pressure on the author.
3. People follow a specific suggestion more than a general reminder.

### Reviewer input
- **UX researcher:** framing matters. "Could use fresh eyes" is better than "nobody reviewed this".
- **Community dynamics:** set a reciprocity norm in onboarding for future cohorts ("you get feedback, you give feedback"), and in the product, surface the most neglected documents first.

### Build notes for the cohort agent
- An add-on to Spec 1, not a separate message.
- If reading comment counts programmatically is hard, I provide the zero-comment list on Tuesday morning.
- If every report is at zero, skip the section. It only adds signal when there's a difference.

---

## Spec 4: Unified MOKR and report template

### What it does
One Google Doc template that holds the MOKR (updated monthly) and the weekly report together, to cut the switching between two documents.

### Why we think this will work
- I felt the friction myself as a participant: checking whether my priorities traced to my key results meant switching documents.
- A mentor explained why the methodology keeps them separate: copying and updating is easier with separate files. That made sense on paper; it may not hold in Google Docs, where sections can be updated in place.
- The UX researcher added this to scope, seeing template friction as a cause of submission drop-off.

### How it works

```
MOKR (updated in place; version history tracks changes)
├── Mission
├── Objective 1 → Key Results
├── Objective 2 → Key Results
├── Objective 3 → Key Results
└── Peer feedback log (appended each review cycle)

───────────────────────────────────

Management report, week of [DATE]
├── Key indicators (maps to the key results)
├── Progress (deliverables, not effort)
├── Plans (binary, dated)
├── Problems (with proposed solutions)
└── Priorities (3 max, tagged to key results)

Previous weeks (collapsed below)
```

**Test plan:** I test it on my own documents first. If it works better, I offer it to the group at the session as an option. No forced migration.

### Success criteria (KEEP if any)
- It reduces my own switching between the two documents
- At least one other participant adopts it voluntarily
- Submissions don't drop because of the change

### Kill criteria (KILL if any)
- The unified doc is unwieldy (too long, harder to update weekly)
- A methodology veteran pushes back on departing from the methodology
- Participants are confused by the new format

### Assumptions being tested
1. The separation causes real friction for others, not just for me. My experience may not be representative.
2. One document is simpler than two in Google Docs. It could also be harder: longer, harder to find the right section.
3. The methodology's document structure can be adapted without losing its value.

### Reviewer input
- **UX researcher:** test on yourself first; that's the right move for a methodology change. Ask the people who know the methodology best whether the separation serves a purpose we're not seeing. Critical constraint: the MOKR must stay visible while writing the report, like a frozen row in a spreadsheet. Later, the agent could keep the peer feedback log updated from the comments.

### Build notes for the cohort agent
- Build one template from my current MOKR and report.
- Keep a condensed MOKR table at the top of each week's report section, so the key results are visible without scrolling.
- Separate previous weeks clearly.
- Don't migrate anyone else's documents.

---

## Cross-cutting design principles

1. **One message, not four.** Specs 1 and 3 share one Tuesday message. Spec 2 is two messages. Don't flood the channel.
2. **Peer-to-peer tone.** The bot speaks as the system but sounds like a helpful peer.
3. **Measure behavior, not sentiment.** Success is more comments, submissions and attendance, not "people said they liked it".
4. **Kill fast.** If a feature creates negative energy, kill it immediately. Don't wait for the session.
5. **Configurable in the product.** What works for this cohort becomes a setting, not a default. (UX researcher)
6. **Adults co-create norms.** Offer scaffolding ("other groups have handled this like…") and let the cohort shape its own rules. (UX researcher, adult learning theory)
7. **Positive visibility over negative accountability.** Lead with who did the thing, not who didn't. (both reviewers)
