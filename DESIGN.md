# Crunch Time: Design Doc

A side-view restaurant game inspired by the sushi bar in Dave the Diver, set in a 90s fast-food joint. One employee, one late-night shift, too many customers.

This doc is the single source of truth. If an idea isn't in **Core** or the current **Milestone**, it goes in the **Parking Lot**, not the code.

---

## Core loop (locked)

1. A customer arrives and places an order (example: 2 tacos, 1 burrito, 1 drink, 1 quesadilla).
2. The player walks between stations and grabs the items.
3. The player packs the items into that customer's **bag**.
4. The player hands the finished bag to the customer before their patience runs out.
5. Paid + tipped based on speed. Slow service makes customers angry. Three walkouts and they **call corporate**, and the shift ends.

The fun is in **routing and juggling**, not in any single action: which order to start, what to grab on the way, how to avoid walking back and forth.

## Pillars

- **Readable at a glance.** You always know who is about to blow and what they want.
- **Movement is the skill.** Walking efficiently is what separates a good shift from a bad one.
- **90s fast-food nostalgia.** Purple, teal, hot pink, Memphis confetti, pixel art. An original brand, no real logos.
- **Plays great on the AYN Thor.** Controller first, touch second.

## Decisions (locked 2026-11-03)

1. **Bags live at a central pick-up counter.** Kitchen stations sit on both sides of it. You walk out, pick items up, and walk back to drop them in. Each bag sits right under its customer in the pick-up window.
2. **Carry limit: 5 items.** This is a tuning knob (`T.HANDS`). If routing feels too easy, try 3 before changing anything else.
3. **Two kinds of station.** Grab stations hand you the item instantly. Machines (grill, fountain) need you to press start, then you walk away while they cook and come back to grab the item.
4. **Pick-up window only.** No drive-thru until the core loop is proven.
5. **A wrong item in a bag is a penalty.** The item is wasted, you lose $1, and the customer loses patience. The bag auto-hands-off once it's complete.

6. **Real 3D, PS1 style.** Low-poly 3D rendered at 320x180 with chunky pixels and wobbly vertices, fixed angled camera, free movement in every direction. Layout follows the sketch in `docs/sketches/2026-11-03-kitchen-layout.jpg`: long pick-up counter across the back, stations spread around the floor.

### Controls (Milestone 1)

- D-pad / left stick: walk anywhere
- L / R: switch which held item is selected
- A: grab, start a machine, or bag the selected item
- B: toss the selected item (-$1)

## Milestones

- **v1: side-view bag loop (done).** First version of the bag loop, 2D side view. Lives in `prototypes/v1-side-view.html`.
- **v0: combo kitchen (done).** Walking, stations, arrow combos, tables, patience, corporate strikes, gamepad input. Lives in `prototypes/v0-combo-kitchen.html`. Used to prove the feel and the art direction.
- **Milestone 1: bag loop (first build done, now playtesting).** One counter, 4 to 5 grab stations, bagging counter, orders of 2 to 5 items, patience, pay, corporate strikes. No unlocks, no upgrades. Goal: is routing fun?
- **Milestone 2: feel.** Real sprites from the user's drawings, sound, juice (item pops, bag rustle, angry customer animation).
- **Milestone 3: a full shift.** Difficulty curve over a shift, end-of-shift results.

Nothing after Milestone 3 is planned on purpose.

## Parking lot

Ideas that sound cool but are **not** being built yet:

- Arrow-combo cooking (from v0)
- Food burning if left in a machine too long
- Machines that cook batches of 2+
- Drive-thru window
- Menu unlocks over a shift
- Upgrades between shifts (faster shoes, bigger hands)
- District manager boss visit
- Multiple employees / co-op
- Thor bottom-screen as the order board
- APK wrapper for the Thor launcher

## Tech

- Single HTML file, plain JS, no build step.
- Three.js r128 from cdnjs. Renders at 320x180 and scales up with nearest-neighbor for the PS1 look.
- UI (order bubbles, timers, hands) is HTML drawn over the 3D view.
- Input: keyboard, touch buttons, Gamepad API.
- Hosted with GitHub Pages so it runs in any browser, including on the Thor.
