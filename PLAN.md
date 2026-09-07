# ROOF — Shingle re-roof build plan

**Goal:** the most visual working model of a Treasure Coast shingle re-roof that still tells the truth — and that a new hire can *play* until the order is in his hands.

Not eight cards in a row. A **Periodic Table of Roof Parts** on the left (every item, sorted by the question it answers and the inspection it has to pass), a **living roof** in the middle that you build by dragging parts onto it, and an **inspector** who lifts a tab. Order is not a line. It is a set of gates with work between them, and the roof looks identical from the street whether you did it right or not.

This is the plan for app 1 (shingle). Tile, metal, and low-slope reuse the same shell.

Sister projects, same DNA:

- **BODY** — dark stage, honest imaging, evidence grades, drag food onto the mouth. We take the shell, the grades, and the "plain film" idea.
- **Periodic Table of Frameworks** (RULEROFWISDOM `/forum`) — white paper, family gradients, black ink, `z` in the corner, gaps allowed, complements, *data not code paths*. We take the tray.
- **/play Roof Raiser** (COVENANT) — the verified county order, the leak lines, the PASS stamps. We take the facts and outgrow the format.

---

## 1. What "accurate" means here

Three views of the same roof. The user can switch instantly.

| Mode | What it shows | What it must not fake |
|---|---|---|
| **Cutaway** | The roof as a stack, peeled back band by band: deck → nails → underlayment → metal → cover. Every layer you placed is visible. | A roof that is one flat color per step. A layer that appears with no thickness under it. |
| **From the street** | What the homeowner and the adjuster see: shingles, drip edge, cap, a vent. Everything that keeps water out is invisible. | A "finished" glow. A four-nail roof and a six-nail roof **look identical** from the street — the view says so. |
| **Inspector** | Only what the current gate checks, lit. Everything else dimmed. The tab lifted. The tape in frame. | Inspecting things the inspector cannot see anymore (step flashing after the shingles are on). |

The killer honesty: **a wrong roof looks like a right roof.** The only people who ever know are the inspector who lifted the tab, and the homeowner three storms later. That is why the game refuses to let you cover anything before its gate.

Sources: Indian River County / City of Vero Beach *Roofing Inspection Guide* (the five gates and what is checked at each); FBC 8th Edition (2023) Residential R905.2 and Existing Building Table 706.7.1.2; F.S. 553.844; Florida Product Approvals / NOAs for the actual products.

---

## 2. Product: one HTML app

Single page, no login, GitHub Pages, like BODY.

```
index.html                    ← series hub (shingle live; tile / metal / low-slope "soon")
apps/shingle/index.html       ← the app (MVP is one self-contained file)
apps/shingle/js/
  table.js                    ← the periodic table tray (families, rows, seats, peek)
  scene.js                    ← the roof SVG: layers, clip bands, three views
  engine.js                   ← partial order, gates, traps, leaks, score
  ui.js
data/parts.json               ← the catalog. Adding a part is a new object, never a new route.
data/gates.json               ← the five inspections and what each one checks
docs/sources.md               ← every claim, graded
```

Rule carried over from `frameworks.ts`: **if you write `if (part.id === 'shingles')` the engine is dead.** Hue lives on the family. Order lives on `needs`. What a gate checks lives on the gate.

---

## 3. Visual architecture

### 3.0 One model, two views (decided 6 Sep)

The periodic table is the **data model** — families, rows, seats, `needs`. It is not what the crew sees first. The **playing view is a dial**: all 24 tiles on one ellipse around the roof, clockwise by `z` from 12 o'clock, the five gate rows drawn as arcs of the ring (grey → gold when open → green PASS → red FAIL). You drag to the middle. **Everything fits on one screen with no scrolling** at 1440, 1024 and a phone. Tiles that are ready right now wear a gold ring — that is the partial order made visible without a list. The card is a peek anchored to the tile, opening toward the center. The table itself is one click away ("The table") as a read-only chart, because the grammar below is still how parts get added.

### 3.1 The table (the data) — the tray is a periodic table

White paper on the dark stage. Same grammar as the Frameworks table:

- **Column = family = the question the part answers.** Hue is data on the family.
- **Row = period = the inspection it must pass.** Reading down the table *is* the job.
- **Seat.** Two parts in one family at one gate stack under each other; the row gets taller, other columns leave a hole. Coordinates do not move.
- **`z`** in the corner = the order you can first place it. Gaps are allowed and will be filled by tile, metal, and low-slope parts later — Mendeleev left holes on purpose.
- **Gutters** between blocks: Paper | the Field (Deck, Water) | the Details (Edge, Wall, Hole) | what Shows (Cover, Seal).
- **Complements.** Peel-and-stick and two-ply felt sit as a pair: *the other way to do the same job.* Place one and the other greys out as "already covered".
- **Traps.** A tile that looks exactly like a real one and is accepted by the roof. *Four-nail shingles.* You find out at the gate. The trap gets a ✗ Cartoon grade only after it burns you.
- **Gate tiles** live in the Paper column. They are placed like any other part — because calling the inspection *is* a step, and calling it early or late is the most expensive mistake on the job.

Tile: family gradient (`hue → hueTo`, poster fill), hairline border, black ink, `z` top-left, 26 px serif symbol, 9 px name. Spent tiles go to paper-grey with a check. Hover / tap = peek card (law, spec, grade). Drag = place.

| Family | Symbol | The question | Hue |
|---|---|---|---|
| Paper | Pp | Is it legal, and who signed? | manila `#efe6cf → #d7c79b` |
| Deck | Dk | Will it hold in wind? | plywood `#e6bf8f → #c48f57` |
| Water | Wt | What if the cover fails? | membrane `#9db3c6 → #5f7e9a` |
| Edge | Ed | Where does water leave the roof? | galvanized `#d5dbe2 → #99a5b3` |
| Wall | Wl | Where does the roof hit a wall? | stucco `#e2c9b8 → #bd9273` |
| Hole | Ho | What goes through the roof on purpose? | breath `#b9dcd2 → #6fb8a6` |
| Cover | Cv | What faces the sun? | shingle `#b3a7a2 → #756360` |
| Seal | Sl | What closes the last gap? | mastic `#f0c79f → #d8925a` |

| Row (gate) | Label | What the inspector must see |
|---|---|---|
| 1 | Sheathing | The nails. Bare deck, 8d ring-shank at 6 in. |
| 2 | Dry-in | A roof that survives tonight's rain with nothing on top. |
| 3 | Flashing | Metal at every hole and joint — still visible. |
| 4 | In-progress | Two squares on, in the corner. The tab lifted. |
| 5 | Final | Vents, penetrations, drainage, kick-outs, a clean yard. |

### 3.2 The roof (center) — a living stack, not a coloring page

One gable slope in three-quarter view, eave at the bottom, ridge at the top, with the three things that leak: a **valley** (a wing roof meets it on the left), a **plumbing vent** mid-slope, and a **chimney / sidewall** upper right. The old roof is on it when you arrive: curled tabs and one soft sheet of plywood.

Each placed part draws a real layer:

| Part | What appears |
|---|---|
| Tear-off | Old shingles slide off. Bare plywood, one dark soft sheet. |
| Replace soft wood | The dark sheet becomes new wood. Seams land on rafters. |
| Re-nail | Nail heads march down every rafter line at 6 in. |
| Drip edge | A bright L along the eave and rakes, hemmed lip below the fascia. |
| Peel-and-stick / two-ply felt | Slate membrane in courses with rolled laps — or black felt with cap-nail dots. |
| Cement the flange | An amber bead along the eave over the flange. |
| Boot / valley metal / step / counter / kick-out | Metal, each in its true place, each still visible. |
| Starter, shingles | Starter strip, then courses of tabs climbing from the eave — Zone 3 corner marked. |
| Ridge vent, cap, sealant | A raised dark band, cap tabs over it, amber dots on every exposed head. |

**Cutaway** clips each layer to a band so the stack stays readable: deck full, underlayment from ~30 % across, cover from ~55 %. **Street** removes the clips. **Inspector** dims everything except the parts the open gate checks.

Wrong drop = a **leak**: a blue drip runs from the spot, the tile shakes back to the table, the card says *why* in the inspector's words. Score = leaks + failed gates. Three stars at zero.

### 3.3 The card (right) — the lab

Same as BODY's booth. For the selected or last-placed part:

- Symbol, name, family · gate
- **Law** — one sentence. The thing to remember on the ladder.
- **Spec** — the numbers: nail, spacing, lap, gauge, code section.
- **Fails when** — the inspector's reason, in his words.
- **Grade + source** — ✓ / ~ / ⚠ / ◈ / ✗, link to the county guide or code section.

Gate tiles show the checklist instead of a spec, and the stamp: PASS in green, FAIL in red with the item that failed.

---

## 4. The engine

A partial order, five gates, traps.

```
parts[]     {id, z, sym, name, fam, row, needs[], altOf?, trap?, layer, law, spec, fail, grade, src}
gates[]     {id, row, checks[], failsIf[]}
state       placed:Set, open gate, leaks, fails, view
```

- A part can be placed when every id in `needs` is placed (an `a|b` entry means either).
- Placing a part whose needs are not met is a **leak**. It does not land.
- A **gate** is a part. Placing it runs `checks` (all present) and `failsIf` (a trap present). PASS stamps and opens the next row. FAIL stamps, removes the trap layer, sends the trap tile back with a ✗, and stays open.
- `altOf` pairs complements: placing one satisfies any `a|b` need and greys the other.
- Rows are not locked as a whole — real crews run parallel. Drip edge and underlayment can go on in either order; the gate is what is strict.

Critical truths cartoons get wrong, and we will not:

1. **Order is a partial order, not a line.** ✗ cartoon: eight cards, one sequence. Real: boots, valley metal, and step flashing all happen between dry-in and the flashing inspection, in whatever order the roof dictates.
2. **The gate is the step.** Calling the inspection is on the table as a tile. Skip it and the roof will not accept the next layer — because in life the inspector makes you tear it back.
3. **Right and wrong look the same.** The trap tile lands. Street view shows a finished roof. The gate is the only truth.
4. **The county's order, not ours.** Sheathing → dry-in → flashing → in-progress → final, as the Indian River County guide lists them. Where practice varies (drip-edge/underlayment sequence, closed-cut vs metal valley) the grade says ~ and the card says *confirm with the inspector*.

---

## 5. The catalog — 24 parts (MVP)

`z` = first possible placement. Gates in bold.

| z | Sym | Part | Fam | Gate | Needs | Grade |
|---|---|---|---|---|---|---|
| 1 | Pm | Pull the permit | Pp | 1 | — | ✓ |
| 2 | To | Tear off to bare deck | Dk | 1 | Pm | ✓ |
| 3 | Rw | Replace soft wood | Dk | 1 | To | ~ |
| 4 | Rn | Re-nail the deck, 8d ring-shank 6 in. o.c. | Dk | 1 | Rw | ✓ |
| 5 | **I1** | **Sheathing inspection / affidavit** | Pp | 1 | Rn | ✓ |
| 6 | De | Drip edge at eaves and rakes | Ed | 2 | I1 | ✓ |
| 7 | Ps | Peel-and-stick, full deck (ASTM D1970) | Wt | 2 | I1 | ✓ |
| 7 | Fl | Two-ply felt, taped seams (alt of Ps) | Wt | 2 | I1 | ✓ |
| 8 | Rc | Cement the drip flange, 4 in. | Sl | 2 | De, Ps\|Fl | ~ |
| 9 | **I2** | **Dry-in inspection** | Pp | 2 | De, Ps\|Fl, Rc | ✓ |
| 10 | Pb | Boot every pipe | Ho | 3 | I2 | ✓ |
| 10 | Vm | Valley metal | Ed | 3 | I2 | ~ |
| 10 | Sf | Step flashing at the wall | Wl | 3 | I2 | ✓ |
| 11 | Cf | Counter flashing | Wl | 3 | Sf | ✓ |
| 11 | Ko | Kick-out at the bottom | Wl | 3 | Sf | ✓ |
| 12 | **I3** | **Flashing inspection** | Pp | 3 | Pb, Vm, Sf, Cf, Ko | ✓ |
| 13 | St | Starter strip | Cv | 4 | I3 | ✓ |
| 14 | Sh | Field shingles, 6 nails | Cv | 4 | St | ✓ |
| 14 | S4 | Field shingles, 4 nails — **trap** | Cv | 4 | St | ✗ |
| 15 | **I4** | **In-progress inspection** (fails if S4) | Pp | 4 | Sh | ✓ |
| 16 | Rv | Ridge vent | Ho | 5 | I4 | ✓ |
| 17 | Hr | Hip and ridge cap | Cv | 5 | Rv | ✓ |
| 18 | Sv | Seal every exposed nail | Sl | 5 | Hr | ✓ |
| 19 | **Fn** | **Final inspection** | Pp | 5 | Sv | ✓ |

Specs on the cards (all from the county guide unless marked):

- Re-nail: 8d ring-shank, 6 in. o.c. along every rafter/truss, field and edge — FBC Existing Building 8th ed. Table 706.7.1.2; F.S. 553.844. ✓
- Sheathing affidavit: licensed contractor only; an owner-builder cannot sign it. ✓
- Underlayment System #1: self-adhering polymer-modified bitumen, ASTM D1970, slopes over 2:12. System #2: two layers ASTM D226 Type II / D4869 Type III–IV / D8257, half-width starter, full sheets lapped half a sheet + 2 in. System #3 (3¾ in. self-adhered strips over deck joints) is slopes over 4:12 only. ✓
- Drip edge: min 3 in. lap, ½ in. below the sheathing, min 2 in. back on the roof, fastened max 4 in. o.c.; where installed over the underlayment, min 4 in. width of roof cement over the flange. ✓ (sequence ~ — see §7)
- In-progress: min 2 squares / 200 sq ft in Zone 3; 6 nails per shingle or per the NOA / Florida Product Approval. ✓
- Final: penetrations, vents, drainage, valleys, sidewall flashing, kick-outs, plumbing vent heights — ladder and mirror. ✓

---

## 6. Evidence grades

| Grade | Meaning |
|---|---|
| ✓ **Robust** | In the county guide or the code table. Build the game on it. |
| ~ **Range** | Real, but practice varies by product approval or inspector. Card says *confirm*. |
| ⚠ **Contested** | Roofers argue about it. Show both. |
| ◈ **Model** | Simplification for the sim (one slope, one pipe, one wall). |
| ✗ **Cartoon** | Common lie. The trap tiles. We let you place it, then the gate refuses it. |

---

## 7. Open decisions (Josias)

1. **Drip edge before or after the underlayment at the eave?** The county guide's wording is *drip edge over the underlayment with 4 in. of roof cement on the flange*. /play has drip edge first. Both are on Treasure Coast roofs. The MVP accepts either order and grades the cement step ~. **Pick one for the crew standard and the card will say it flat.**
2. **Valley: open metal or closed-cut over self-adhered?** MVP teaches open metal (harder to get wrong). If the crew standard is closed-cut, Vm becomes the alt of a new "Vc" tile — one object, no code.
3. **Zone 3 corner** — which corner the inspector wants the first two squares in changes with the wind map. MVP marks the lower-left corner ◈.
4. **Second trap** for V1.1: *one layer of 15# felt, stapled* (the 1995 dry-in). Cheap to add — it is a data row.

---

## 8. Series

1. **Shingle** — this plan. MVP first.
2. Tile — foam-set vs screw-set, battens, the weight question.
3. Metal — 5V vs standing seam, exposed fasteners, the in-progress waiver.
4. Low-slope — modified bitumen / TPO, the condo funnel.
5. Roof-to-wall — straps and clips (My Safe Florida Home crossover).

Later: email gate → CRM lead (storm-quiz pattern); a **manager mode** that plays back a rep's run with leak count; Spanish tiles (the card strings are data).

---

*Plan written 2026-09-06. County facts from the Indian River County / City of Vero Beach Roofing Inspection Guide; code references FBC 8th Edition (2023). A training model, not a permit.*
