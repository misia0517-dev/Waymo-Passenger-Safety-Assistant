# 🚖 Waymo Passenger Safety Assistant

An interactive mobile prototype that reimagines in-ride safety controls for Waymo One autonomous rides.

**[🔗 Live Demo](https://misia0517-dev.github.io/Waymo-Passenger-Safety-Assistant/)**

---

## The Problem

Solo riders — especially women traveling late at night — feel a loss of control during autonomous rides. The car drives itself, and if something feels wrong, the only options are calling 911 or contacting Waymo support: both require leaving the app, losing ride context, and acting under pressure with no visible fallback.

Post-ride survey data shows solo night-time riders rate their subjective safety 0.4 points below the fleet average, despite a zero incident rate. The gap is not about actual safety — it's about perceived control.

## The Solution

A proactive safety layer embedded directly in the ride UI. Every feature is one tap away, available without leaving the app, and designed for the moment a rider feels uncertain — not after a situation has already escalated.

---

## Features

### 🗺️ Live Ride Simulation
A full journey from pickup to arrival on a Leaflet-powered night-mode map. The car moves in real time and the UI transitions automatically through four phases — **Waiting → En Route → Approaching → Arrived** — with live progress tracking throughout.

### 📍 Unsafe Drop-Off
Available once the ride is 75% complete. Riders can flag a drop-off that feels wrong and immediately see nearby safe alternatives — police stations, hospitals, pharmacies, fire stations — fetched live from Overpass. Selecting a location reroutes the car on the map in real time. If results are sparse, a Nominatim keyword fallback runs automatically to find more options.

### 🔄 Re-Route
Change the destination at any point mid-ride. Address search uses live Nominatim autocomplete; confirming a new location redraws the route immediately. Trip progress is preserved — the progress bar never resets to zero after a reroute.

### 🆘 I'm in Danger
One tap opens an emergency overlay with a 5-second cancel window (for accidental triggers). After the window, the system commits:
- A Waymo Safety Agent connects
- The nearest police station is located via Overpass
- The car reroutes there automatically
- A persistent red banner shows the destination and an active cancel option

If the situation resolves, the rider taps **I'm Safe** to cancel the emergency routing and restore the original destination.

### 🔓 Return to Car
On arrival, riders can unlock the car door and re-board within a 60-second window — enough time to look around before deciding whether to exit. Tapping **I'm in** locks the door immediately and prompts a check on whether the current location feels safe.

### ⭐ Post-Ride Safety Survey
Triggered by tapping **Done** on the arrival screen, or automatically 8 seconds after arrival. Collects a 5-star safety rating and an optional written comment. Survey responses feed the Subjective Safety Score used to evaluate the A/B experiment.

---

## Demo Walkthrough

| Phase | What you'll see |
|-------|----------------|
| **Car Arrived** | Pickup confirmation, ride start |
| **En Route** | Live map, ETA countdown, safety controls unlock at 75% |
| **Unsafe Drop-Off** | Nearby safe locations fetched live, reroute on confirm |
| **I'm in Danger** | 5s cancel window → agent connect → police station navigation |
| **Arrived** | Return to Car (60s window), Done → survey |

Use the speed controls and nav buttons below the phone to move through phases or adjust simulation speed.

---

## Built With

- **Vanilla HTML / CSS / JavaScript** — no frameworks, no build step
- **Leaflet.js** — interactive night-mode map with live car animation
- **Overpass API** — real-time nearby safe place lookup
- **Nominatim** — address autocomplete and place search fallback
- **Single-file prototype** (~2,900 lines)

---

## Running Locally

No build step required:

```bash
git clone https://github.com/misia0517-dev/Waymo-Passenger-Safety-Assistant.git
open index.html
```

Or visit the [live demo](https://misia0517-dev.github.io/Waymo-Passenger-Safety-Assistant/) directly.
