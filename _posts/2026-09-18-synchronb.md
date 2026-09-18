---
layout: post
published: false
title: "SynchroNB: Toward Robust Timing for 5G NB-IoT Networks"
date: 2026-09-18
description: How we make time synchronization more accurate and efficient on cellular IoT devices.
author: Muhammad Abdullah Soomro
tags: [research, NB-IoT, time synchronization]
permalink: /synchronb/
---

**Can a tiny cellular device keep accurate time without keeping its radio awake?** That question motivated SynchroNB, our work on time synchronization for 5G Narrowband Internet of Things (NB-IoT) networks. The paper appeared at [ACM/IEEE SenSys 2026](https://doi.org/10.1145/3774906.3800502).

**[Read the paper](https://doi.org/10.1145/3774906.3800502)** · **[See the conference talk abstract](https://newenglandsystemsday.github.io/2026/schedule.html)** · **[Citation](#citation)**

## Why timing is hard on NB-IoT

NB-IoT connects low-power devices through cellular networks. A synchronized clock helps devices coordinate measurements and make sense of events recorded at different places. But a device has to conserve energy, so its radio may sleep for long periods. While it sleeps, its local clock drifts.

Waking up and asking a time server does not solve the whole problem. Cellular scheduling, retransmissions, and uneven delays in the two directions can make a network time exchange misleading. Those effects can produce tens or hundreds of milliseconds of error, even when the device successfully receives a response.

> The challenge is to decide **when** a device needs a new timing update, then make that update dependable despite the behavior of the radio and network.

## The SynchroNB approach

SynchroNB combines prediction with control across the device's timing and communication layers:

1. **Predict clock drift.** Estimate how the device's local clock changes while the radio sleeps, so it can avoid unnecessary wake-ups.
2. **Choose when to synchronize.** Schedule modem activity around the expected timing error and the cost of turning on the radio.
3. **Improve the timing exchange.** Account for changing link conditions, reserve uplink resources when needed, and prioritize synchronization traffic at the MAC layer.

Together, these pieces address both sides of the problem: error that grows while the device is asleep and error introduced when it communicates with the network.

## What we observed

We deployed SynchroNB on commercial hardware over a live network. In the [public talk abstract](https://newenglandsystemsday.github.io/2026/schedule.html), we report single-millisecond synchronization accuracy while using **36% of the radio-on time** and **25% of the bandwidth** of an NTP baseline. These figures describe that evaluation, not a guarantee for every device or network.

The result suggests that accurate time on a low-power cellular device does not require constant communication. The device can spend less time on the air when it predicts its clock well and treats each timing exchange as a network scheduling problem.

## Citation

```bibtex
@inproceedings{soomro2026synchronb,
  title     = {SynchroNB: Toward Robust Timing for 5G NB-IoT Networks},
  author    = {Soomro, Muhammad Abdullah and Nazeer, Muhammad Shayan and DelSignore, Collin and Chandio, Yasra and Raza, Muhammad Taqi and Anwar, Fatima Muhammad},
  booktitle = {Proceedings of the 24th ACM Conference on Embedded Networked Sensor Systems},
  year      = {2026},
  doi       = {10.1145/3774906.3800502}
}
```
