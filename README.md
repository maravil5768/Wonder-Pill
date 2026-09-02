<h1 align="center">💊 Wonder Pill</h1>

<p align="center"><b>A Claude skill that refuses to give you the answer.</b></p>

<p align="center">
  <img alt="Agent Skill" src="https://img.shields.io/badge/Agent-Skill-7F77DD?style=flat-square">
  <img alt="Claude" src="https://img.shields.io/badge/Claude-compatible-D85A30?style=flat-square">
  <img alt="Interactive map" src="https://img.shields.io/badge/output-interactive%20mind%20map-1D9E75?style=flat-square">
  <img alt="No answers" src="https://img.shields.io/badge/answers-0-888780?style=flat-square">
  <img alt="License MIT" src="https://img.shields.io/badge/license-MIT-378ADD?style=flat-square">
</p>

<!--
  VIDEO: GitHub does not play videos from a repo path reliably.
  To get the real player: open this README in the GitHub web editor,
  delete the <video> block below, and drag assets/demo.mp4 into the editor.
  GitHub uploads it and leaves a https://github.com/user-attachments/assets/... URL
  that renders as an inline player. The block below is the fallback until then.
-->

<p align="center">
  <video src="assets/demo.mp4" poster="assets/demo-poster.png" controls muted loop width="820"></video>
</p>

<p align="center"><i>Panning around a Wonder Pill map — seeds, branches, dead ends, and the two places the thinking converged.</i></p>

---

Ask Claude for ideas and you get a list. Install Wonder Pill and you get a map of the questions you didn't know you were standing on — plus an interactive mind map you can drag around, showing where every thought came from and which ones got thrown away.

Not an answer. A different kind of side effect.

---

## Read this part first

**Wonder Pill does not generate good ideas. It is not supposed to.**

This matters enough to say plainly, because the failure mode of tools like this is someone installing it, reading the output, thinking "half of this is nonsense," and concluding it's broken. It isn't broken. Half of it being nonsense is the design.

What Wonder Pill produces is **raw material for your own thinking**. A stepping stool. Some of what comes out will be wild. Some of it will be impractical. Some of it will be, honestly, dumb — the kind of thing you'd be embarrassed to say out loud in a meeting. That's the cost of reaching past the obvious, and it's a cost worth paying, because the obvious answers are the ones you'd have found anyway without any tool at all.

Here's the reasoning. Language models are trained to predict likely continuations. Ask one for "ideas" and you get the statistically likeliest ones, which is another way of saying: **the ideas everyone else already got.** Every tool built on top of a model inherits that pull toward the center of the distribution. The only way out is to deliberately aim at the tails — and the tails contain both the genuinely novel and the genuinely stupid, because that's what "unlikely" means. You cannot filter for one without losing the other.

So Wonder Pill doesn't try. It generates loosely, marks how far each thread has drifted from reality, and hands you the whole spread. **You are the filter.** That's not a limitation being apologized for — it's the correct division of labor. You know your budget, your deadline, your skill level, your taste, and what would actually be interesting to *you*. The tool doesn't and can't.

A few honest expectations:

- **Roughly a third of any given map will be useless.** Expected. Look at it and move on.
- **A third will be interesting but not usable** — right shape, wrong context. Still valuable: it usually tells you something about the problem.
- **A third will be worth pulling on.** That's a good yield for something that took thirty seconds.
- **The most useful output is often not a what-if at all** but a *gut-check line* — the note about where the real difficulty hides. Several times in testing, that line reframed what a project actually was. Watch for those.
- **If everything on the map seems sensible, something went wrong.** That means it collapsed back toward the consensus answers, which is the exact thing this exists to escape.

Judge it by whether it got you thinking somewhere you wouldn't have gone. Not by whether every branch was correct.

---

## The problem it solves

Ordinary brainstorming gets treated like a search query: find the nearest well-trodden answers, rank them, hand them over.

```
> give me science fair ideas

1. Build a solar oven
2. Test which paper towel is most absorbent
3. Grow plants under different colored lights
...
```

Three things just went wrong:

1. **You became the chooser, not the thinker.** Your job is now to evaluate someone else's list — which is a much smaller job than the one you actually wanted.
2. **You got anchored.** Everything you think next is a variation on "solar oven." The first answer eats the space.
3. **It never left the training distribution.** Those *are* the likeliest answers. That's not a bug in the model, it's what the model is for — which is precisely why you need something pushing the other direction.

Wonder Pill attacks all three by changing the deliverable. Instead of ideas, you get **provocations to think with.**

---

## What it actually does

```
> give me science fair ideas

seed: nobody grades a project that isn't finished
   ↓
assumes: a project has to be finished to be judged
→ what if the project were a thing still running — measurements
  arriving during the judging, no known result yet?
   ├─ and the judges watched it change while they stood there
   ├─ and "the result" was whatever it happened to be at 2:47pm
   └─ and you genuinely didn't know if it would work
        └─ so what does a poster board even show?
  gut-check: only interesting if the hard part is the
  unfinishedness, not the topic

scrapped: what if it ran for a year?
  derivation: inverts the deadline
  flaw: the deadline is a hard wall, not a thing you can invert
  judgment: scrapped for generativity — there's nowhere for
  the thread to go once you're standing in "no deadline"
```

Every what-if is **derived by inverting a named assumption** — never invented freely. That single constraint is the whole trick, and the reason the output isn't the usual vague "what if you thought bigger?" filler.

### The three-part deliverable

| Part | What it is |
|---|---|
| 🗺️ **Interactive mind map** | Drag to pan, zoom, click any node for its gut-check. Every node states itself in plain language, so the map reads on a first pass without clicking. Fully expanded, nothing hidden behind a reveal. Shows seeds, dead ends, cross-links, and uneven depth. |
| 📝 **Orientation paragraph** | Names the *throughlines* — which tension kept recurring, where it went feral. Not a summary of the nodes. |
| 🌱 **Written wonderings** | `Premise → What if → tendrils → gut-check`, for reading instead of scanning. |

And then it **stops.** No ranking, no "here's my favorite," no quiet convergence back into a recommendation. If you want to land on one, you say so — and then it re-runs the whole audit on just that branch.

---

## What's on the map

The map is deliberately *not* a tidy tree radiating evenly from a center. Real thinking isn't uniform, and a map that pretends otherwise throws away the most interesting information.

- **Seed nodes** sit *outside* the branch they caused, further from the center than their own consequence. This is where "why did it think that" lives — a real fact, a historical precedent, an oddity it found while looking around. The map reads inward as well as outward.
- **Uneven depth.** One branch gets a single hop because the thread ended there. Another goes four deep because it kept opening. A map where every branch is exactly three deep is a map that stopped thinking on a schedule rather than when it ran out of thread.
- **Scrapped what-ifs** float detached at the edges, struck through, showing *where it came from, what's wrong with it, and why that was judged disqualifying* — three separate fields, not one blended reason. Kills can only happen for being a genuine dead end, never for just sounding implausible or weird, so an idea that's out there but still generative survives. This is more useful than it sounds: it shows you a direction that's already been checked, and sometimes you'll disagree with the call and pick it back up. Dead ends are information.
- **Cross-links** connect branches that collided on the same underlying tension. A pure tree structurally cannot show convergence, and convergence is often the most interesting thing on the whole map — it usually means the real problem is one level up from where you were looking.
- **Grounded vs. feral** is marked by border style, not just position. Feral threads are kept deliberately. They're not failures of the process; they're the point of letting it run loose.

---

## Install

Download `wonder-pill.skill` from [Releases](../../releases) and click **Save skill** on the file card in Claude.

Or drop the folder into your skills directory:

```bash
git clone https://github.com/ara-mkr/Wonder-Pill.git
cp -r Wonder-Pill ~/.claude/skills/wonder-pill
```

---

## Usage

Call it directly:

```
/wonderpill fungi
wonder about tidal energy for a bit
```

It also triggers on its own when you clearly want to open a space rather than close one:

```
what are the weird angles on urban heat islands
help me think about what a community darkroom could be
I want to explore this, not decide yet
```

It stays out of the way when you want concrete output. A named deliverable, a count ("give me 5 names"), a deadline, or a "which should I pick" question gets a normal answer, not a wonder pill. When it genuinely can't tell, it asks one line first instead of branching.

### The three intake questions

It opens by asking three things, and that intake isn't ceremony — it's the one variable that governs everything:

1. **How far can it drift?** Pure wondering, or does something eventually have to get built?
2. **What's off-limits?** Budget, timeline, materials, audience — walls it shouldn't waste effort inverting.
3. **Should it go hunting?** Whether to look for a genuinely weird real fact to start from.

*"What if plants could hear"* is a great provocation for a curious kid and a useless one for someone submitting a materials list in three days. Same topic, different leash. Get the leash wrong and everything downstream is wasted.

Skip the questions by front-loading context yourself: *"two weeks, $30, has to fit on a poster board."*

### Getting more out of it

- **Give it a real constraint.** Counterintuitively, tight constraints produce better what-ifs than "go wild," because there's more structure to push against. "$30 and two weeks" generates sharper inversions than "no limits."
- **Pick a thread and go again.** The most valuable output is usually on the *second* pass, once a branch has become the new topic and its tendrils have become the assumptions to invert.
- **Read the gut-checks first.** They're the densest part. If you only read one thing per branch, read that.
- **Argue with the scrapped ones.** If you disagree with why something died, that disagreement is a real signal about what you actually care about.
- **Don't ask it to pick.** If you want a recommendation, ask for one explicitly. Left alone it won't converge, on purpose.

---

## How it works

<table>
<tr><td><b>0</b></td><td><b>Intake</b></td><td>Three questions, max. Calibrates the leash length.</td></tr>
<tr><td><b>1</b></td><td><b>Oddity hunt</b></td><td>One cheap pass for a genuinely weird fact. Fails fast, never repeats per-branch. Becomes a seed node.</td></tr>
<tr><td><b>2</b></td><td><b>Assumption audit</b></td><td>Surface 3–5 load-bearing assumptions. Invert each. <i>The inversion is the what-if.</i> Keep the provenance.</td></tr>
<tr><td><b>3</b></td><td><b>Tendrils</b></td><td>Each branch runs through scale / time / reversal / audience / material / sense / causality. Depth varies. Scraps get kept with where they came from, what's wrong with them, and why that was disqualifying — only a genuine dead end can kill one, never just sounding implausible.</td></tr>
<tr><td><b>4</b></td><td><b>Gut-check</b></td><td>One line per branch: where the real difficulty hides. Tag <code>grounded</code> or <code>feral</code>.</td></tr>
<tr><td><b>5</b></td><td><b>Render</b></td><td>Interactive map, then orientation, then written wonderings.</td></tr>
<tr><td><b>6</b></td><td><b>End open</b></td><td>An invitation, never a verdict.</td></tr>
</table>

---

## The one failure mode it's built to avoid

**"Generic wild"** — what-ifs that *sound* expansive but have no hook.

> ❌ What if plants were different?
> ✅ What if plants could hear, and had been responding to sound the whole time?

The first hands the work back and gives you nothing to push against. The second names a mechanism, so you can immediately feel what would have to change. Strong what-ifs are *specific*; weak ones merely negate.

This is why the derivation rule exists. If a what-if can't name the assumption it's pushing against, it isn't ready — and "sounds bold" is not the same as "is specific." Most bad brainstorming output fails exactly here: it reaches for scale ("what if it were huge?") when it should be reaching for mechanism.

---

## Honest limitations

- **No reality-testing loop.** It can't build a thing, watch it fail, and update. Every what-if is untested by construction, and it has no stake in whether any of them work.
- **It doesn't know what's been tried.** A branch may be a well-known dead end in your field. The scrapped nodes catch some of this; they won't catch domain-specific history.
- **Feral branches are genuinely often useless.** Kept on purpose. Skim them.
- **Quality depends heavily on the intake.** Bad leash calibration produces confidently irrelevant output. Front-load context.
- **The map gets dense fast.** Six branches with uneven depth is near the readability ceiling even with pan and zoom.
- **It won't tell you which idea is best.** Not modesty — that judgment needs your context, and faking it would undo the whole point.

---

## Repo layout

```
Wonder-Pill/
├── SKILL.md                  # the six stages + the specificity rules
├── README.md
├── wonder-pill.skill         # packaged, installable bundle
├── assets/
│   ├── demo.mp4              # the recording above
│   └── demo-poster.png
└── references/
    └── mindmap.md            # interactive map build spec — loaded at render time
```

`mindmap.md` is a separate file for two reasons. It's only needed at render time, so keeping it out of `SKILL.md` saves context on every other turn. And it's the part most likely to need fixing — it's written against the renderer's real constraints (no fixed positioning, CSS-variable-only colors, no color-alone encoding), which are stricter than they look and caused an actual failure during testing before being pinned down.

---

## When *not* to use it

- You need one decided answer, fast
- It's a factual lookup
- You've already chosen the plan and want it executed
- You want validation rather than provocation

Wonder Pill is for the part before all of that — the part where you don't yet know what question you're asking.

---

## License

MIT
