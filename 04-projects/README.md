<div align="center">

# 04 / PROJECTS

**Tools built to solve real, practical problems.**
*Why each project exists, what it does, and where to find it.*

![Projects](https://img.shields.io/badge/PROJECTS-3-30363D?style=flat-square)
![Focus](https://img.shields.io/badge/FOCUS-WEB%20%C2%B7%20DESKTOP%20%C2%B7%20ANDROID-2f81f7?style=flat-square)
![Approach](https://img.shields.io/badge/APPROACH-LOCAL--FIRST-238636?style=flat-square)

</div>

---

> 📂 **Personal Archive** · [← Back to Archive](../README.md)

## 01 / ABOUT THIS FOLDER

This folder collects the projects of **Afif Sakti Widialukman** (IoT, web development, Linux, and cybersecurity). Each one started from a concrete problem: a stream that competes for bandwidth, a school bell that depends on someone pressing a button, a phone that throttles itself during a benchmark.

Every project has its own folder with a summary README and a button to the live repository. This page explains the reasoning behind them.

## 02 / PROJECT OVERVIEW

| Project | Problem it solves | Stack | Links |
|---|---|---|---|
| 🔴 **Lokalens** | Camera feeds compete with the live broadcast for venue internet | Node.js · WebRTC · Socket.IO | [Summary](lokalens/README.md) · [Repo](https://github.com/afifcom321/lokalens) |
| 🔔 **School Bell System** | School bells that rely on paper schedules and someone pressing a button | Electron · Node.js · SQLite | [Summary](school-bell-system/README.md) · [Repo](https://github.com/afifcom321/School-Bell-System) |
| 🌡️ **GT30Pro Thermal Kill** | Thermal throttling that distorts benchmark results | KernelSU · Shell · MediaTek | [Summary](gt30pro-thermal-kill/README.md) · [Repo](https://github.com/afifcom321/Infinix-gt-30-pro-Disable-Thermal-) |

---

## 03 / 🔴 LOKALENS

[![OPEN PROJECT](https://img.shields.io/badge/▶_OPEN_PROJECT-LOKALENS-e33b3b?style=for-the-badge&logo=github&logoColor=white)](https://github.com/afifcom321/lokalens)

### Why it exists
At an event, the venue's internet is usually limited and already carrying the main broadcast to YouTube or Facebook. If extra camera feeds also travel over the internet, they compete with that broadcast for the same bandwidth. Tools like VDO.Ninja solve multi-camera streaming well, but they depend on the internet.

Lokalens keeps the two separate. Camera feeds stay inside the local network, so the internet connection is reserved for the broadcast.

### What it does
Turns phones, laptops, and webcams on the same Wi-Fi/LAN into camera sources for OBS Studio. A phone opens a web page and taps **START STREAM**, and the picture shows up in a Director page and in OBS.

### How it works
Video flows directly between devices over WebRTC P2P. A small Express + Socket.IO server on the user's own PC handles only signaling, the web app, and QR codes, so it never relays video.

### Design decisions
- **No internet at runtime.** No CDN, no cloud services, and QR codes are generated locally.
- **No build step.** The frontend is plain HTML/CSS/JS.
- **A separate plain-HTTP port for OBS**, so its browser has no trouble with the self-signed certificate.
- **A known trade-off, stated openly:** reach is limited to one network, in exchange for zero load on the venue's internet.

---

## 04 / 🔔 SCHOOL BELL SYSTEM

[![OPEN PROJECT](https://img.shields.io/badge/▶_OPEN_PROJECT-SCHOOL_BELL_SYSTEM-d29922?style=for-the-badge&logo=github&logoColor=white)](https://github.com/afifcom321/School-Bell-System)

### Why it exists
A school bell has to ring on time, every time, without someone remembering to press a button or reading a paper schedule. Many simple bell apps use a single timer calculated once at startup. Those drift over time, lose their place when restarted, and depend on a browser tab staying open.

### What it does
A Windows desktop app that runs a local server which schedules and rings the bell automatically. A web dashboard, reachable from any phone or computer on the school network, manages schedules, sounds, exam mode, holidays, and user roles.

### How it works
The scheduler runs on the computer, not in a browser tab. It ticks about once per second and computes bell times from the real system clock. Each rung schedule is marked in the database to prevent double-ringing, and the next bell is recalculated after every restart. A late bell within a tolerance still rings, and a very late one is logged as missed.

### Design decisions
- **Restart-safe scheduling** instead of one long timer.
- **`node:sqlite`**, the SQLite module built into Node.js, so building the `.exe` needs no Python or Visual Studio Build Tools.
- **Viewer and Administrator roles**, so the teacher on duty can see the schedule without being able to change it.
- **Security basics included:** scrypt password hashing, login rate limiting, and strict validation of uploaded sound files.
- **Automated tests** for the scheduler and every REST endpoint.

---

## 05 / 🌡️ GT30PRO THERMAL KILL

[![OPEN PROJECT](https://img.shields.io/badge/▶_OPEN_PROJECT-GT30PRO_THERMAL_KILL-f0883e?style=for-the-badge&logo=github&logoColor=white)](https://github.com/afifcom321/Infinix-gt-30-pro-Disable-Thermal-)

### Why it exists
During a benchmark, a phone's thermal management lowers performance as it heats up, so the score reflects the throttling as much as the hardware. This module removes that limiting for short benchmark sessions on the Infinix GT 30 Pro, so the result shows what the chip can actually do.

### What it does
A KernelSU module that disables kernel and DVFS-level thermal limiting: thermal zones, cooling devices, the DVFS ceiling, and battery throttle. It also unlocks the APU/NPU and tunes the scheduler.

### Design decisions
- **The `vendor.thermal-mediatek` service is left running on purpose**, so the system does not flag a thermal anomaly.
- **CPU/GPU frequency is not locked.** The governor keeps the system's default behavior.
- **A watchdog every 5 seconds** stops the thermal service again if it restarts and resets any cooling device that becomes active.
- **Honest scope and warnings:** the module is for benchmark sessions only, tested only on KernelSU with this device, and the README states the hardware risks plainly.

---

## 06 / WHAT THESE PROJECTS HAVE IN COMMON

- **They start from a real problem**, not from a technology looking for a use.
- **Local-first.** Lokalens and School Bell System both run fully on the local network, with no internet needed for daily operation.
- **Reliability matters more than features.** Restart-safe scheduling, watchdogs, and automatic reconnects appear throughout.
- **Trade-offs are documented.** Each repository lists its limitations, and the risky one carries explicit warnings.

<!--
Personal notes (optional): add a short paragraph in your own words about what
motivated you to build these, e.g. a specific event, a school need, or what you
wanted to learn. Delete this comment when done.
-->

## 07 / NEXT

More projects will be added to this folder as they are built and documented. Each one follows the archive's documentation standard:

```
project-name/
├── README.md
└── documentation/
    └── screenshots, demos
```

---

<div align="center">

[← Back to Personal Archive](../README.md)

<sub>Personal Archive · Afif Sakti Widialukman ([@afifcom321](https://github.com/afifcom321))</sub>

</div>
