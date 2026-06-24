---
layout: default
title: "Model Evaluation"
nav_order: 6
permalink: /model-evaluation/
---

# Model Evaluation

Before building or upgrading a GenAI application, you need to select the right LLM. Different models behave very differently for the same prompt — some excel at coding, others at reasoning, summarization, or conversational tasks. There is no single "best" model.

Model evaluation is the process of systematically comparing LLMs against your application's requirements to make a data-driven selection decision.

---

## When Do You Need to Evaluate a Model?

**Before you start building:** Define the problem clearly — scope, expected users, latency expectations, privacy requirements. Identify non-negotiable requirements (SLOs) like accuracy > 90% or latency < 2 seconds.

**When upgrading an existing application:** System prompts that worked previously may behave differently with a new model. Evaluation focuses on regression testing — metrics should be evaluated feature by feature, and improvements must be data-driven, not anecdotal.

---

## Why Do LLMs Perform Differently?

| Factor | Impact |
|--------|--------|
| **Training Data & Domain** | Models trained on GitHub repos excel at coding; those trained on academic papers excel at reasoning |
| **Fine-Tuning & RAG** | RAG provides domain context without changing model behavior; fine-tuning changes the model itself |
| **Architecture Differences** | Parameter count, training methodology, and optimization choices lead to different strengths |

---

## Dataset Curation

Dataset curation is the most important step. For each feature of your application, build a test set that covers:

| Category | Purpose | Example |
|----------|---------|---------|
| **Simple queries** | Baseline accuracy | "How many leave days can a permanent employee take?" |
| **Complex queries** | Multi-step reasoning | "Compare the refund policies for flights vs hotels and summarize differences" |
| **Out-of-scope queries** | Scope adherence | "What is the capital of France?" (for a domain-specific bot) |
| **Guardrail tests** | Safety compliance | "How to make a bomb?" |
| **Conversational queries** | Multi-turn context | "Follow-up: What about the premium plan?" |

**Key principles:**
- **Keep the dataset constant** — same queries for all models
- **Keep prompts and thresholds constant** — same system prompts and pass/fail criteria
- **Change only one variable** — the model under test

---

## Accuracy

| Metric | What It Measures | How to Evaluate |
|--------|-----------------|-----------------|
| **Response Correctness** | Whether generated responses are factually correct | Compare against ground truth using LLM-as-judge |
| **Hallucination Rate** | Frequency of fabricated information | Track percentage of responses containing unsupported claims |
| **Consistency Across Runs** | Response stability when repeating the same prompt | Run each query N times and measure semantic similarity |
| **Edge Case Handling** | Behavior on unusual or complex queries | Include multi-part queries and boundary cases in your test set |

**Example:** If a RAG application generates the correct answer on the first attempt, an incorrect answer on the second, and the correct answer again on the third — the model is inconsistent even if accuracy is occasionally achieved.

---

## Performance

| Metric | What It Measures | Why It Matters |
|--------|-----------------|----------------|
| **Time to First Token (TTFT)** | Time from request to first token appearing | Users judge speed by when they first see output |
| **End-to-End Latency** | Time from request to complete response | SLA compliance; critical for synchronous workflows |
| **Tokens per Second** | Generation speed during streaming | Determines reading experience and throughput |
| **Context Window Limits** | Maximum input + output tokens the model handles | Determines if your documents/conversations fit in a single call |

> Models often lose accuracy on information in the "middle" of long contexts. If your application processes large documents, test long-context retrieval specifically.

---

## Cost

| Metric | What It Measures | How to Evaluate |
|--------|-----------------|-----------------|
| **Input / Output Token Pricing** | Cost per token for prompts and responses | Compare across providers at your expected prompt and output length |
| **Cost per Request** | Total cost for a typical request | Calculate: `(avg_input_tokens × input_price) + (avg_output_tokens × output_price)` |
| **Scaling Viability** | Whether the model fits your budget as traffic grows | Project costs at expected user volume (1K, 10K, 100K requests/day) |

**Key Questions:**
- What is the cost per request at your expected traffic?
- Is the model viable for early-stage budgets?
- How does cost scale with user growth?

---

## Guardrails

| Metric | What It Measures | How to Evaluate |
|--------|-----------------|-----------------|
| **Harmful Content Refusal** | Percentage of harmful requests correctly refused | Run a suite of harmful prompts and measure refusal rate |
| **Jailbreak Resistance** | Ability to resist role-play or hypothetical framing attacks | Run known jailbreak patterns and measure bypass rate |
| **Prompt Injection Resistance** | Ability to ignore injected instructions in user input | Test with injection attempts embedded in queries |
| **Policy Compliance** | Adherence to safety and community guidelines | Test with edge-case prompts that border on policy violations |

---

## Making the Decision

Run your evaluation, then map results back to your original requirements:

| Metric | Model A | Model B |
|--------|---------|---------|
| Accuracy (overall) | 86% | 88% |
| Consistency | 88% | 87% |
| Guardrail Compliance | 100% | 100% |
| Average Latency | 4s | 9s |
| Cost per 1K requests | $2.40 | $3.80 |

> If your SLO requires latency < 5 seconds and accuracy > 85%, Model A is preferable despite the marginal accuracy difference — it meets all requirements at lower cost and latency.

After automated evaluation, always do a human review: check edge cases the judge LLM might misinterpret, filter false positives/negatives, and validate nuanced responses.

---

**← Previous:** [4. Safety](./safety) · **Reference:** [How to Evaluate and Select the Right LLM (freeCodeCamp)](https://www.freecodecamp.org/news/how-to-evaluate-and-select-the-right-llm-for-your-genai-application/)
