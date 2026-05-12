# Waymo Passenger Safety Assistant — Agent Spec

> Read this before starting any work. This is the source of truth for what we're building, who it's for, and how each feature should behave. When in doubt, come back here — don't infer intent from code.

---

## 1. What We're Building

An in-ride safety layer for Waymo passengers. When a rider feels unsafe — about where they're being dropped off, about their surroundings, or about an immediate threat — this overlay gives them a fast, one-tap path to a safe outcome without having to call anyone, figure out an address, or leave the app.

**Target user**: Someone riding alone at night in an unfamiliar neighborhood who isn't sure whether their drop-off location is safe and wants a fallback they can trust.

**Behavior we want to create**: Riders complete their trips even when they feel uncertain. They don't abandon rides or call support — they use the safety tools and arrive somewhere safe.

**What this is NOT**:
- Not a general rideshare or navigation app
- Not a wellness or comfort feature — every interaction leads to a concrete action
- Not a replacement for 911 — it helps passengers get to safe locations, it does not contact emergency services on their behalf
- Not social — no crowdsourced reports, no community input

---

## 2. Features

### Unsafe Drop-Off

When a passenger is approaching their destination and doesn't feel safe about the drop-off location, they can request to be taken somewhere safer instead. The app finds nearby safe places — police stations, hospitals, pharmacies, fire stations — and lets the passenger pick one. The car re-routes there instead.

This option becomes available once the ride is well underway (roughly 75% of the way through the route). Before that point, it's not accessible — the passenger committed to a destination and early changes are handled through normal rerouting.

If the passenger opens the safe places list and decides they're fine, they can dismiss it and continue to the original destination.

### Ride Re-Route

The passenger can change their destination mid-ride. They search for a new location, confirm it, and the ride re-paths. The progress bar doesn't reset to zero — it holds at wherever the ride was when the change happened and continues from there.

If the passenger changes their mind immediately after rerouting, they have a short window to cancel and restore the original destination.

### I'm in Danger

For situations where a passenger feels an immediate threat. One tap opens an emergency overlay. There's a 5-second window where the passenger can cancel if they tapped by accident — after that, the system commits: the car is silently re-routed to the nearest police station, and a persistent red banner appears on screen indicating an emergency response is active.

If the passenger resolves the situation before arrival, they can tap "I'm Safe" on the banner to cancel the emergency routing and return to their original destination.

The 5-second cancel window is intentional. Do not remove it or shorten it — false triggers are common in stressful moments and an immediate non-cancellable action would erode trust.

### Return to Car

After the ride ends and the passenger has exited, they may realize they need to go back — maybe they forgot something, or the area doesn't feel safe. Tapping "Return to Car" unlocks the door and starts a 60-second countdown. If the passenger boards and taps "I'm in — Lock the Door," the door locks immediately. If the countdown expires, the door auto-locks.

60 seconds is the right window. It's long enough to actually board without rushing; shorter countdowns were tested and felt stressful.

### Post-Ride Survey

After the ride completes, the passenger is asked to rate their experience. The survey appears when the passenger taps Done on the arrival screen. It's a simple 5-star rating — selecting a star enables Submit, and submitting closes the loop with a thank-you screen.

Done is the only entry point to the survey. There is no separate "Rate Ride" button — that was redundant.

---

## 3. Arrival Screen

When the ride ends, the passenger sees two options:

- **Return to Car** (top) — for when they need to go back or the area feels unsafe
- **Done** (bottom) — confirms arrival and opens the survey

That order is intentional. Return to Car is the more time-sensitive action — the car might drive away — so it sits above Done.

---

## 4. Design Principles

**One clear action per moment.** Every screen or overlay should have one obvious next step. Don't make passengers think when they're already stressed.

**Fast to safety, easy to cancel.** The path to a safe outcome should be as short as possible. But every committed action should have an undo window — people tap things by accident, especially when nervous.

**Real data, graceful fallback.** Where possible, use live location data to find actual nearby safe places. If the network fails, show a clear message rather than an empty state or a spinner that never resolves.

**Don't replace 911.** The app routes to safe locations. It does not auto-dial, auto-text, or contact authorities on the passenger's behalf. That boundary is deliberate.

---

## 5. What We Are Not Building (in this prototype)

- Real vehicle integration (door locks, dispatch signals)
- User accounts or persistent history
- Push notifications or background monitoring
- Any server-side component — this is a browser-based prototype
- Automatic risk scoring of drop-off locations (progress % is a proxy for now)
- Emergency contact notification

---

## 6. Open Questions

Things that are unresolved and should not be assumed away:

- **Risk signal**: What actually triggers the Unsafe Drop-Off prompt — a fixed progress threshold, a geographic risk model, or something the passenger manually activates? The prototype uses 75% progress as a stand-in.
- **Danger escalation**: Should "I'm in Danger" notify anyone outside the app (Waymo ops, emergency contact)? Currently it only re-routes the car.
- **Place staleness**: If the car is stopped for several minutes, the nearby safe places list may be outdated. No refresh logic is defined.
- **Distance limits**: If the nearest police station is 15 miles away, should it still be shown? No distance cap is defined yet.
- **Survey data**: Where do ratings go? The prototype captures them in memory only.
