# 🚖 Waymo Passenger Safety Assistant

An interactive mobile prototype that reimagines passenger safety controls for Waymo One autonomous rides — built as a research prototype for UCLA MGMT 275.

**[🔗 Live Demo](https://misia0517-dev.github.io/Waymo-Passenger-Safety-Assistant/waymo_safety_prototype.html)**

---

## The Problem

Late-night Waymo riders — especially women traveling alone — have no real-time way to intervene if something feels wrong. The car drives itself, and current options (calling 911, contacting support) require leaving the app and losing context.

## The Solution

A proactive safety layer built directly into the ride UI. Passengers can act immediately without leaving the app — before a situation escalates.

---

## Features

### 🗺️ Live Ride Simulation
Full journey phases with an animated night-mode map: **Waiting → En Route → Approaching → Arrived**. The car moves in real time, behavior updates at each intersection, and phase transitions happen automatically.

### 📍 Unsafe Drop-Off
Flag a drop-off location that feels unsafe. Choose from vetted alternatives (well-lit storefronts, staffed hotel lobbies) — the car reroutes on the map in real time with an animated route preview.

### 🔄 Re-Route
Request a new drop-off mid-trip. The reroute screen draws an animated teal route to the new destination; the main map updates immediately on confirm.

### 🆘 I'm in Danger
One tap connects to a live safety agent. The prototype simulates the full sequence:
1. Agent connects (~3s)
2. Nearest police station located (~5.5s)
3. Animated reroute preview drawn to SFPD Northern Station
4. Car automatically navigates there — emergency banner stays visible with a cancel option

### ⭐ Post-Ride Safety Survey
A 30-second feedback form collects safety ratings and lets riders flag specific concerns. Responses feed directly into Waymo's safety data.

---

## Demo Walkthrough

| Phase | What you'll see |
|---|---|
| Car Arrived | Pickup confirmation, ETA share, Start Ride |
| En Route | Live map, ETA countdown, safety controls |
| Unsafe Drop-Off | Alternative locations, reroute animation |
| I'm in Danger | Agent connect sequence → police station navigation |
| Arrived | Door unlock, safety survey |

Use the **nav buttons below the phone** to jump to any phase instantly.

---

## Built With

- Vanilla HTML / CSS / JavaScript — no frameworks, no dependencies
- HTML5 Canvas for animated map and reroute visualization
- `requestAnimationFrame` animation loop
- Single-file prototype (~1,400 lines)

---

## Running Locally

No build step needed. Just open the file:

```bash
git clone https://github.com/misia0517-dev/Waymo-Passenger-Safety-Assistant.git
open waymo_safety_prototype.html
```

Or visit the **[live demo](https://misia0517-dev.github.io/Waymo-Passenger-Safety-Assistant/waymo_safety_prototype.html)** directly.

---

## Course Context

Built for **UCLA Anderson MGMT 275** as part of an experimentation and evaluation exercise on AI-assisted product design. The prototype was designed to test whether proactive in-app safety controls meaningfully change passenger confidence during autonomous vehicle rides.

**Researcher:** Mia Wu, UCLA Anderson School of Management
