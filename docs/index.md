---
layout: default
title: Home
nav_order: 1
description: "GenAI Applications Evaluation Guidelines - A structured guide to evaluating GenAI applications"
permalink: /
---

# GenAI Applications Evaluation Guidelines

GenAI teams are moving fast — but evaluation often remains ad hoc.

Unlike traditional software, GenAI applications are not always easy to test with simple input-output assertions. The same prompt can produce different valid responses, and quality often depends on hidden or intermediate steps: retrieved context, tool calls, memory state, agent handoffs, safety checks, and more.

That makes evaluation harder — but also more important.

This guide provides a structured way to think about GenAI evaluation across common application patterns, including RAG, tool use, memory, agents, multimodal systems, performance, and safety.

It is designed to help teams answer:

- **What should we evaluate for this application?**
- **Which method should we use** — manual review, code-based checks, LLM-as-judge, or a combination?
- **How can we start implementing these evaluations** in a repeatable way?

<a href="./mindmap.html" target="_blank">View the interactive mind map of all evaluation areas to see the overall organization of this guide →</a>

---

## How to Use This Guide

Start with **[Strategy](./strategy)** if you are defining an evaluation approach from scratch.

Then jump to the areas that match your application:

- **Building a RAG app?** Look at [retrieval quality, context relevance, faithfulness, citations, and hallucination](./accuracy/context-sourcing).
- **Using tools or APIs?** Evaluate [tool selection, parameter correctness, execution success, and recovery from failures](./accuracy/agentic).
- **Using memory?** Check [what gets stored, what gets retrieved, and whether memory introduces privacy, poisoning, or stale-context risks](./accuracy/memory).
- **Building agents?** Evaluate not only the final answer, but also the [trajectory: handoffs, intermediate decisions, role adherence, and unnecessary steps](./accuracy/agentic).
- **Preparing for production?** Use the [Performance](./performance) and [Safety](./safety) sections to evaluate latency, cost, reliability, guardrails, privacy, and harmful-output risks.

---

## How This Guide Is Organized

| Section | What It Covers |
|---------|----------------|
| **[Strategy](./strategy)** | Evaluation methods, test data, ground truth, scoring, LLM-as-judge, human review, and code-based checks |
| **[Accuracy](./accuracy)** | Capability-specific evaluation for LLM responses, RAG, context provision, tool use, memory, multimodal systems, and agents |
| **[Performance](./performance)** | Latency, cost, throughput, reliability, and scalability under realistic usage conditions |
| **[Safety](./safety)** | Guardrails, privacy, bias and fairness, harmful content, prompt injection, and data leakage |

Each leaf node in the mind map links to a short practical guide. Some include code snippets or implementation examples that teams can adapt as a starting point.

---

The goal is not to prescribe one universal recipe. GenAI applications vary too much for that.

The goal is to help teams stop winging evaluation — and start making quality measurable, repeatable, and easier to discuss.

**Start here:** [Strategy →](./strategy)
