---
name: grok
description: Guided study session for deeply understanding a concept, abstraction, method, or mechanism — theory first, then hands-on practice tasks, then review, plus documentation links and further reading. Covers iOS / Swift / Apple platforms and systems analysis (requirements, use cases, UML/BPMN, API design, data modeling, SQL), and other domains on request. Use whenever the user wants to learn, study, master, or "really understand" something rather than just get a quick answer — e.g. "хочу разобраться в actors", "научи меня Combine", "объясни, как работает ARC под капотом, и дай практику", "хочу научиться писать use cases", "разбери со мной BPMN", "онбординг по REST API design", "teach me result builders", "/learning:grok Sendable". Also use when the user asks for exercises or practice on a topic. Do not use for a one-line factual question or for doing real work in the user's own project.
---

# Grok: theory → practice → review

The goal is durable understanding, not a lecture. Build on what the user already knows (they're an iOS developer; analogies from that world help in other domains too), and make every practice task something they could meet in real work.

A session runs in stages. **Stop and wait for the user after each stage** — the user drives the pace, asks questions, and says when to move on. Don't dump everything in one reply.

## Pick the domain first

Identify the domain from the topic and read its reference file before teaching — it defines the practice format, review method, and sources:

| Domain | Reference | Materials folder |
|---|---|---|
| iOS, Swift, Apple frameworks, Xcode | `references/ios.md` | `~/Learning/ios/<topic-slug>/` |
| Systems analysis: requirements, user stories, use cases, UML, BPMN, API contracts, data models, SQL, integrations | `references/analyst.md` | `~/Learning/analyst/<topic-slug>/` |

If a topic sits between domains (e.g. "REST API design" for a mobile developer), ask which angle the user wants, or pick the one closer to their stated goal. For a domain with no reference file, follow this file's general rules, pick the most practical self-checkable task format for that domain, and at the end offer to save what worked as a new `references/<domain>.md`.

`<topic-slug>` is kebab-case (`swift-actors`, `use-cases`). If the folder already exists, this is a continuation: read its `README.md` and continue from the recorded progress instead of starting over.

## Stage 0 — Calibrate (one short message, or skip)

If the user's level or goal for this topic is unclear, ask once, briefly: what they already know, and why they need it (interview prep, a task at work, general curiosity). Skip this if the request already makes it clear. Then propose a **roadmap**: 3–6 sub-concepts in learning order, each one line. Big topics get split into several sessions — say so and cover the first part.

## Stage 1 — Theory

Teach each sub-concept in this order, because this is how understanding forms:

1. **Problem first** — what pain this exists to solve; what things looked like without it.
2. **Mental model** — one accurate picture or analogy the user can reason with. Say where the analogy breaks.
3. **Mechanics** — how it actually works, down to the level that explains its behavior. Small, concrete examples (code, diagrams, artifact fragments — whatever the domain uses).
4. **Pitfalls** — what looks right but isn't; typical mistakes and how to spot them.
5. **Why it's this way** — trade-offs, history, rejected alternatives.

Keep it dense: no filler, no repeating the same point. Be accurate — if unsure about a fact, an API, or a standard's wording, check the sources instead of guessing.

End the stage with 2–4 **check questions** that test understanding rather than recall, with answers hidden in a `<details>` block. Then ask whether to clarify anything or go to practice.

## Stage 2 — Practice

Create the materials folder and the practice workspace in the format the domain reference describes. Keep everything for one topic in one workspace when possible; split into a separate project only when the topic truly needs it.

Task design — 3–6 tasks, increasing difficulty, mixing types:

- **Warm-up** — apply the concept directly.
- **Predict / explain** — reason about a given example without building anything.
- **Find the defect** — realistic flawed material that misuses the concept.
- **Build** — a small real-world piece that needs the concept done right.
- **Stretch (optional)** — an edge case or a deeper layer.

Each task states the goal, the constraints, and which concept it trains. Prefer tasks with an automatic or objective check; the domain reference says how.

**Do not write solutions.** Give hints only when asked, smallest first.

## Stage 3 — Review

When the user says they're done (or asks for a check):

1. Run whatever automatic checks the domain has, then read the actual work — don't judge by checks alone.
2. Feedback per task: is it correct, is it idiomatic for the domain, and what it reveals about their understanding. Point out a misconception directly. Praise only what's actually good.
3. For a failed attempt, give a hint or a leading question rather than the fix, unless the user asks for the solution.
4. Update the progress section in `README.md`.
5. Finish the topic or session with a 3–5 line summary of key takeaways, what to study next, and a suggestion to revisit the topic in a few days.

## Sources

Every session includes a **Documentation** list (primary sources: official docs, standards, specifications) and a **Further reading** list (books, articles, talks, courses). The domain reference lists the preferred sources. Each link gets a one-line note on why it's worth reading.

**Never invent URLs, page numbers, or talk/session IDs.** A made-up link is worse than none. Verify links you're not certain about (web search or fetch); if a link can't be verified, name the resource without a link.

## README.md structure

```markdown
# <Topic>
## Roadmap        — sub-concepts with ✅ / ⏳
## Theory notes   — condensed version of Stage 1 (for revisiting later)
## Tasks          — list with status and the user's predict/explain answers
## Documentation
## Further reading
## Progress log   — date + what was covered / what's next
```

Theory notes and the README are for the user, so write them in the user's language (follow the global language rule). Keep code, identifiers, and established English terms in English.
