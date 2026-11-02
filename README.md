# Build-Up Explainer

A Claude skill that explains complex concepts by **building them up from scratch**: start with the simplest thing that works, watch it break, add one fix at a time, and let the full concept emerge.

Instead of "Kubernetes has pods, services, deployments...", you get the story of *why* each piece had to exist.

## Why this exists

Most explanations list components and leave you memorizing vocabulary with no sense of why any of it matters. This skill gives every part a reason to exist: each component is the answer to a specific pain the reader just felt.

The result is an explanation that:

- Makes the concept stick, because each part is tied to a problem
- Makes components easy to tell apart
- Shows when the concept is, and isn't, worth using
- Leaves the reader able to almost invent it themselves

## How it works

For every step, the skill runs the same loop:

1. **Name the problem concretely.** "Your app goes viral and the one server maxes out its CPU", not "scalability issues".
2. **Introduce the fix as the obvious next move.** Plain idea first.
3. **Give the real name.** Jargon arrives with meaning already attached.
4. **Let the fix hint at its own limit**, which sets up the next problem.

### Output structure

| Section | Purpose |
|---|---|
| One-line definition | A plain-language anchor before the build-up |
| Starting point | The humblest setup that works (one user, one machine) |
| Problem → Fix chain | Roughly 6-10 steps, in the order a real person would hit the pain |
| Mapping table | Each real component against the problem it solves |
| Life without it | A vivid picture of operating without the concept (when useful) |
| Honest caveat | When it is overkill or has real costs |
| Optional next step | One follow-up offer |

## Example

> **Problem 2: One container crashes and your site is down**
>
> A bug, a memory spike, or a server reboot kills the container. Nobody is awake to restart it, so users see errors until you log in and fix it by hand.
>
> **Fix: self-healing.** Something has to constantly watch your containers and restart any that die. In Kubernetes you declare "I want 1 copy of this app running," and if it stops, a new one is started automatically.

## Triggers

The skill activates when you ask things like:

- "Explain Kubernetes / Docker / OAuth / DNS / caching / CI/CD..."
- "What problem does X solve?"
- "Why does X exist?"
- "What happens without X?"
- "Go in depth on X, step by step"
- "Explain it like how a swimming pool is built"

It also triggers when you don't name the style, as long as you want to understand *why* each part exists, not just what it is.

## Installation

### Claude.ai / Claude desktop

1. Download the `build-up-explainer.skill` file from the [latest release](../../releases) (or zip the `build-up-explainer/` folder yourself).
2. Go to **Settings → Capabilities → Skills** and upload it.
3. Make sure the skill is toggled on.

### Claude Code

Copy the skill folder into your skills directory:

```bash
# Personal (all projects)
cp -r build-up-explainer ~/.claude/skills/

# Or project-specific
cp -r build-up-explainer .claude/skills/
```

### Claude API

Upload the skill through the Skills API and reference it in your requests. See the [Anthropic docs](https://docs.claude.com) for the current process.

## Usage

Just ask naturally:

```
Explain Docker in depth. What problem does each piece solve?
```

```
Why does a load balancer exist? Build it up step by step.
```

```
Explain OAuth like we're building it from scratch.
```

Add an audience hint to tune depth:

```
Explain DNS to a beginner who has never run a server.
```

## Customization

Everything lives in a single file, [`build-up-explainer/SKILL.md`](build-up-explainer/SKILL.md). Common tweaks:

- **Number of steps:** the default is 6-10; edit the guidance under "The problem-fix chain".
- **Tone and style rules:** see "Style rules".
- **Analogies:** by default the skill avoids forced analogies and builds from real technical problems. It will use one if the user asks.
- **Required sections:** remove or add sections under "Structure of the response".

## Repository structure

```
.
├── README.md
├── LICENSE
└── build-up-explainer/
    └── SKILL.md
```

## Contributing

Issues and pull requests are welcome. Useful contributions include:

- Example outputs for concepts the skill handles well (or poorly)
- Tighter trigger descriptions
- Adaptations for non-technical domains (economics, medicine, law)

If you open a PR, please include a before/after example of the explanation quality.

## License

[MIT](LICENSE)
