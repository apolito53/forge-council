# ForgeCouncil ⚒️

**Independent engineering proposals. Adversarial cross-review. A fresh judge. One buildable decision.**

ForgeCouncil is a reusable [agent skill](https://agentskills.io/) for difficult software engineering and architecture decisions. Instead of having one coding agent produce a confident answer, it asks *genuinely separate* specialist agents to investigate the same problem independently, critique one another's proposals, and submit the evidence to a fresh judge.

The goal is **a small, defensible implementation plan**, not consensus for its own sake or another elaborate architecture nobody asked for.

## What it does

- **Freeze the brief:** inspect the relevant code and project constraints at a specific repository revision.
- **Independent proposals:** typically three specialists, with blind initial reviews and credible alternatives.
- **Cross-review:** exchange proposals after the blind round and challenge assumptions, correctness, performance, and scope.
- **Fresh judge:** a separate agent verifies key disputed claims and chooses an accepted, conditional, or blocked design.
- **Implementation handoff:** produce explicit interfaces, integration points, acceptance tests, remaining risks, dissent, and evidence boundaries.

The specialists are chosen for the problem. A game-engine task might use physics, navigation, and gameplay reviewers; a backend problem might use database, security, and reliability reviewers. ForgeCouncil is not specific to games.

## Installation

With a coding agent that supports skills, install from this public GitHub repository:

```sh
npx skills add apolito53/forge-council
```

Or clone/copy the repo into your coding agent's skills directory. For Codex, a common user-level location is `~/.codex/skills/forge-council/`. Restart or begin a fresh agent session if the skill isn't picked up immediately.

## Prerequisites

You need a coding agent that can inspect your project and **actually delegate work to separate agent invocations**. For the full process, a fresh agent invocation is also needed for judging. Parallel runs help but aren't essential.

**No fake councils:** if independent agents are unavailable, the skill must say so and provide a runnable review brief or a clearly labeled single-agent alternative. It must not invent identities, votes, verdicts, or consensus.

## Example

```text
$forge-council Review the architecture for a security gate in my game.
Three specialists should independently examine physics/collision,
AI navigation, and gameplay interaction. Cross-examine the proposals,
then ask a fresh judge for the smallest safe implementation plan.
Design review only; do not modify production code.
```

Other examples: evaluate a database migration strategy, compare authentication architectures, review a caching redesign, or select a real-time collaboration approach.

## What comes back

A council record identifies who really participated, the repository revision reviewed, each independent proposal, the strongest objections, any unresolved disagreement, and the judge's **Accepted / Conditional / Blocked** verdict. It ends with a concrete implementation sequence and verification criteria, including what was *not* tested.

**Review is read-only by default.** Publication, code edits, deployment, spending, and implementation are separate user-authorized activities.

## Contributing

Feedback and issue reports are welcome. If proposing changes to the review process, please explain how they improve independence, auditability, efficiency, or the quality of engineering decisions. Example council records with private identifiers and secrets removed are especially helpful.

## License

[MIT](LICENSE). Inspired by the value of independent critic workflows demonstrated by [DreamLoop](https://github.com/achimala/dream-loop), but focused on engineering decisions rather than visual matching.
