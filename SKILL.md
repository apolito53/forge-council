---
name: forge-council
license: MIT
description: Convene genuinely independent coding agents and a fresh judge to deliberate on a difficult engineering or software architecture decision. Use for explicit ForgeCouncil requests, multi-agent design consensus, or an adversarial architecture review before implementation. Not for routine coding, ordinary code review, or DreamLoop visual judging.
---

# ForgeCouncil

Produce an evidence-backed design decision through **independent specialist proposals, adversarial cross-review, and an independent judge**. A single model presenting several voices is not a council.

## Scope and permissions

- Treat a council request as **design review only**, unless the user separately authorizes implementation. Do not edit production code, create a PR, merge, deploy, change infrastructure, or spend money as part of deliberation. Save a review artifact in the repository only when requested.
- Respect the user's actual scope, constraints, time or cost budget, and project instructions. Avoid turning a small feature into a platform rewrite.
- Inspect the live repository state before dispatch: project guidance (including `AGENTS.md`), relevant source/tests, main or base SHA, active feature branch and PRs, current interfaces, and relevant performance evidence. Freeze one common brief with the inspected revision and known unknowns. Never deliberate from a remembered stale checkout.
- Choose the smallest worthwhile council. Default to **three specialist reviewers and one fresh judge** for substantial cross-system choices; adapt the disciplines or number when the task justifies it. Prefer one bounded review round over perpetual debate.

## Actual independence is mandatory

Use native subagent/delegation capabilities, or genuinely separate Codex agent invocations with isolated contexts, when available. Parallel execution is helpful but not mandatory. Give each reviewer the same frozen problem statement and relevant repo revision plus only its role-specific focus. **Do not share initial proposals between reviewers before the blind round closes.** Do not ask one model to simulate three independent reviewers or act as its own "fresh judge."

If independent agent invocations are unavailable, **say so before claiming to convene a council**. Offer a ready-to-run council brief for an agent-capable environment, or clearly label a single-model multi-perspective review as a fallback. Never fabricate reviewer identities, exchanges, votes, consensus, or tool results.

## Deliberation protocol

1. **Freeze the brief.** State the decision to make, user-facing success criterion, scope exclusions, compatibility invariants, likely risks, repository revision, available tests, and performance/security constraints. Distinguish verified facts from assumptions. Use the *same* baseline for every reviewer.
2. **Blind independent proposals.** Dispatch domain-appropriate specialists. For an interactive game feature, physics/rendering, navigation/runtime authority, and gameplay/UX/reliability are useful defaults, not universal roles. Each agent must inspect relevant code independently and return:
   - The recommended design and at least one credible alternative, including a deliberately simpler approach if viable.
   - Concrete integration points with repository paths and symbols; distinguish inspected evidence from inference.
   - State ownership and interfaces, lifecycle/reset behavior, failure modes, performance implications, and minimal acceptance tests.
   - Specific objections to its own proposal and questions it cannot resolve from current evidence.
3. **Adversarial cross-review.** Share the anonymized initial proposals with the reviewers only after all have reported. Ask each to identify the strongest correctness, scope, performance, or integration objection to competing approaches. Require specific evidence or an executable verification experiment, not rhetorical disagreement. Allow **one concise revision** from each reviewer after seeing the critiques.
4. **Fresh independent judge.** Launch a separate judge with the frozen brief, original proposals, cross-reviews, revisions, and references. Ask it to independently spot-check decisive source claims, challenge common assumptions, compare viable designs, and select the smallest defensible solution. A judge may select a hybrid, request one narrow experiment, return a conditional decision, or block the proposal. Do not turn a majority vote into proof of correctness.
5. **Resolve and stop.** Reconcile the judge's verdict with material technical dissent. If a blocker depends on untested behavior, label it **unresolved** and specify the next test, rather than claiming consensus. Stop after the judge's ruling unless an essential blocker requires one bounded follow-up or the user requests another round.

## Decision criteria

Weight correctness and player/user-visible value first, then compatibility with existing architecture, deterministic or network authority semantics where applicable, safety, measurable performance, maintainability, testability, and delivery cost. Preserve established optimizations unless evidence supports replacing them. Favor minimal vertical slices over speculative generalized infrastructure.

Demand explicit answers when a proposed change crosses boundaries: **Who owns the state?** How does physical/rendered behavior agree with navigation or authoritative logic? What happens on reset, failure, pause, reconnect, and completion? How is the design proven without relying on an attractive demo alone?

## Final council record

Deliver a compact but auditable verdict in the conversation. Include:

- **Identity:** Council name/number if supplied, decision, repository revision, and actual reviewers/judge invoked (with model or session identifiers when available). Mark absent agents honestly.
- **Independent positions:** Each proposal's core idea, evidence, benefits, objections, and changed position after cross-review.
- **Contested points:** The strongest disagreements, how they were resolved, and any minority dissent or unverified claims.
- **Verdict:** **Accepted**, **Conditional**, or **Blocked**, with rationale, chosen design and rejected alternatives. Consensus means objections were addressed, not that everyone was pressured to agree.
- **Buildable plan:** Concrete affected modules/contracts, smallest implementation sequence, migration or rollback concerns, focused tests, measurable performance checks, and a player-visible acceptance criterion.
- **Boundary:** What was inspected, tested, and *not* tested. Confirm whether any files or external systems were changed. Do not imply the design has been implemented.

When a persistent record is requested, put the verdict in an appropriate existing project decisions/reviews location and retain agent provenance. Never silently alter source code to make a judge's recommendation look complete.

## Reviewer prompt core

Supply this unchanged shared brief to each separate reviewer, followed by its specialty:

> Work independently and read-only at the specified repository revision. Inspect actual source, not recollection. Propose the smallest technically credible design, a viable alternative, tradeoffs, failure modes, and a focused verification plan. Cite files/symbols for decisive facts, label assumptions, and argue against your own proposal. Do not implement or read other reviewers' answers during this first round.

The judge receives a separate instruction:

> Independently evaluate the frozen brief, original proposals, peer critiques, and revisions. Verify key disputed claims when possible. Choose a defensible design without forced unanimity; preserve material dissent and blocking unknowns. Return concrete interfaces, implementation milestones, acceptance tests, and the evidence boundary. You are the judge, not the implementation agent.
