---
layout: post
title: "PyCon Lithuania 2026 Notes"
---

These are my key takeaways distilled from talks, side discussions, and patterns that kept repeating.

## Software engineering is shifting from code to systems thinking
- Code is no longer the main asset, solutions are, “Code → test → refactor” still matters, but now
maintenance > writing
- Great engineers delete more than they write
- Specification is the source of truth before, during, after coding
- Reverse engineering from code alone is no longer viable
- The job is evolving from writing code to designing systems that survive AI
  
## AI doesn’t replace engineering, it amplifies it
- AI makes good practices better — and bad practices catastrophic
- “Vibe coding” ≠ software engineering
- AI-generated code often not maintainable, poorly understood, creates hidden technical debt
- Better to be 2–3× faster sustainably, not 10× faster and unmaintainable
  
## Documentation became critical infrastructure
- “The code is the documentation” → no longer true
- AI cannot see invisible context, if you don’t document, future engineers (and AI) will fail
- Keep docs close to code (plain text), document decisions, not just code
- Good docs today → better AI outputs tomorrow
  
## The real bottleneck is no longer coding — it’s maintenance
- Writing code is cheap
- Maintaining systems is expensive
- New reality is that code is an output, not an input
- Systems decay faster due to AI speed
- Companies must track technical debt and track AI-generated debt
- We can build anything” → now replaced with → “What should we NOT build?”
  
## Fundamentals matter more than ever
- Despite all the AI you still need infrastructure, understanding, system design thinking, debugging skills
- Hiring is shifting - less focus on output, more on process and reasoning
- Abstraction is rising — but fundamentals are the only anchor

## AI is a social shift, not just a technical one
- Adoption is uneven: juniors → heavy usage, seniors → cautious, but reviewing AI output
- Companies now define AI budgets, AI strategies
- Some trends: middle management questioned, smaller teams by default, more remote work
- AI is behaving more like electricity than a tool

## Risk, security, and regulation are catching up (slowly)
- Key risks: data leakage (GDPR), automation bias (“death by GPS”), overconfident AI outputs
- Best practices: never use production data → use Faker
- Sandbox everything
- Implement guardrails before/after LLM use
- Inform users instead of silently blocking
- Important idea: technology is not forbidden — its usage is

## Agents are the new computing model
- The focus is shifting to memory management, tool orchestration
- Constraints are that context windows are limited
- More context ≠ better results
- Patterns emerging: multi-agent systems, model-as-a-tool (LLMs calling LLMs), disposable sub-agents
- We’re moving toward software factories run by agents

## The uncomfortable truth about AI
- Productivity gains don’t equal production impact
- Many AI-built features never ship
- Marketing > reality (for now)
- And the biggest insight “The future isn’t what it used to be.”

## Key takeaway
Code is cheap, decisions are expensive, maintenance is everything
- The winners won’t be the fastest coders
- They’ll be the best system thinkers
