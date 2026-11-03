# Crunch Time: Design Doc

A side-view diner game in the style of the sushi bar in Dave the Diver, set in a 90s fast-food joint at 1 a.m. and seen through a PS1 survival-horror lens. One cook, one server (you), too many customers.

This doc is the single source of truth. If an idea isn't in **Core** or the current **Milestone**, it goes in the **Parking Lot**, not the code.

---

## Core loop (locked 2026-11-03, replaces the bag-packing loop)

1. A customer walks in, sits in a booth, and orders 1 to 4 items. The order floats over their head.
2. The **cook** (an NPC, like Bancho) makes each food item in the order it was ordered and sets it on the **pass**.
3. **Drinks are on you**, like Dave's green tea: press A at the fountain to start it, walk away, come back and take the drink.
4. You walk the floor, take items off the pass, and serve each item to whoever ordered it. Any taco works for any taco order.
5. When everything is served, the customer eats, pays, and tips based on how fast you were.
6. Serving the wrong item costs $1 and some patience. If a customer waits too long, they **call corporate**. Three calls and the shift ends.

The fun is in **juggling**: which plates to grab, who to serve first, when to break off and pour a drink.

## Pillars

- **Readable at a glance.** You always know who is about to blow and what they want.
- **Movement is the skill.** Walking efficiently is what separates a good shift from a bad one.
- **A 90s fast-food diner through a PS1 survival-horror lens.** Fog, grime, flickering fluorescents, a cook who never quite turns around. Unsettling, never gory. The comedy ("they'll call corporate") stays, it just gets ominous. An original brand, no real logos.
- **Plays great on the AYN Thor.** Controller first, touch second.

## Decisions

1. **Side view, camera follows you**, like Dave the Diver. You walk left and right along one lane in front of everything.
2. **Real 3D, PS1 style.** Low-poly 3D rendered at 320x180 with chunky pixels and wobbly vertices, fog, film grain.
3. **Single items, not bags.** The cook hands out individual items; you match items to customers.
4. **Carry limit: 5 items** (`T.HANDS`). If juggling feels too easy, try 3.
5. **Wrong item is a penalty.**
6. **Pass holds 4 items** (`T.PASS_SLOTS`). If it's full, the cook stops and waits, so letting food pile up slows the whole kitchen.

### Controls

- Left / Right: walk
- L / R (or Up / Down): choose which held item you're holding out
- A: take from the pass, start or take from the fountain, serve
- B: throw out the held item (-$1)

## History

- **v0: combo kitchen.** Arrow-combo cooking, tables. `prototypes/v0-combo-kitchen.html`
- **v1: side-view bag loop.** You gathered items and packed bags. `prototypes/v1-side-view.html`
- **v2: bright PS1 3D.** Bag loop, top-down 3D from the 2026-11-03 sketch. `prototypes/v2-bright-3d.html`
- **v3: horror kitchen.** Bag loop with fog, grime, fixed RE-style cameras, ticket rail. `prototypes/v3-horror-kitchen.html`
- **v4: Dave-style diner (current).** Cook + pass + delivery, side view, horror look kept. `index.html`

## Milestones

- **Milestone 1: is serving fun? (now playtesting v4).** One cook, pass, fountain, 5 booths, patience, pay, corporate calls. No upgrades, no unlocks.
- **Milestone 2: feel.** Real sprites or models from the user's drawings, sound, juice (plate clatter, customer reactions).
- **Milestone 3: a full shift.** Difficulty curve over a shift, end-of-shift results.

Nothing after Milestone 3 is planned on purpose.

## Parking lot

Ideas that sound cool but are **not** being built yet:

- Drink refills mid-meal (Dave's tea refills)
- Bagged takeout orders or a drive-thru window
- Arrow-combo cooking (v0)
- Food burning, machines that cook batches
- Horror events (lights cut out, a customer who never leaves, something in the walk-in, the cook turning around)
- Fixed RE-style camera angles (v3) and tank controls
- Menu unlocks, upgrades between shifts, a district manager boss visit
- Multiple employees / co-op
- Thor bottom screen as the order board
- APK wrapper for the Thor launcher

## Tech

- Single HTML file, plain JS, no build step.
- Three.js r128 from cdnjs. Renders at 320x180 and scales up with nearest-neighbor.
- UI (order bubbles, timers, hands) is HTML drawn over the 3D view.
- Every gameplay number lives in the `T` tuning block at the top of the script.
- Hosted with GitHub Pages so it runs in any browser, including on the Thor.
