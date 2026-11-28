<div align="center">

# 🌡️ GT30PRO THERMAL KILL

**A KernelSU module that bypasses thermal throttling on the Infinix GT 30 Pro, for benchmark sessions only.**
*Deep kernel/DVFS-level bypass without stopping the MediaTek thermal service.*

![Version](https://img.shields.io/badge/version-1.1--KSU-f0883e?style=flat-square)
![Category](https://img.shields.io/badge/CATEGORY-PROJECT-30363D?style=flat-square)
![KernelSU](https://img.shields.io/badge/root-KernelSU-2f81f7?style=flat-square)
![Chipset](https://img.shields.io/badge/chipset-MediaTek-d29922?style=flat-square)
![Device](https://img.shields.io/badge/device-Infinix%20GT%2030%20Pro-8b949e?style=flat-square)
![Use](https://img.shields.io/badge/USE-BENCHMARK%20ONLY-e33b3b?style=flat-square)

<br>

[![OPEN PROJECT](https://img.shields.io/badge/▶_OPEN_PROJECT-GT30PRO_THERMAL_KILL-f0883e?style=for-the-badge&logo=github&logoColor=white)](https://github.com/afifcom321/Infinix-gt-30-pro-Disable-Thermal-)

<sub>Opens the live repository with the module source, installation guide, and full documentation.</sub>

</div>

---

> 📂 **Personal Archive** · `04 — Projects` · [← Back to Archive](../../README.md)

> [!WARNING]
> This module disables almost all of the device's thermal protection. It is intended **only for short benchmark sessions** and should be **uninstalled right after**. Using it for daily use or gaming risks overheating, faster battery degradation, and permanent hardware damage. Always monitor the device temperature manually while it is active.

## 01 / OVERVIEW

GT30Pro Thermal Kill is a **KernelSU** module for the **Infinix GT 30 Pro** (MediaTek). It removes kernel and DVFS-level temperature limiting (thermal zones, cooling devices, the DVFS ceiling, and battery throttle) so the chip can sustain its full performance during a benchmark run.

It deliberately does **not** stop the `vendor.thermal-mediatek` service, so the system does not flag a thermal anomaly. It also does **not** lock CPU/GPU frequency: the governor keeps the system's default behavior.

## 02 / WHAT IT DOES

1. **Stops non-essential thermal services**, except `vendor.thermal-mediatek`, which is left running on purpose.
2. **Disables all kernel thermal zones.** Mode is set to `disabled`, trip points are raised to 200 °C, and the policy is switched to `user_space`.
3. **Forces cooling devices to state 0**, so cooling-side throttling never activates.
4. **Unlocks the APU/NPU** by locking the AI engine to maximum frequency.
5. **Disables battery throttle**, the power capping triggered by battery level or heat.
6. **Tunes the scheduler** by raising `schedtune.boost` for top-app/foreground, disabling `sched_autogroup`, and enabling CPU boost.
7. **Removes MediaTek's DVFS thermal ceiling** through several debugfs/procfs paths.
8. **Runs a "safe" watchdog** every 5 seconds. It stops the thermal service again if it restarts and resets any cooling device that becomes active, without touching `vendor.thermal-mediatek`.

Activity is logged to `/data/local/tmp/gt30pro_thermal.log`.

## 03 / PROJECT AT A GLANCE

| | |
|---|---|
| **Project** | GT30Pro Thermal Kill |
| **Version** | v1.1-KSU |
| **Type** | KernelSU module (shell scripts + system properties) |
| **Domain** | Android internals · Kernel · Performance tuning |
| **Target device** | Infinix GT 30 Pro (MediaTek chipset) |
| **Root method** | KernelSU |
| **Intended use** | Short benchmark sessions only |
| **Source** | [github.com/afifcom321/Infinix-gt-30-pro-Disable-Thermal-](https://github.com/afifcom321/Infinix-gt-30-pro-Disable-Thermal-) |

## 04 / MODULE STRUCTURE

| File | Purpose |
|---|---|
| `module.prop` | Module metadata shown in the KernelSU manager |
| `system.prop` | Build-time properties: disables MTK Thermal 2.0, DVFS bypass, APU/NPU thermal, and battery throttle |
| `customize.sh` | Install-time script: prints analysis info and instructions, copies module files |
| `post-fs-data.sh` | Runs very early in boot and disables thermal zones through sysfs as soon as possible |
| `service.sh` | Runs after boot: APU unlock, battery throttle disable, scheduler tuning, and the watchdog |

## 05 / COMPATIBILITY

| Device | Root method | Status |
|---|---|---|
| Infinix GT 30 Pro | KernelSU | ✅ Tested |
| Infinix GT 30 Pro | Magisk | ❌ Not tested |
| Other MediaTek devices | KernelSU / Magisk | ❌ Not tested, not recommended |

## 06 / QUICK START

1. Download the module zip from the repository's Releases page.
2. In **KernelSU Manager**, go to **Module → Install from storage** and select the zip.
3. Reboot, then check `/data/local/tmp/gt30pro_thermal.log` to confirm it is running.
4. Run the benchmark, then **uninstall the module** and reboot.

**Benchmark tips:** charge to 80% or more (or keep the charger connected), let the device cool for about 5 minutes first, and close all background apps before running AnTuTu or similar.

For the full guide, including verification and bootloop recovery, see the [main repository](https://github.com/afifcom321/Infinix-gt-30-pro-Disable-Thermal-).

## 07 / DISCLAIMER

This module is provided as-is, without warranty, for experimentation and benchmarking on the Infinix GT 30 Pro with KernelSU. All risks, including bootloops, soft-bricking, and battery or hardware damage, are the user's responsibility. Only use it if you understand the risks and know how to recover your device.

## 08 / DOCUMENTATION

<!--
Add benchmark screenshots to the documentation/ folder, then uncomment:

![Benchmark result](documentation/benchmark.png)
![Module log](documentation/log.png)
-->

*Benchmark results and screenshots will be added to the `documentation/` folder.*

## 09 / LINKS

| | |
|---|---|
| 🔗 **Source code** | [github.com/afifcom321/Infinix-gt-30-pro-Disable-Thermal-](https://github.com/afifcom321/Infinix-gt-30-pro-Disable-Thermal-) |
| 📂 **Back to archive** | [Personal Archive](../../README.md) |

---

<div align="center">

[![OPEN PROJECT](https://img.shields.io/badge/▶_OPEN_PROJECT-GT30PRO_THERMAL_KILL-f0883e?style=for-the-badge&logo=github&logoColor=white)](https://github.com/afifcom321/Infinix-gt-30-pro-Disable-Thermal-)

<sub>Personal Archive · Afif Sakti Widialukman ([@afifcom321](https://github.com/afifcom321))</sub>

</div>
