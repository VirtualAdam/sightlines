---
layout: default
title: "Standups Are Broken: Rethinking Team Sync in the Age of AI Coding"
description: "A practical approach to maintaining shared context when your codebase changes faster than your team can follow"
---

*A practical approach to maintaining shared context when your codebase changes faster than your team can follow*

---

## The Day Everything Changed

In November of 2025, I wrote 30,000 lines of code in a single day.

Not alone, of course. I was collaborating with an AI coding assistant. In my case, I was using [Amplifier](https://github.com/microsoft/amplifier), a modular developer assistant that makes it easy to wire up repeatable "workflows" around your repo.

In traditional development, 30,000 lines might represent months of work across a small team. Now it was a Tuesday.

Although happy with the productivity boost, and extremely happy with my new feature, I realized something uncomfortable: our processes aren't built for this pace of development.

---

## The Problem with Standups

In traditional Agile development, standups work because of shared context. When you have a small team of developers and a PM, everyone is close enough to the codebase (and each other) that three sentences of status actually mean something:

> "I'm finishing the user authentication flow. Blocked on the API spec from backend. Should be done by EOD."

Everyone nods. They understand the auth flow, the API dependency, and the tradeoffs that got you here.

But what happens when AI-assisted development compresses weeks of work into a day? What happens when you come back from a week-long vacation and the codebase has transformed so completely it might as well be a different project?

Shared context evaporates. Those three sentences become meaningless without a 30-minute preamble explaining what changed.

Standups aren't the root problem. Shared context is. Standups are just the ceremony most dependent on it.

---

<img src="/sightlines/bearings/images/context-stack/CAT_status_update.png" alt="Alice's agent shares a status update with Bob's agent. The agents work to include the architectural and health context required to understand the status." width="70%">
## A Different Kind of Handoff

I started thinking about this differently. Instead of humans trying to maintain context through conversation, what if we created artifacts that preserved context automatically?

The idea is simple: at every commit, your AI assistant writes a short, agent-readable artifact that captures the direction and pace of the work. I call it **CAT.md** (Current Active Trajectory) - a snapshot of intent, progress, and blockers that anyone (including future you) can use to rehydrate context quickly.

Then, when someone else pulls your branch, or when you come back to your own cold feature branch, their AI assistant can read these artifacts and explain the full situation with the required context.

Instead of asking a teammate:

> "Hey, where did you leave off on the auth vulnerability fix?"

And getting:

> "I'm almost done. Just need to finish the token refresh logic."

Your AI assistant reads the CAT and gives you:

> "The auth vulnerability remediation is about 80% complete. We're replacing the legacy API key/secret pattern with OAuth 2.0 client credentials flow. The token acquisition and caching are done and tested. Currently blocked on getting the new OAuth app registered in the production identity provider. The immediate next step is implementing the token refresh logic, and we'll know it's done when the integration tests pass against the staging environment. Two decisions to know about: we chose to cache tokens in memory rather than Redis to avoid adding infrastructure, and we rejected using the implicit grant flow because it's deprecated for server-to-server auth."

That's the kind of context that makes collaboration possible at the new pace of development.

---

## The Mental Model: System Design, Health/Maturity, Trajectory

This pattern works because it treats shared context as a set of complementary artifacts, each answering a different question:

- **ARCHITECTURE.md is your system design:** the map of what the software is, how it's shaped, and why it's built that way.

- **TEST_REPORT.md gives you the health:** the health and maturity of the system: what's passing, what's failing, and what level of coverage we have.

- **CAT.md is your trajectory:** a vector showing where the work is headed and how quickly it's moving, expressed in concrete deltas, blockers, and next steps.

When those three stay current, you can understand the terrain, trust the health reading, and see the direction of travel, without needing a standing meeting to reconstruct it all from memory.

---

## How It Works in Practice

The workflow has two key moments.

### Before you commit

You run the prompt '/cat-update' which directs your AI assistant to update the architecture, test report, and CAT in sequence. Each captures a different slice of context: how the system is shaped, whether it's healthy, and where the work is headed.

The goal is not "more documentation." The goal is diffable, commit-linked context.

### After you pull

You run the prompt '/status' which directs your AI assistant to read those artifacts and synthesize them into a narrative, not a template dump, but an actual story:

- what the project does,
- what changed recently,
- what matters right now,
- what's next,
- what's blocked,
- and what might surprise you when you open the code.

---

## This Isn't Just for Teams

This pattern is useful for solo developers too.

We all have feature branches that go cold. We all context-switch between projects. We all come back to code after a weekend and think: *what was I doing here?*

Having your AI assistant update CAT.md before you step away, and read it back to you when you return, is like leaving yourself a really good note, except you don't have to write it and it includes the details you would have forgotten to mention.

---

## Living Documentation

The key insight is that these artifacts stay current as a side effect of the workflow, not as a separate documentation chore. When you run `/cat-update`, the prompts cascade: architecture, then test report, then CAT. You get diffable, commit-linked context without adding a "documentation step" to your process.

---

## A Humble Offering

This is *an* approach, not *the* approach. The challenge of maintaining shared context in AI-assisted development is new, and there will be many solutions.

Maybe your team will use something like this. Maybe you'll build something better. Maybe the tooling will evolve to make this unnecessary. I don't know.

What I do know is that the old ceremonies need to evolve. Standups, sprint reviews, the hallway conversations that used to keep teams aligned: all of them need to adapt.

The pace of development has changed. The volume has changed. The way we build software has changed.

Our processes for staying in sync need to change too.

---

## Want to Try It?

I open-sourced the prompt library I'm using so you can drop it into a repo and adapt it to your team's workflow. The README covers setup and usage.

**[Context-Stack on GitHub](https://github.com/VirtualAdam/Context-Stack)**

If you're curious about the CLI workflow I used to drive this, check out **[Amplifier](https://github.com/microsoft/amplifier)** as well.
