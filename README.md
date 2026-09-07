# ROOF

A series of **HTML apps** that show how a Treasure Coast roof actually goes on — every part on a periodic table, a roof you build by dragging parts onto it, and the county inspector who decides whether it counts.

Live:

- **Shingle** — [`apps/shingle/index.html`](apps/shingle/index.html) (`ROOF Shingle`, crew edition)

Training model, not a permit.

---

## The one-paragraph version

Most "how a roof is built" pictures are eight cards in a row. A real re-roof is a **partial order with five gates**: the county inspects the sheathing, the dry-in, the flashing, the first two squares, and the final — and nothing may cover what the inspector has not seen. Between the gates, the order is the roof's, not a list's. And the cruel part: a roof done wrong looks exactly like a roof done right from the street. The only truth is the inspector lifting a tab.

## Repo map

| File | What's in it |
|---|---|
| [`index.html`](index.html) | Series hub |
| [`apps/shingle/index.html`](apps/shingle/index.html) | **Live.** Table → drag → cutaway / street / inspector → five gates |
| [`PLAN.md`](PLAN.md) | Shingle build plan: what accurate means, the table grammar, the 24-part catalog, the engine, open decisions |

## Sister projects (same DNA)

- **BODY** — the dark stage, the honest-imaging toggle, the evidence grades.
- **Periodic Table of Frameworks** (RULEROFWISDOM `/forum`) — the tray: families, rows, seats, gaps, complements, *data not code paths*.
- **/play Roof Raiser** (COVENANT) — the verified county order this grew out of.

## Run ROOF Shingle

Open [`apps/shingle/index.html`](apps/shingle/index.html).

1. Drag **Pm — Pull the permit** onto the roof. Then try dragging shingles. Watch it leak.
2. Work down the table. Call each inspection when the row is done — the gates are tiles.
3. Toggle **From the street** after the shingles go on. Then read the hint.
4. There is one tile that lies. You will find it at the in-progress inspection.
5. Checks the engine must still pass:
   - Nothing lands before the permit.
   - Underlayment refuses to go on before the sheathing inspection.
   - Peel-and-stick and two-ply felt cover each other — you only do one.
   - Four-nail shingles land, then fail the in-progress gate and come off.
   - Cap refuses to go on before the ridge vent.

## Evidence grades

| Grade | Meaning |
|---|---|
| ✓ **Robust** | In the county guide or the code table. |
| ~ **Range** | Real, but practice varies by product approval or inspector. Confirm. |
| ⚠ **Contested** | Roofers argue about it. Both shown. |
| ◈ **Model** | Simplified for the sim. |
| ✗ **Cartoon** | The common lie. The trap tiles. |

*Shingle MVP: 2026-09-06 · Sources: Indian River County / City of Vero Beach Roofing Inspection Guide; FBC 8th Edition (2023).*
