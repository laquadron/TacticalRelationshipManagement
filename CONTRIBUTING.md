# Contributing to TacticalRelationshipManagement (TRM)

> First of all: why are you here? Do you need to talk to someone?
> We're not therapists (see disclaimer #14) but we are listening.

Thank you for your interest in contributing to TRM. This is an open source project maintained by developers with questionable priorities and excellent API knowledge. We welcome contributions from the community, provided those contributions meet the standards outlined in this document.

Please read this guide fully before opening a PR. We have feelings.

---

## Table of Contents

1. [Code of Conduct](#code-of-conduct)
2. [What We Need](#what-we-need)
3. [What We Absolutely Do Not Need](#what-we-absolutely-do-not-need)
4. [How To Contribute](#how-to-contribute)
5. [PR Requirements](#pr-requirements)
6. [Commit Message Standards](#commit-message-standards)
7. [Issue Reporting](#issue-reporting)
8. [Use Case Requirements](#use-case-requirements)
9. [Review Process](#review-process)
10. [Recognition](#recognition)

---

## Code of Conduct

We maintain a respectful, inclusive environment for all contributors regardless of experience level, background, or current relationship status (which we are not judging, but we are quietly noting).

**You must not:**
- Be rude to other contributors
- Submit PRs without testing your code
- Open issues that are just "this is wrong" with no further context
- Submit iOS support. Not now. Not ever. Not in a branch. Not as a joke PR. No.

**You should:**
- Be kind
- Write tests
- Comment your code
- Reconsider your life choices (optional but recommended)

---

## What We Need

The following contributions are actively welcomed:

### 🎵 Acoustic Alibi Presets
New ambient audio environments for the `AcousticAlibiEngine`. Good candidates include:

- `ENV_HOSPITAL` — For when you need sympathy AND an alibi
- `ENV_AIRPLANE` — "I told you I had a work trip"
- `ENV_WEDDING` — Distant music, clinking glasses, someone else's happiness
- `ENV_FUNERAL` — The nuclear option. Use sparingly.
- `ENV_PARENT_HOUSE` — Awkward silences, TV in background, a dog

Please include:
- A 60-second seamless looping audio file (MP3, 128kbps minimum)
- A clear use case in the PR description
- A personal reflection on why you knew exactly what audio this situation needed

### 🐛 Bug Reports
See [Issue Reporting](#issue-reporting). We have many bugs. We are aware of most of them. We would like to be aware of all of them.

### 😂 Additional Disclaimers
We currently have 30 disclaimers. There is no upper limit. If you have thought of a scenario we have not disclaimed our way out of, please submit it. PRs adding disclaimers will be reviewed within 24 hours because honestly they are the best part.

### 🌍 Translations
The README in other languages. The humor must survive translation. If it does not survive translation, do not submit it. We will not accept a translated README that is less funny than the original. This is a hard requirement.

### 📱 Additional Decoy App Recommendations
The `KinetographicProcessKiller` currently supports a small list of decoy apps. We need more options for more scenarios. Please provide:
- App name
- Why it works as a cover
- What kind of person it implies you are
- Whether it has ever actually worked (honesty appreciated)

### 🧪 Tests
Actual unit tests for the Kotlin modules. Yes, we're serious about this one. The joke is funnier if the code works.

---

## What We Absolutely Do Not Need

The following will be closed immediately, possibly with a custom response:

| Contribution | Why We Don't Want It | Custom Response |
|---|---|---|
| iOS support | See the manifesto. Read it. | "No." |
| A PR removing disclaimers | They are load-bearing | "Absolutely not." |
| "Make it actually undetectable" | That's not the vibe | "Sir this is a joke repo." |
| Anything involving actual spyware | Hard no | Reported and blocked |
| A PR that "fixes" the Pizza Hut bug | It's not a bug | "It's not a bug." |
| Relationship advice in issue comments | We are not qualified | Closed with sympathy |
| A feature that makes the battery drain worse | It's already bad | "We know. We know." |

---

## How To Contribute

### Step 1: Fork the Repository

Fork TRM to your own GitHub account. If your GitHub profile is otherwise entirely serious and professional, we appreciate the chaos this will introduce to your contribution graph.

### Step 2: Clone Your Fork

```bash
git clone https://github.com/YOUR_USERNAME/TacticalRelationshipManagement.git
cd TacticalRelationshipManagement
```

### Step 3: Create a Branch

Branch naming convention:

```bash
# For features
git checkout -b feature/acoustic-alibi-funeral-preset

# For bug fixes  
git checkout -b fix/pizza-hut-alias-persistence

# For documentation
git checkout -b docs/disclaimer-additions

# For things that should not exist but here we are
git checkout -b cursed/ios-attempt
# (This branch will be deleted. But we respect the spirit.)
```

### Step 4: Make Your Changes

Write your code. Comment it. Test it. Sit with what you've done.

### Step 5: Submit a PR

Fill out the PR template fully. PRs with empty templates will be closed with a note that says "we can tell you didn't read CONTRIBUTING.md."

---

## PR Requirements

All pull requests must include:

### ✅ A Use Case

"I needed this" is **not** a use case.

"I needed this at 7pm on a Saturday when Partner A arrived 45 minutes early and the geofence hadn't triggered yet" **is** a use case.

Be specific. We are not here to judge. We are a little bit here to judge. But mostly we need context for code review.

### ✅ Test Coverage

All Kotlin modules must have corresponding unit tests. Yes, even the funny ones. Especially the funny ones. Nothing is funnier than a well-tested panic button.

```
Minimum coverage requirement: 70%
Ideal coverage requirement: High enough that you feel okay about this
```

### ✅ Updated Documentation

If your PR adds a feature, update the README. If your PR adds a module, add it to the architecture diagram. If your PR adds a disclaimer, update the disclaimer count in the README header. The number must always be accurate. This is the one thing we are strict about.

### ✅ A Comment Explaining The Funny

Every new module must contain at least one comment that acknowledges the absurdity of what the code is doing. This is not optional. It is a stylistic requirement. The codebase has a voice. Maintain the voice.

**Good:**
```kotlin
// Block the call. Technically this is a feature.
// Ethically this is complicated. But here we are.
callScreeningService.respondToCall(
    CallResponse.Builder().setDisallowCall(true).build()
)
```

**Bad:**
```kotlin
// Block call
callScreeningService.respondToCall(
    CallResponse.Builder().setDisallowCall(true).build()
)
```

See the difference. Feel the difference.

---

## Commit Message Standards

We follow a modified version of Conventional Commits. Modified in the sense that we also require emotional honesty.

### Format

```
<type>(<scope>): <description>

[optional body]

[optional footer]
[mandatory existential note]
```

### Types

| Type | When To Use |
|---|---|
| `feat` | New feature |
| `fix` | Bug fix |
| `docs` | Documentation only |
| `refactor` | Code change that neither fixes a bug nor adds a feature |
| `test` | Adding or fixing tests |
| `chaos` | You're not sure what this is but it felt right |

### Examples

```bash
# Good commit messages
git commit -m "feat(geofence): reduce trigger radius to prevent premature sanitization

Previously the geofence was firing 47 meters from the target location,
causing the browser history to clear while the user was still at the
corner shop. Radius adjusted to 50m with a 10m buffer.

This should have been caught in testing. It was not caught in testing.
We are thinking about what we did."

git commit -m "fix(contact-camouflage): Pizza Hut alias now correctly reverts at 09:00

It was not reverting. It had not been reverting for three weeks.
Three users were affected. They know who they are."

git commit -m "docs(disclaimer): add disclaimer #31 re: Calculator suspicion

Users are reporting that Calculator as a decoy app is raising more
suspicion than the original concerning app. This has been documented.
No fix is planned. A disclaimer has been added."

git commit -m "chaos(acoustic-alibi): add ENV_FUNERAL preset

I don't want to talk about why I knew exactly what this should
sound like. The preset works. Please just merge it."
```

---

## Issue Reporting

Before opening an issue, please check:

1. Is this actually a bug, or did you just not read the README?
2. Have you checked the Known Bugs table in the README?
3. Is the issue "this doesn't work on iOS"? Because that's not an issue. That's the point.

### Issue Template

```markdown
**Describe the bug:**
[What happened]

**Expected behavior:**
[What you expected to happen]

**Actual behavior:**
[What actually happened, including any exposure events that resulted]

**Device:**
[Make, model, Android version. If you say iPhone we will close this immediately.]

**Were you detected?**
[ ] Yes
[ ] No  
[ ] Partially, but I talked my way out of it
[ ] The geofence saved me
[ ] The geofence did not save me

**Additional context:**
[Anything else. We are not judging. We are a little bit judging.]
```

### Issue Labels

| Label | Meaning |
|---|---|
| `bug` | Confirmed technical issue |
| `by-design` | Working as intended, unfortunately |
| `pizza-hut-related` | The alias is stuck again |
| `touch-grass` | The issue is not technical |
| `ios-adjacent` | Closed. |
| `critical` | Active exposure event reported |
| `existential` | The issue raises questions we are not prepared to answer |

---

## Review Process

PRs are reviewed by maintainers within a reasonable timeframe. "Reasonable" is defined loosely given that this is a joke repo maintained by people with day jobs and, apparently, complicated personal lives.

### Review Criteria

Your PR will be evaluated on:

1. **Does the code work?** This is still a real criterion. We have standards. They are low, but they exist.
2. **Does it maintain the voice?** Read the existing comments. Match the energy.
3. **Is the use case believable?** Even in a satirical context, the scenarios should be grounded in the kind of chaos that actually happens to real people.
4. **Does it make things worse in a funny way?** This is the highest form of contribution.
5. **Did you add a disclaimer?** You should add a disclaimer.

### Approval Requirements

- 1 maintainer approval for documentation changes
- 2 maintainer approvals for code changes
- Unanimous approval for anything that makes the battery drain worse
- A brief moment of silence for anything touching the Pizza Hut alias

---

## Recognition

Contributors will be added to the `HALL_OF_CHAOS.md` file (coming soon) with their contribution noted.

Contributor tiers:

| Tier | Requirement | Title |
|---|---|---|
| 🥉 Accomplice | First merged PR | "Technical Accomplice" |
| 🥈 Architect | 5+ merged PRs | "Chaos Architect" |
| 🥇 Partner In Crime | 10+ merged PRs | "Senior Partner In Crime" |
| 💀 Legend | Merged the iOS PR we said we'd never merge | "This Has Never Happened" |

---

## Final Note

If you have read this entire document, you are either a very thorough developer or you are procrastinating on something important.

Either way, welcome. We're glad you're here. Please write good tests.

And for the love of everything, stop trying to submit iOS support.

---

*TacticalRelationshipManagement (TRM) aka CheaterOS*
*"We just like the code."*
