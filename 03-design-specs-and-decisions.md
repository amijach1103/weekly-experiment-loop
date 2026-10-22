# Design specs and decisions: a later build week

**Work sample, Agueda Schwartz.** The specs I wrote on April 17, 2026, for the cohort's sixth session, as revised after review on April 20 and 21, followed by the decisions I locked on April 20 after review. By this point the weekly rhythm (nudges, scaffolding, comment routing) was running; this week moved up to intelligence and structure, where the system reads the reports and shapes the session. Names are removed.

---

## How to read this doc

Each spec describes one feature to build before the session. Priority this week: **dashboard v2 > session structure > template prompt**. Specs are sequenced by build effort, not value. The dashboard is the biggest lift and starts Monday.

**Decision rule:** after the session, each feature gets KEEP, ITERATE or KILL. We're looking for signal direction, not statistical significance.

**The frame for this week** came from a peer facilitator's pushback after the last session: the metrics shouldn't become a standard of success for the peers, and could be used internally instead. I agreed. So this week we split the dashboard, structure the session, and prompt founders to reframe stuck metrics, without adding more nudges.

---

## Spec 8: Dashboard v2, two tiers

### What it does
Splits the first dashboard into two artifacts: a **peer pre-read** about where the group can help, and a **facilitator brief** with trajectory and airtime. It keeps the triage value the group validated and drops the "standard of success" framing.

### Why it's the top priority
- The group accepted dashboard v1 as a pre-read and read it before the session.
- A peer facilitator's pushback, described above.
- The community-dynamics colleague's review of v1: public posting is fine, progress visibility is safe.
- The UX researcher confirmed the split: the pre-read shapes how participants prepare; the brief shapes how the session is run.

### How it works

**Tier 1: peer pre-read** (Wednesday AM, public in the cohort channel):

```
:clipboard: Session 6 pre-read, Week 4

This week's experiments:
- [Name]: [plan from report, one line]

Where the group can help:
- [Name] ([build stage]): [problem, paraphrased with stage context] → needs [what they asked for]

Milestones this week:
- [Name]: [milestone, e.g. first customer conversation, first sale]

Tonight's order:
1. [Name]: 8 min, unresolved async issue: [topic]

:link: Full reports in Drive | Pinned message has the peer review tips
```

**Tier 2: facilitator brief** (Wednesday AM, DM to the two peer facilitators, archived in a facilitator notes folder):

```
:compass: Facilitator brief, Session 6

Trajectory (week over week, key indicators):
- [Name]: [metric → metric], [trend]

Submission + engagement:
- Reports in: X. Missing: [name(s)].
- Peer comments: X total. Top reviewers: [names]. Flat reviewers: [names]

System flags (things the participant did NOT ask for help on):
- Stuck key results (no progress 2+ weeks): [Name]: [KR]
- Missed commitments from last session: [Name]: [commitment]
- Outcome-vs-action red flags (stuck, and not self-flagged): [Name]: [KR]
- Non-submission patterns: [Name]: missed [N] of last [M] reports

Airtime recommendations (suggested, not prescriptive):
- Give extra room to: [Name]: stuck metric, problem in report
- Watch for: [Name]: heavy reviewer, light airtime last session

Session shape (60 min):
- 0:00–0:10  Commitments + announcements
- 0:10–0:50  Peer coaching, 5 slots × 8 min, ordered by unresolved async issue
- 0:50–0:55  Flex buffer
- 0:55–1:00  Close
```

**Implementation:**
1. Reports land in Drive on Monday; peer review runs Tuesday morning to Wednesday noon.
2. Wednesday morning, after the review window: the agent reads this week's and last week's reports **and the peer comments** (what was answered, what stayed open). That feeds both tiers.
3. I review both drafts. The pre-read posts to the channel before noon; the brief goes by DM and into the notes folder.
4. Facilitators get both tiers. The brief never goes to a shared channel.

Timing was revised on April 21 from a Tuesday pre-read to Wednesday morning, so the pre-read captures what peer review resolved instead of freezing at submission time. The cohort still has six to eight hours to read it before the session.

### Success criteria (KEEP if any)
- Participants reference the pre-read in the session ("I saw [Name]'s problem and was thinking…")
- A facilitator uses the brief to shape the session (airtime, order)
- Session time shifts toward unresolved issues and away from general status
- No one reports feeling surveilled or graded

### Kill criteria (KILL if all)
- The pre-read is ignored
- The brief doesn't change how the session runs
- Anyone raises the "standard of success" concern again

*Kill protocol: this faces the cohort, so a kill is discussed with the group before the feature is removed.*

### Assumptions being tested
1. Moving metrics out of the peer doc removes the concern without losing triage value.
2. Facilitators will use the brief, not just receive it.
3. "Unresolved async issue" is a better ordering principle than reciprocity or volunteering.
4. The pre-read changes preparation: people read reports more carefully because the session hinges on the help they offer.

### Build notes for the cohort agent
- Read two weeks of reports per participant from Drive.
- Paraphrase problems with build-stage context; don't quote them verbatim.
- Tone: "where the group can help", never "who's struggling". "Unresolved async issue", never "problem".
- The pre-read fits one Slack message. If it scrolls, trim.
- I sign off on both tiers before anything is sent. No auto-posting.

---

## Spec 9: Session structure: time slots, ordering, one-question opener

### What it does
Restructures the session around (1) an 8-minute slot per founder, (2) ordering by unresolved async issue, and (3) a one-question opener for each turn. Replaces ad-hoc airtime with a visible structure.

### Why now
- In the last session, one founder took a large share of the airtime, while the two heaviest reviewers got little. Reciprocity was broken.
- The group had committed to letting the heaviest reviewers go first this week. In a sync with the UX researcher we refined that: ordering by unresolved async issues lasts longer than pure reciprocity, because the group comes to solve the hardest problems, not to reward reviewers.
- Equal slots were the UX researcher's recommendation: the same structural airtime for everyone, used or yielded.

### How it works

**Per-founder turn (8 min):**
```
0:00–0:45  One question for the group (speaker)
0:45–2:00  Context (speaker points to their row in the pre-read)
2:00–7:00  Group responds to the question
7:00–8:00  Commitment captured (speaker names the next experiment)
```

**Ordering rule, written in the pre-read:** tonight's order is by unresolved async issue. The issues that got the least traction in peer review go first, while attention is freshest.

### Success criteria (KEEP if any)
- Airtime more balanced: no one takes more than 20% of the session outside their slot
- Each founder states their one question within the first minute
- Three or more founders reference the pre-read during their turn
- The session ends on time

### Kill criteria (KILL if any)
- Pushback on the cap ("this feels like a meeting, not a conversation")
- The ordering feels punitive for whoever goes last
- The opener creates awkwardness, and people default to status updates

### Assumptions being tested
1. Eight minutes feels like fair airtime, not a speed limit.
2. "Unresolved async issue" is clear to participants without a long explanation.
3. The one-question opener compresses context into a useful ask, not a performance.
4. Facilitators keep time softly. This is about predictable rhythm, not hard cutoffs.

---

## Spec 10: Template prompt for stuck metrics

### What it does
Adds one callout to the Problems section of the report, prompting founders to turn a stuck outcome into a controllable action when a key result hasn't moved for two weeks.

### Why it's a light touch
In the last session the cohort coached me in real time to reframe "5 customer conversations" (an outcome) as "20 outreach attempts" (an action). It was the session's most useful coaching moment. A template line can prompt the same reframe without waiting for the moment.

### How it works

```
Problems
- [What's blocking me]
- [What I need from the group]

⚠️ STUCK METRIC GUT CHECK ⚠️
If any key result has been at 0 for 2+ weeks, ask yourself:
- Is this metric an outcome or an action?
- What's the smallest controllable action you could measure instead?

If you can't answer on your own, add it to "What I need from the group" as an explicit ask.
```

**Two roles.** It's a template line for the founder, and a signal on the facilitator brief: if a key result is stuck and the founder didn't flag it, it shows up as an outcome-vs-action red flag.

### Success criteria (KEEP if any)
- At least one founder reframes a stuck metric with the prompt by the eighth session
- A peer comment references a reframe
- Someone mentions the prompt in the session

### Kill criteria (KILL if any)
- No visible uptake after three weeks
- The prompt feels preachy or over-engineered

---

## ~~Spec 11: Nudge decay, a natural experiment~~ (dropped April 20)

I dropped the plan to skip a week's nudges and see whether peer review held. The nudges stay as standing infrastructure. We gave up the chance to learn whether the behavior had become a habit, in exchange for less risk to the next session and a smaller build.

---

## Decisions locked April 20

The UX researcher left comments on the specs; the other two reviewers didn't respond by Monday. I decided with the UX researcher's input.

| # | Spec | Decision |
|---|------|----------|
| 1 | 8 | The facilitator brief carries both what participants asked for and what the system flags: key results stuck 2+ weeks, missed commitments, outcome-vs-action patterns, non-submission |
| 2 | All | Every remaining spec faces the cohort, so a kill is discussed with the group first. Spec 11 was dropped separately |
| 3 | 8 | Facilitators receive both the peer pre-read and the brief (the brief by DM only) |
| 4 | 9 | Session shape: 10 min open, 5 × 8-min peer coaching, 5 min flex buffer, 5 min close. 60 total |
| 5 | 10 | Self, then group: the founder answers the prompt first and, if they can't, adds it to "What I need from the group", with a visual callout so it isn't skipped |
| 6 | 10 + 8 | The prompt also surfaces on the brief when a key result is stuck and the founder didn't flag it |

**Spec 8 became a real expansion, not a tweak.** The brief now does two jobs: the asks participants make, and the flags the system raises.

### What the UX researcher's comments changed
- Paraphrase problems with build-stage context, for example that these founders need to talk to customers and are stuck on one part of it, instead of quoting them.
- The facilitator brief is a DM, not a shared channel. The agenda already shows what the facilitator learned; the dashboard shouldn't surprise anyone or become a scorecard.
- An hour with six 10-minute turns left no room. Turns became 8 minutes, with a buffer.
- The brief should flag things the founder didn't ask about, not only what they asked for.
- Kills on cohort-facing features get a conversation with the group, not just a behavioral threshold.
