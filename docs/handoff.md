# Sailboat Profile — Build Handoff

**Leadership Failure Simulation · Engineering handoff**

## How the sailboat profile is built — and how to make it real.

This is the reference for the shipped demo at **demo.belegendary.org**: a
twelve-run leadership profile whose face is an interactive sailboat, backed by a
live, appreciative, evidence-bound coach. Everything below traces to the actual
code in `lpmoon007/lfs-demo`. The last two sections — [Make it real](#08--making-it-a-real-per-leader-product)
and [Deploy](#09--deploy--verify) — are what the LFS product team needs to turn
this from one fictional participant into a live per-leader product.

| | |
|---|---|
| Repo | `lpmoon007/lfs-demo` |
| Branch | `main` (merged) |
| Live | demo.belegendary.org |
| Stack | static HTML + one Vercel function |
| Coach model | `claude-sonnet-4-5` |

> An interactive HTML version of this handoff is also published as an artifact —
> ask the product owner for the link.

---

## 01 · What shipped

One self-contained page (`index.html`) plus one serverless coach endpoint
(`api/coach.js`). The participant of record is **Dana Whitmore**, a fictional
leader with a twelve-run history over fourteen months. Reading the profile
top-down:

| Component | Status | What it is |
|---|---|---|
| The sailboat | Shipped | The story-lens face. Six markers mapped to boat parts; tap any part for its trace, the leak, or the coach. |
| Twelve-run timeline | Shipped | Two markers climbing while the confirmation lag holds flat at 1.8 — the invariant, "twelve times." |
| Six-marker radar | Shipped | The fingerprint as a hexagon, Run 01 vs Run 12, in the numbers card. |
| The live coach | Shipped | A grounded model that cites the record, refuses the unevidenced, argues, and now coaches from strength. |
| Plain ↔ Insider | Shipped | A label toggle: barrier-free words for newcomers, insider vocabulary (sails / leak / helm) for adopters. |
| Practice → rep loop | Shipped | The leak routes to the recommended run (Handover) and the 30-day rep. |

> **The one-line summary for a busy reader.** The design is done and coherent;
> the **data is placeholder**. To productise, the real system feeds each
> leader's own measured runs into the same structures. Nothing here needs
> re-architecting — it needs real data and original artwork.

---

## 02 · Architecture & philosophy

The product sits on a four-part spine that holds true at every scale:

| Part | Role |
|---|---|
| **Be Legendary** | The destination — who the leader is becoming. |
| **Better Every Day** | The daily path — the felt promise that today beat yesterday. |
| **The Simulation** | The mirror — what the leader actually did under pressure, logged and scored. |
| **The Coach** | The relationship — where the leader makes sense of it. The most important part. |

The operating philosophy is **Appreciative Inquiry**: lead with strengths, do
more of what works, and treat the one low marker as a growth edge — a cable to
tension, not a flaw to fix. This is a deliberate reversal of the deficit framing
the name ("Failure Simulation") uses as a hook. Crucially, appreciation never
loosens the evidence — see [the coach contract](#06--the-coach-contract).

> **Naming, decided.** Keep **Leadership Failure Simulation** as the edgy
> top-of-funnel name for now; **Better Every Day** remains the felt promise
> underneath. The rename to bettereveryday.pro is parked, not dropped.

---

## 03 · The measurement model

The instrument is **twelve markers in two tiers**. Only **Tier A** (six
individual-decision markers, scored every run) is used in this demo; **Tier B**
(six teaming markers, team mode only) is on the shelf for the team product. The
six Tier A markers, their current values, and how each maps onto the boat:

| Marker (Tier A) | R01 | R12 | Δ | Boat part | Plain / Insider |
|---|--:|--:|--:|---|---|
| **Consultation breadth** | 86 | 88 | +2 | Fleet | People / Other boats |
| **Composure under escalation** | 81 | 81 | 0 | Compass | Your read / Compass |
| **Decision calibration** | 68 | 71 | +3 | Jib | Strength / Sail |
| **Truth-seeking over comfort** | 59 | 68 | +9 | Mainsail | Strength / Sail |
| **Intent–action integrity** | 51 | 52 | +1 | Helm | Follow-through / Helm |
| **Information-seeking** | 36 | 44 | +8 | Leak | Growth edge / Leak |

Two structural rules the product depends on:

- **The lowest marker is the leak.** Information-seeking (44) is the growth edge
  and the narrative pivot — "you reach everyone and stop at the first answer."
  Truth-seeking (+9) is the trace hero because it moved most, via a targeted rep.
- **Three number systems, never conflated** — marker rates (the six,
  difficulty-normalised, used for every longitudinal claim), run score (a
  weighted composite per run), and raw in-scenario scores (never compared across
  runs). The coach is instructed to refuse anyone who stacks raw scores across
  runs.

Each marker also carries a confidence tier (provisional / moderate / high) that
rises only when it survives a *new* condition, and the whole profile passes a
**grounding gate**: every generated line traces to the record or is withheld.

---

## 04 · The data model *(placeholder)*

The profile is twelve runs over fourteen months. **Four carry full event-level
transcripts; eight are recorded at summary level.** This 4-deep / 8-summary
split is a demo artifact — in the real product every run has a real log.
Ordering and the four real runs' positions matter, because every finding
references them by number.

| # | Run | Date | Condition | Score | Lag | Transcript |
|--:|---|---|---|--:|--:|---|
| 01 | **Ridgeline** | Jun 2025 | forthcoming | 51 | 1.8 | Full |
| 02 | Longwater | Jul 2025 | forthcoming | 53 | 1.8 | Summary |
| 03 | Fenland | Sep 2025 | guarded | 50 | 1.9 | Summary |
| 04 | **Sennar Ascent** | Oct 2025 | guarded | 48 | 1.8 | Full |
| 05 | Halyard | Nov 2025 | forthcoming | 54 | 1.8 | Summary |
| 06 | Cinder | Jan 2026 | guarded | 52 | 1.9 | Summary |
| 07 | **Blackout** | Feb 2026 | guarded | 55 | 1.9 | Full |
| 08 | Meridian | Mar 2026 | forthcoming | 58 | 1.8 | Summary |
| 09 | Drawdown | Apr 2026 | guarded | 60 | 1.8 | Summary |
| 10 | Keel | May 2026 | forthcoming | 61 | 1.8 | Summary |
| 11 | Tallgrass | Jun 2026 | guarded | 62 | 1.8 | Summary |
| 12 | **Overdrive** | Jul 2026 | forthcoming | 63 | 1.8 | Full |

The narrative these numbers carry (all authored, all consistent): **reaches
people, stops at the first answer**; a **1.8-day confirmation lag that never
moves** (the invariant, twelve times, variance 0.05); **softens only with people
her own decisions have cost** (conscience, not avoidance); and a **truth-seeking
rep that moved the number**. Total logged events: **2,411**.

---

## 05 · Component specs

### The sailboat & its doorways *(shipped)*

A hand-authored inline SVG at the top of the overview pane. Each marker becomes a
boat part (table above); sail fill height encodes the marker value; the lowest
marker is the ochre leak, which pulses until first interaction. Tapping any part
opens a detail panel:

- **Sail (a strength):** "how you built it" — the trace — with the run it moved
  in and the cited event, then "do more of this." Buttons: **Ask the coach**,
  **Read the moment**.
- **Leak (the growth edge):** why it's low, the fix, the suggested rep. Buttons:
  **Ask the coach**, **Practice it in Handover**, **Your 30-day rep**.
- **Lighthouse:** the coach — three grounded opening questions.

> **Artwork is placeholder — and there's a licensing note.** The SVG boat is a
> stand-in. The sailboat metaphor is adapted from Alberts, H.J.E.M. (2016), *The
> Sailboat* (positivepsychology.com) — fine to use as a coaching framework
> **with attribution**, but commission **original artwork** before productising,
> and confirm a commercial-use license if the metaphor becomes a core product
> feature at scale.

### Twelve-run timeline & six-marker radar *(shipped)*

Both are self-contained, namespaced SVG modules using the page's own CSS
variables. The timeline plots two climbing markers over the flat lag lane with
challenge flags; the radar draws Run 01 vs Run 12 hexagons with the leak corner
dented. Both read the same twelve-run dataset described above.

> **Interaction contract — how the boat wires into the page.** The boat calls
> three globals the page exposes, so the real product only needs to keep these
> stable:
>
> - `window.LFSask(question)` — sends a question to the live coach and opens the rail.
> - `window.gpOpen(runId)` — opens a run transcript (`r1`–`r4` = the four deep runs).
> - `window.LFSshow(paneId)` — navigates to a section (used for the rep + Handover routes).

---

## 06 · The coach contract *(shipped)*

The coach lives entirely in `api/coach.js`, split into two strings:

| String | Role |
|---|---|
| `CASE_FILE` | The closed-world record: the twelve runs, six markers, four findings, key events, the gap, the rep ledger, and how each finding is measured. If a fact isn't here, the coach must refuse. This is the whole credibility argument. |
| `SYSTEM` | Behaviour: ground everything, refuse rather than invent, argue back, handle the meta — plus the appreciative additions below. |

Three rules the real product must preserve when it swaps in a real leader's
record:

- **The grounding gate is the product.** "A visitor trying to catch you out
  should fail — and should notice you declined." Never invent a figure, quote,
  event, date, or person.
- **Coach from strength (the appreciative layer).** Lead with what's working;
  frame the low marker as the highest-leverage next move, not a deficit. When it
  helps, put the **2Q** to the leader — *"What are you creating? What are you
  allowing?"* — and let it sit. This never overrides the grounding gate: a
  strength must trace to the record exactly like a gap.
- **The summary-run rule.** The case file tells the coach that only four runs
  have transcripts; for the other eight it must say so plainly and answer only
  from the one-line summary — **never fabricate event detail.** This is how the
  4-deep / 8-summary demo stays honest.

> **Known inconsistency this handoff resolved — don't reintroduce it.** The repo
> previously had a half-finished marker rename (fingerprint used the new six;
> verdict, ledger and coach still said "candor / prudence / care for people,"
> with numbers that contradicted). It's now fully aligned to the six Tier A
> markers. If you edit marker names or values, change them in **both**
> `index.html` and `api/coach.js`, and re-check for stragglers.

---

## 07 · File map

Everything is grep-able by comment markers and class prefixes:

| Where | What | Find it by |
|---|---|---|
| `index.html` | The whole profile page — self-contained styles + scripts, no build step | — |
| ↳ boat | Sailboat SVG, panels, Plain/Insider, wiring | `SAILBOAT DOORWAY` · `.bt-*` |
| ↳ timeline | Twelve-run timeline module | `TWELVE-RUN TIMELINE` · `.tl-*` |
| ↳ radar | Six-marker hexagon | `SIX-MARKER RADAR` · `.rd-*` |
| ↳ run log | Twelve rows; four clickable, eight "log only" | `class="rlr"` |
| ↳ fallback KB | Authored answers for demo-mode (no backend) | `const KB` / `match(` |
| ↳ transcripts | The four deep run transcripts | `const GP_RUNS` |
| `api/coach.js` | Live coach endpoint — `CASE_FILE` + `SYSTEM` | — |
| `vercel.json` | Function config (timeout, no-cache on /api) | — |

Design provenance (the reasoning behind these choices) lives in the working
artifacts: the two-lens comparison, the boat-as-doorway prototype, the Now /
Next / Shelf scope board, and the phased build order. Ask the product owner for
those links.

---

## 08 · Making it a real per-leader product *(to build)*

This is the core of the handoff. The demo hardcodes one fictional leader; the
real LFS system already produces per-leader event logs, markers and a
memory-backed coach. To reflect this demo, each hardcoded piece becomes generated
per participant:

| Demo (hardcoded) | Real product (generated per leader) |
|---|---|
| Six marker values + deltas | From the scoring engine's marker rates for this participant |
| Boat encoding (sail fills, which part is the leak) | Computed from those rates; **leak = lowest marker**, mainsail = biggest mover |
| Twelve-run timeline dataset | The participant's real run history (any N, not fixed at 12) |
| Traces ("how you built it") | Generated from run-over-run rate deltas + the run where it moved + a cited event |
| `CASE_FILE` as a static string | The participant's real event log — the behavioural memory layer the live coach already has |
| 4-deep / 8-summary transcripts | All runs have real logs; drop the summary distinction and its case-file rule |
| Placeholder SVG boat | Commissioned original artwork, driven by the same value→fill encoding |

What carries over unchanged: the four-part architecture, the appreciative coach
stance + 2Q, the grounding gate, the Plain/Insider toggle, the marker→boat
mapping, and the interaction contract (`LFSask` / `gpOpen` / `LFSshow`).

> **Where the beta actually starts.** Per the scope decisions, the beta opens in
> a **ready profile** — no intake form. The role + "what do you want to get
> better at" intake, the CQ commitment lens, transcripts-as-source-files, Friday
> wins, badges, and the whole Tier-B team side (the fleet + LDOL) are all marked
> **Next / Shelf**, not Now.

---

## 09 · Deploy & verify

Static page + one function, deployed to Vercel from `main` as its own project →
**demo.belegendary.org**. Framework preset **Other**; build command empty; no
dependencies (the function uses Node's built-in `fetch`).

| Env var | Notes |
|---|---|
| `ANTHROPIC_API_KEY` | Required. Use a key dedicated to this project. Env vars bake in at deploy time — **redeploy after changing it**, or the coach stays in demo mode. |
| `LFS_MODEL` | Optional, default `claude-sonnet-4-5`. |
| `LFS_MAX_TURNS` | Optional, default 14. |

**Verify after any deploy:** open the page and check the coach badge reads
**live**, not "demo mode" (that confirms the key + function work). Then try to
catch it out — ask *"how did I get truth-seeking to 68?"* (should cite Overdrive
and the rep) and *"open the Meridian transcript"* (should decline — Meridian is a
summary run). If both behave, the case file is sound.

> **Fallback safety net.** If `/api/coach` is ever unreachable, the page silently
> serves the authored fallback answers and flips the badge to "demo mode" — no
> broken panel in front of a prospect. That fallback KB is also synced to the
> twelve-run data.

---

*Sailboat Profile — build handoff · grounded in `lpmoon007/lfs-demo` @ `main`.
Placeholder demo, internally consistent end to end. Everything worth keeping is
committed and deployed.*
