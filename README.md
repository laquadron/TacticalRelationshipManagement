# TacticalRelationshipManagement-aka-CheaterOS-
CheaterOS. It's exactly what it sounds like. Please read the disclaimers.



# TacticalRelationshipManagement (TRM)
### aka CheaterOS 🤣

> Enterprise-grade proximity detection, collision avoidance, and relationship risk mitigation
> for the modern multi-stakeholder personal life.

---

![Build Status](https://img.shields.io/badge/build-passing-brightgreen)
![License](https://img.shields.io/badge/license-MIT%20probably-blue)
![Platform](https://img.shields.io/badge/platform-Android%20Only-orange)
![Ethical Score](https://img.shields.io/badge/ethical%20score-0%2F10-red)
![Stars](https://img.shields.io/badge/stars-undeserved-yellow)
![Therapy](https://img.shields.io/badge/should%20you%20be%20in-therapy%3F%20yes-purple)

---

## ⚠️ DISCLAIMER #1 of 30

This repository is a **satirical educational project** exploring the limits of mobile APIs, proximity detection, and device management systems. It is intended for developers who find humor in the intersection of software engineering and terrible life decisions.

If you are actually using this to manage multiple simultaneous romantic engagements, your primary issue is not technical. It is psychological. Please consult a licensed therapist, a priest, or at minimum a trusted friend who will tell you the truth.

We just like the code.

---

## Table of Contents

1. [Executive Summary](#executive-summary)
2. [The Android-Only Manifesto](#the-android-only-manifesto)
3. [System Architecture](#system-architecture)
4. [Module 1: Proximity Collision Avoidance (PCA)](#module-1-proximity-collision-avoidance)
5. [Module 2: Spatial Data Sanitizer (Geofence Scrub)](#module-2-spatial-data-sanitizer)
6. [Module 3: Contact Camouflage](#module-3-contact-camouflage)
7. [Module 4: Acoustic Alibi Engine](#module-4-acoustic-alibi-engine)
8. [Module 5: Kinetic Process Killer (Panic Flip)](#module-5-kinetic-process-killer)
9. [Phase 2: Advanced Deployment (GrapheneOS)](#phase-2-advanced-deployment)
10. [Threat Model](#threat-model)
11. [Known Bugs](#known-bugs)
12. [Changelog](#changelog)
13. [Contributing](#contributing)
14. [The Remaining 29 Disclaimers](#the-remaining-29-disclaimers)

---

## Executive Summary

Modern relationship management presents unique technical challenges. As personal portfolios scale horizontally, the risk of **Partner Collision Events (PCEs)** increases proportionally. Legacy solutions (lying, having a bad memory, moving to another city) are no longer sufficient in an era of persistent connectivity, location sharing, and read receipts.

**TacticalRelationshipManagement (TRM)** is an open-source Android framework that applies enterprise-grade infrastructure principles to personal life management. Drawing from established patterns in distributed systems — load balancing, event-driven architecture, and zero-trust security — TRM provides a robust toolkit for the modern, highly parallel individual.

**Key Features:**
- Real-time Bluetooth Low Energy (BLE) proximity detection
- Geofence-triggered automated evidence lifecycle management
- Dynamic contact identity masking
- Sensor-based emergency UI switching
- Ambient audio environment simulation

**Target User:** Developers who have made questionable life choices but at least have the technical skills to make them slightly less catastrophic.

**Not for:** iOS users. See [The Android-Only Manifesto](#the-android-only-manifesto).

---

## The Android-Only Manifesto

This framework is **Android-exclusive**. This is a deliberate architectural decision, not a resource constraint. The following table explains why iOS users are not the target demographic for this project:

| Feature | Android (The Ally 🤝) | iOS (The Snitch 🐀) |
|---|---|---|
| Call Interception | `CallScreeningService` allows silent rejection based on runtime logic | Impossible. Apple wants you to confront your problems. |
| Background BLE Scanning | Can scan for Partner A's device 24/7 | Suspends background apps. Partner A walks in. App is asleep. You are not. |
| Custom OS | Flash GrapheneOS for Phase 2 deployment | Stuck with whatever Tim Cook decided you deserve. |
| Sideloading | Install via APK, no questions asked | Requires App Store approval. They will not approve this. |
| Call Screening Logic | Full programmatic control | "Have you tried just... not doing this?" |
| Emergency App Switching | Achievable via background services | Sandboxed into irrelevance |

### The Verdict

> *"If you are trying to run this lifestyle on an iPhone, you are a tourist. Buy a Pixel or go home. The blue bubbles are not worth it. Nothing is worth it. Reconsider your choices. But also, buy a Pixel."*

**Recommended Hardware:** Google Pixel 6 or newer (GrapheneOS compatible)
**Minimum Requirement:** Any Android device with API level 26+
**iOS Support:** Scheduled for never.

---

## System Architecture

```
┌─────────────────────────────────────────────────────────────┐
│              TRM Core Runtime                               │
│                                                             │
│  ┌─────────────┐    ┌──────────────┐    ┌───────────────┐  │
│  │  Watchdog   │───▶│  Event Bus   │───▶│  Action       │  │
│  │  Service    │    │              │    │  Dispatcher   │  │
│  │             │    │  - BLE_ALERT │    │               │  │
│  │ BLE Scanner │    │  - GEO_ENTER │    │ - REJECT_CALL │  │
│  │ GPS Monitor │    │  - CALL_IN   │    │ - NUKE_CACHE  │  │
│  │ Accel Watch │    │  - FLIP_EVT  │    │ - SWAP_APP    │  │
│  └─────────────┘    └──────────────┘    └───────────────┘  │
│         │                                       │           │
│         ▼                                       ▼           │
│  ┌─────────────┐                      ┌───────────────┐    │
│  │  Contact    │                      │  Alibi        │    │
│  │  Map DB     │                      │  Engine       │    │
│  │             │                      │               │    │
│  │ DeviceID_A  │                      │ Audio Presets │    │
│  │ → Block_B   │                      │ SMS Templates │    │
│  └─────────────┘                      └───────────────┘    │
└─────────────────────────────────────────────────────────────┘
```

### Core Components

| Component | Module | Responsibility |
|---|---|---|
| The Watchdog | `ProximityWatchdogService` | Scans for known Danger Zone BLE device IDs every 30 seconds |
| The Contact Map | `RelationshipGraphDB` | Local database linking Device_ID → Blocked_Caller |
| The Silencer | `IncomingCallInterceptor` | Triggers on `PHONE_STATE = RINGING`, checks proximity |
| The Geofence | `SpatialDataSanitizer` | Executes cleanup script on `GEOFENCE_TRANSITION_ENTER` |
| The Alibi | `AutoResponseEngine` | Sends pre-configured SMS to blocked callers |
| The Flipper | `KinetographicProcessKiller` | Accelerometer-based emergency UI switching |

---

## Module 1: Proximity Collision Avoidance

### Overview

The **Proximity Collision Avoidance (PCA)** module is the core risk mitigation engine of TRM. It uses Bluetooth Low Energy (BLE) scanning to detect when a registered "Stakeholder A" device enters the vicinity, and automatically activates **Ghost Mode** to suppress incoming communications from "Stakeholder B."

### How It Works

BLE allows passive scanning of nearby devices without pairing. Each device broadcasts a MAC address or UUID that can be detected and filtered by RSSI (signal strength).

```
RSSI Thresholds:
  < -80 dBm  →  Safe. They are in another building.
  -80 to -60 →  Caution. Same venue. Stay aware.
  -60 to -40 →  Danger. Same room. Ghost Mode activated.
  > -40 dBm  →  Critical. They are literally next to you.
               Put your phone away. Make eye contact. Smile.
```

### Ghost Mode Behaviours

When Partner A's device is detected within the danger threshold:

- All calls from Category B contacts are silently rejected
- Auto-SMS sent: *"Sorry, my phone is acting up. Talk later!"*
- Category B app notifications are suppressed
- Specific app icons are hidden from the launcher

### Pseudocode

```python
# For educational purposes only. Please don't actually do this.

def on_incoming_call(incoming_number):
    nearby_devices = BLE_Scanner.get_nearby_devices()
    
    if PARTNER_A_DEVICE_ID in nearby_devices:
        rssi = nearby_devices[PARTNER_A_DEVICE_ID].rssi
        
        if rssi > DANGER_THRESHOLD:  # e.g. -60 dBm
            if incoming_number in CATEGORY_B_CONTACTS:
                reject_call()
                send_sms(
                    to=incoming_number,
                    body="My phone is acting up, talk later!"
                )
                log_event("Collision avoided. You're welcome.")
                return
    
    allow_call()
```

### ⚠️ DISCLAIMER #2 of 30

Constant BLE scanning will drain your battery approximately 40% faster. You will also need to explain to Partner A why your phone is always at 12% battery. We suggest blaming a "background system process." This is technically true.

---

## Module 2: Spatial Data Sanitizer

### Overview

The **Spatial Data Sanitizer** creates a geofenced "decontamination zone" around a registered safe location (e.g., your home). Upon entry, the module automatically executes a configurable cleanup pipeline.

Think of it as a digital shower. You take one before you walk through the door. Hygienic.

### Trigger

```
GEOFENCE_TRANSITION_ENTER → Execute SanitizationPipeline
```

### Default Sanitization Pipeline

```
Step 1: Browser Nuke
  └── Clear cache, cookies, and history for Chrome/Firefox/Brave
  
Step 2: Gallery Scramble  
  └── Move files from /HotFolder/ to /EncryptedVault/
  └── Remove from MediaStore index (invisible to gallery apps)
  
Step 3: Notification Purge
  └── Clear all pending notifications from Category B apps
  └── (Signal, Telegram, WhatsApp, Instagram DMs, etc.)
  
Step 4: Alibi Confirmation
  └── Log: "Sanitization complete. Home arrival: [TIMESTAMP]"
  └── Optional: Auto-text Partner A: "Just got home! 😊"
```

### Configuration

```xml
<!-- sanitizer_config.xml -->
<!-- This config file will make your phone deeply uncomfortable -->

<SanitizationProfile>
    <GeofenceRadius unit="meters">100</GeofenceRadius>
    <TriggerOn>ENTER</TriggerOn>
    
    <Pipeline>
        <Task id="browser_nuke" enabled="true">
            <Targets>Chrome, Firefox, Brave, Samsung Internet</Targets>
            <Scope>history, cache, cookies</Scope>
        </Task>
        
        <Task id="gallery_scramble" enabled="true">
            <SourceFolder>/DCIM/HotFolder/</SourceFolder>
            <DestinationFolder>/data/user/0/com.trm.vault/</DestinationFolder>
            <RemoveFromIndex>true</RemoveFromIndex>
        </Task>
        
        <Task id="notification_purge" enabled="true">
            <PackageList>
                org.thoughtcrime.securesms,
                org.telegram.messenger,
                com.whatsapp,
                com.instagram.android
            </PackageList>
        </Task>
    </Pipeline>
</SanitizationProfile>
```

### ⚠️ DISCLAIMER #3 of 30

The Geofence Scrub operates on GPS coordinates with approximately 5-15 meter accuracy. If you live in a dense urban area, there is a non-trivial chance your phone sanitizes itself while you are still at the pub across the street. Feature, not bug.

---

## Module 3: Contact Camouflage

### Overview

The **Contact Camouflage** module implements schedule-based dynamic aliasing for contacts in the device's local database. The same phone number can present differently depending on the time of day.

### Example Configuration

```
Contact: [REDACTED NUMBER]

  Weekdays 09:00 - 17:00  →  "Project Manager"
  Weekdays 17:01 - 08:59  →  "Pizza Hut"
  Weekends all day         →  "Spam Risk"
  Special Events           →  "Dentist Office"
```

### ⚠️ DISCLAIMER #4 of 30

You will at some point genuinely forget which number is which and attempt to order a pizza from your project manager. We accept no liability for this.

---

## Module 4: Acoustic Alibi Engine

### Overview

The **Acoustic Alibi Engine** injects pre-recorded ambient audio into the outgoing microphone stream during phone calls, allowing the user to appear to be in a different environment than their current physical location.

### Available Presets

| Preset ID | Audio Environment | Use Case |
|---|---|---|
| `ENV_OFFICE` | Keyboard clacking, printer hum, muffled meeting | "I'm still at work babe" |
| `ENV_TRAFFIC` | Car horns, engine noise, distant sirens | "I'm stuck in traffic" |
| `ENV_TUNNEL` | Static, echo, signal degradation simulation | "Can you hear me? Hello?" |
| `ENV_LIBRARY` | Complete silence, occasional page turn | "I'm studying, can't really talk" |
| `ENV_WIND` | Strong wind noise | "I'm outside, bad signal" |
| `ENV_GYM` | Weights, treadmill ambience | "Just finished a workout" |

### Emergency Preset

```
ENV_EMERGENCY: Sudden loud noise followed by "Oh god, I have to go"
               Call terminates after 3 seconds.
               No questions asked.
```

### ⚠️ DISCLAIMER #5 of 30

Audio injection at the system level requires low-level hooks that will almost certainly trigger the microphone usage indicator on Android 12+. There will be a small dot in the top corner of the screen. If Partner A sees this dot and asks why your microphone is active, you are on your own. The framework does not cover this scenario.

---

## Module 5: Kinetic Process Killer

### Overview

The **Kinetic Process Killer (KPK)** monitors the device accelerometer for rapid face-down placement events. Upon detection, it immediately terminates the foreground application and launches a pre-configured decoy app.

### Detection Logic

```
Z-axis reading ≈ -9.8 m/s²  →  FACE_DOWN event detected
Response time: < 300ms
Decoy App launched: [Configurable. Default: Calculator]
```

### Recommended Decoy Apps

- Calculator (Classic. Timeless. No one questions Calculator.)
- Google Maps (You were just checking directions)
- LinkedIn (They won't ask follow up questions. No one wants to talk about LinkedIn.)
- Your banking app (Implies responsibility. Respect.)
- Duolingo (You're learning Spanish. How wholesome.)

### ⚠️ DISCLAIMER #6 of 30

If Partner A picks up your phone and Calculator is open for no reason, they already know. Calculator does not save you. Calculator has never saved anyone. But it buys you approximately 2-3 seconds to prepare a facial expression, which may be enough.

---

## Phase 2: Advanced Deployment

### The GrapheneOS Protocol

> *For when things get serious. Not to be deployed prematurely.*

Phase 2 is reserved for situations where a relationship has progressed to a point where Partner B requires a dedicated device.

GrapheneOS is a privacy-focused Android distribution designed for maximum security and minimal data exposure. It is genuinely excellent software used by journalists, activists, and security researchers worldwide.

It is also, theoretically, very funny to deploy in the context of this repo.

### The Sales Pitch (Documented for Satirical Purposes)

```
"Look, I work in [VAGUE INDUSTRY INVOLVING SENSITIVE DATA].
 I've seen what these normal phones do to people's privacy.
 I got you a proper hardened device. It's what the serious
 people use. No sketchy apps, no data harvesting, just clean
 private communication.
 
 Also don't try to install TikTok on it.
 Security reasons."
```

### The "Military Grade" MDM Config

```xml
<!-- TRM Enterprise MDM Policy v1.0 -->
<!-- Restriction Profile: PARTNER_B_STANDARD -->

<RestrictionProfile>
    <ProfileName>Secure Communications Standard</ProfileName>
    <IssuingAuthority>Department of Chaos</IssuingAuthority>
    
    <DisableScreenshot>true</DisableScreenshot>
    <!-- "Anti-Espionage Measure" -->
    
    <EnforceVPN>true</EnforceVPN>
    <!-- "Encrypted tunnel to secure infrastructure" -->
    <!-- (The infrastructure is a $5/month VPS) -->
    
    <AppWhitelist>
        <!-- Only audited, approved applications -->
        <App>Signal</App>
        <App>Maps</App>
        <App>Calculator</App>
        <!-- Calculator always makes the list -->
    </AppWhitelist>
    
    <RemoteWipe>enabled</RemoteWipe>
    <!-- "Self-destruct capability for compromised devices" -->
    <!-- (It's just a factory reset button) -->
    
    <FunnyDisclaimer>
        USE OF THIS DEVICE IS MONITORED IN ACCORDANCE WITH
        SECURE COMMUNICATIONS PROTOCOL 7.4.2-CHAOS
        BY CONTINUING TO USE THIS DEVICE YOU ACKNOWLEDGE
        THAT YOU HAVE READ THE TERMS AND CONDITIONS
        (There are no terms and conditions)
    </FunnyDisclaimer>
</RestrictionProfile>
```

### Timing Guidelines

Deploying the GrapheneOS device too early breaks immersion. The following milestone-based rollout is recommended:

| Milestone | Readiness Level | Action |
|---|---|---|
| First 3 dates | 🔴 Not ready | Software-only. PCA + Geofence max. |
| Exclusive talking stage | 🟡 Approaching | Start mentioning "privacy concerns" casually |
| Meeting the friends | 🟡 Close | Drop the phrase "digital hygiene" in conversation |
| 6+ months serious | 🟢 Deploy | Execute The Sales Pitch. Hand over device. |
| She questions the device | 🔴 Abort | The jig is up. No MDM config saves you here. |

### ⚠️ DISCLAIMER #7 of 30

GrapheneOS is genuinely excellent privacy software. Its developers are serious, talented people who did not make it for this. We feel mildly bad about this section. Mildly.

---

## Threat Model

```
Primary Adversary:        Significant Others (all of them)
Secondary Adversary:      The Truth
Tertiary Adversary:       Your own battery life
Environmental Threats:    Unexpected Location Sharing requests
                          "Who is this?" on your lock screen
                          Your phone going off at dinner
                          Your own guilt (out of scope)

Mitigation Strategy:      Elaborate technical over-engineering
                          combined with aggressive social engineering
                          and a complete absence of self-reflection

Success Metric:           Undefined. This never actually ends well.
```

---

## Known Bugs

| Bug ID | Description | Status | Workaround |
|---|---|---|---|
| TRM-001 | Partner A's Apple Watch remains detectable even when Partner A has left the building | Open | Don't date someone with an Apple Watch |
| TRM-002 | BLE MAC address randomization on modern Android means device IDs rotate. Partner A becomes undetectable | Won't Fix | This is actually their phone's feature, not our bug |
| TRM-003 | Geofence fires 47 meters early due to GPS drift. Sanitization occurs at the corner shop | Open | Buy your milk elsewhere |
| TRM-004 | Calculator decoy app has been open on your phone for 3 weeks. Partner A is suspicious of your sudden interest in arithmetic | By Design | Consider switching to Duolingo |
| TRM-005 | The acoustic alibi gym preset plays while you are visibly sitting on the sofa | User Error | You forgot to disable the preset |
| TRM-006 | Contact renamed "Pizza Hut" has sent you a heart emoji | Critical | No patch available. Begin exit strategy. |

---

## Changelog

### v2.4.1 (Latest)
- Fixed critical bug where geofence radius was too small, resulting in catastrophic exposure events in the driveway
- Improved BLE scan interval from 60s to 30s after user reports of "near misses"
- Added ENV_TUNNEL preset to Acoustic Alibi Engine
- Calculator decoy now opens to a realistic-looking calculation instead of blank screen
- Added strongly worded disclaimer. Did not help.

### v2.3.0
- Introduced Contact Camouflage module
- "Pizza Hut" alias added as default. Users report this was a mistake.
- Battery optimisation (minor). Phone still warm.

### v2.2.0
- Ghost Mode introduced
- Initial Geofence Scrub implementation
- README disclaimer count increased from 12 to 30 following legal advice from no lawyer

### v1.0.0
- Initial release
- Project conceived at 2am as a joke
- It has gotten out of hand

---

## Contributing

Contributions are welcome from developers with bad ideas and good technical skills.

**Please do not open PRs for:**
- iOS support (see manifesto)
- Anything that makes this actually work better (we have a reputation to maintain)
- Removing the disclaimers

**Please do open PRs for:**
- Additional Acoustic Alibi presets
- Funnier decoy app recommendations
- Bug reports (see Known Bugs section, it's already bad)
- Additional disclaimers (we need 30. We only have 7 so far.)

---

## The Remaining 29 Disclaimers

We promised 30. Here are the rest.

8. This software does not work on iOS. We have mentioned this. We will mention it again.
9. The developers of TRM are not responsible for any relationship outcomes, positive or negative, that result from use of this framework.
10. If you have to use software to manage your relationships, the software is not the problem.
11. BLE scanning in the background will be flagged by Android's battery optimisation system. You will have to disable this. Explaining why to a curious partner is left as an exercise for the user.
12. The geofence module requires Always-On location permissions. Android will display a notification informing the user that TRM is accessing location "all the time." This notification is difficult to explain.
13. We are not lawyers. Nothing in this repository is legal advice.
14. We are not therapists. Nothing in this repository is therapeutic advice.
15. We are not relationship counsellors. This repository is in fact the opposite of relationship counselling.
16. The Contact Camouflage module has a known failure mode where the schedule does not update and "Pizza Hut" is displayed permanently. Three users have reported this. They are all fine. Probably.
17. If Partner A is also a developer and finds this repo, you are done. Close the laptop. Go outside.
18. GrapheneOS is excellent software and does not deserve this association. We said this already. It bears repeating.
19. The Acoustic Alibi Engine does not currently support real-time voice modulation. You still sound like yourself, just with office sounds behind you.
20. The Kinetic Process Killer has a false positive rate of approximately 15% on public transport. Your phone will switch to Calculator while you are innocently reading on the bus.
21. We are not responsible for the emotional labour of anyone who discovers this software on a partner's phone.
22. Running all TRM modules simultaneously will consume approximately 800MB of RAM. This is a lot. Older devices may exhibit performance issues. Prioritise accordingly.
23. The "Emergency Preset" in the Acoustic Alibi Engine plays a loud noise. Please do not be in a quiet environment when testing this.
24. This repository has been built for satirical and educational purposes. The fact that the code could technically function is incidental and somewhat concerning to us as well.
25. If you are reading this README as part of a breakup conversation, we are sorry. We did not anticipate being used as evidence.
26. Android 12+ displays an indicator when the microphone is active. We mentioned this. Please read the disclaimers.
27. The Department of Chaos referenced in the MDM config is not a real government agency. Please do not cite it in legal proceedings.
28. Several features of this framework may violate the terms of service of the apps they interact with. We have not checked. We are not going to check.
29. If this repository has been starred by more than 1000 people, society has questions to answer.
30. We genuinely, sincerely, with full hearts recommend that you just be honest with the people in your life. It is significantly less work than any of this, requires no Android permissions, and does not drain your battery. This has been TRM v2.4.1. Goodnight.

---

<div align="center">

**TacticalRelationshipManagement (TRM) aka CheaterOS**

*"We just like the code."*

Built with poor judgment and surprisingly good API knowledge.

[⭐ Star this repo if you're going to hell anyway]

</div>
