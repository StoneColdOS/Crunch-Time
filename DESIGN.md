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

## Open questions (answer before Milestone 1 code)

1. **Where does the bag live?**
   - A: A bagging counter. Bags sit on it, you drop items into them, then carry the finished bag out. *(My recommendation. It creates a hub you route through, like Dave's counter.)*
   - B: You carry the bag around and drop items into it.
2. **Carry limit?** Recommend 2 loose items at a time, so big orders force multiple trips. That's where the routing skill comes from.
3. **Are items ready to grab, or do some need prep?** Recommend: most are instant grabs, and 1 or 2 (quesadilla, drink) need a short timed action (grill, pour) that you can start and walk away from. That's the Dave "juggling" feel. The arrow combos from v0 go in the parking lot unless they test well.
4. **Where do customers pick up?** Counter only, or counter + drive-thru window later?
5. **Wrong bag:** what happens if you pack an item they didn't order? Penalty, or you can pull it back out?

## Milestones

- **v0: combo kitchen (done).** Walking, stations, arrow combos, tables, patience, corporate strikes, gamepad input. Lives in `prototypes/v0-combo-kitchen.html`. Used to prove the feel and the art direction.
- **Milestone 1: bag loop, ugly is fine.** One counter, 4 to 5 grab stations, bagging counter, orders of 2 to 5 items, patience, pay, corporate strikes. No unlocks, no upgrades. Goal: is routing fun?
- **Milestone 2: feel.** Real sprites from the user's drawings, sound, juice (item pops, bag rustle, angry customer animation).
- **Milestone 3: a full shift.** Difficulty curve over a shift, end-of-shift results.

Nothing after Milestone 3 is planned on purpose.

## Parking lot

Ideas that sound cool but are **not** being built yet:

- Arrow-combo cooking (from v0)
- Drive-thru window
- Menu unlocks over a shift
- Upgrades between shifts (faster shoes, bigger hands)
- District manager boss visit
- Multiple employees / co-op
- Thor bottom-screen as the order board
- APK wrapper for the Thor launcher

## Tech

- Single HTML file, plain JS, canvas at 240x150 scaled up, no build step.
- Input: keyboard, touch buttons, Gamepad API.
- Hosted with GitHub Pages so it runs in any browser, including on the Thor.
