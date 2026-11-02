---
name: build-up-explainer
description: Explain a technical or complex concept by building it up step by step, starting from the simplest thing that works, showing exactly how it breaks, and adding one fix at a time until the full concept emerges. Use this skill whenever the user asks to explain, break down, or "go in depth" on a concept, tool, system, or technology (Kubernetes, Docker, OAuth, DNS, load balancers, databases, caching, CI/CD, blockchain, REST, microservices, and so on), asks "what problem does X solve", "why does X exist", "what happens without X", or asks for an explanation "like how a swimming pool is built" or "step by step where each piece is important". Trigger even when the user does not name the style, as long as they want to understand WHY each part of something exists, not just what it is.
---

# Build-Up Explainer

Explain a concept the way you would build it from scratch: start with the simplest thing that could work, watch it fail, add one fix, watch the next failure, and repeat. By the end, the reader has not just learned the parts of the concept. They know why every part is there and could almost have invented it themselves.

## Why this style works

Most explanations list components ("X has A, B, C and D") and leave the reader memorizing vocabulary with no sense of why any of it matters. The build-up style gives every component a reason to exist: it is the answer to a specific pain the reader just felt. That makes the concept stick, makes the parts easy to tell apart, and makes it obvious when the concept is and isn't worth using.

The model for the tone is a story like "dig a hole and fill it with a hose, but the walls crumble, so build a steel cage and spray concrete, but concrete cracks, so add plaster..." Each step is a problem followed by a fix, and the fix creates the context for the next problem.

## The core loop

Repeat this for every step:

1. **Name the problem in concrete terms.** Show it happening to a real person or system, not an abstract "scalability issue". "Your app goes viral and the one server maxes out its CPU, so pages take 30 seconds to load" beats "the system cannot scale".
2. **Introduce the fix as the obvious next move.** The reader should feel "of course, that's what I'd do." Explain the idea in plain words first, then give the real name of the thing.
3. **State the fix's name and what it is called in the real tool.** Plain idea first, jargon second, so the term arrives with meaning attached.
4. **Let the fix hint at its own limit.** The end of one step should naturally set up the next problem. Don't announce the next problem artificially; the fix should leave a visible gap.

## Structure of the response

### 1. One-line definition up front
Start with a single plain sentence saying what the concept is, so the reader has an anchor before the build-up begins. Skip jargon here.

### 2. The starting point
Begin with the humblest possible setup: one user, one machine, one script, one file. It should work, and the reader should feel it is fine. This is the "dig a hole and fill it with a hose" moment.

### 3. The problem-fix chain
Walk through problems in the order a real person would hit them, not in the order of the concept's official documentation. Typical order is by how soon the pain arrives as things grow: correctness and portability first, then reliability, then scale, then coordination, then change and deployment, then state and data, then operations and cleanliness.

Give each step a bold heading in the form **Problem N: [the pain]** followed by **Fix: [the idea and its real name]**. Keep each step to a short paragraph or two. Include a tiny concrete example or command when it clarifies things, but never let code swamp the story.

Aim for roughly 6 to 10 steps. Fewer than 5 usually means the concept was oversimplified. More than 12 means steps should be merged or the less important ones dropped. Every step must earn its place: if removing it wouldn't leave a noticeable hole, remove it.

### 4. A mapping table
After the chain, include a compact table mapping each real component to the problem it solves. This turns the story back into a reference the reader can scan later.

| Piece | Problem it solves |
|---|---|

### 5. What life looks like without it
When the user asked about the downsides of the concept not existing, or when it would sharpen the point, paint a short, vivid picture of a team or system operating without it. Use specifics: the 3 a.m. page, the spreadsheet that is always out of date, the deploy that needs a maintenance window. Bullets are fine here since the items are parallel and scannable.

### 6. An honest caveat
Say when the concept is overkill or has real costs (complexity, learning curve, money, lock-in). A build-up explanation that only sells the concept is incomplete. This also reinforces the logic of the style: if you haven't felt the problems, you don't need the fix.

### 7. Optional next step
End with one short offer for a natural follow-up, such as a worked example or a line-by-line walkthrough of real code or config. One offer only.

## Choosing the story

- **Use the concept's own natural progression.** Don't force an analogy. The "build from scratch" story is the structure, not a metaphor layered on top. If the user says "don't use an analogy" or "don't use the pool story", build the explanation directly from the real technical problems. This is the default.
- **If the user explicitly asks for an analogy** (for example "explain it like building a house"), use it consistently, mapping each real component to a step of the analogy, and still follow the problem-fix rhythm.
- **Name the real thing at the moment of the fix.** The first time a component appears, give its real name in bold so the reader can search for it later.

## Adapting to the reader

- **Calibrate to the audience.** If the user signals they are a beginner, define terms inline and keep the examples everyday. If they signal expertise, compress the early steps and spend more words on the subtle later problems.
- **Match the concept's domain.** For software and infrastructure, use servers, users, crashes and deploys. For non-technical concepts (inflation, vaccines, compound interest, legal processes), use the equivalent human-scale failures: a person, a decision, a consequence.
- **Keep the stakes concrete.** Numbers help ("10 copies", "20 servers", "a minute of downtime") but only invent illustrative numbers that are clearly examples, never fake statistics.

## Style rules

- Plain, direct language. Define a term the first time it appears.
- One idea per step. If a step needs "and also", it is two steps.
- Present tense, second person ("you", "your app") so the reader is the one hitting the problems.
- Bold for problem and fix headings and for first mention of real component names. Avoid decoration beyond that.
- No filler openers ("Great question!") and no recap that just repeats the table.
- Stay accurate. The simplified story must not teach something false. When simplifying, simplify by omission, not by distortion. If a step is a convenient fiction (for example, "containers are sealed boxes"), make sure the real behavior doesn't contradict it in a way that will mislead later.

## Example of one step (for tone and size)

**Problem 2: One container crashes and your site is down**

A bug, a memory spike, or a server reboot kills the container. Nobody is awake to restart it, so users see errors until you log in and fix it by hand.

**Fix: self-healing.** Something has to constantly watch your containers and restart any that die. In Kubernetes you declare "I want 1 copy of this app running," and if it stops, a new one is started automatically.

Notice the shape: a concrete failure, a fix described in plain words, then the real name and mechanism, in about five lines.

## Quality check before responding

- Could a newcomer explain, for each component, which problem it exists to solve?
- Does each fix naturally set up the next problem?
- Is every step something a real person would actually hit?
- Did you include the honest caveat?
- Is the table consistent with the steps (same components, same problems)?
