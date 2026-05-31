# Appendix: Multi-Agent Architecture

## Why Multi-Agent Is More Reliable Than Single-Agent

This was our most important engineering discovery during the Illusion Period, and the key turning point for entering the Boundaries Period.

## The Single-Agent Problem

The typical failure mode of a single Agent handling complex tasks:

```
User instruction: "Write a Zhihu Q&A post and publish it to the Fu Yi account"
         ↓
    [Single Agent execution]
         ↓
    1. Topic selection → picked 3
    2. Writing → wrote a draft
    3. Review → "looks fine"
    4. Publishing → published
         ↓
    Result: the article wrote "He Yue Theory" as "Five Elements He Yue Theory" (a deprecated term)
         Because the Agent referenced its own memory during step 2 (writing),
         and the memory hadn't been updated with the terminology change.
```

The problem is not that the Agent isn't smart. It's that **the context window is too long, and the Agent cannot maintain consistency across all steps.** The output of one step influences the input of the next, and errors amplify step by step.

## The Multi-Agent Approach

```
User instruction: "Write a Zhihu Q&A post and publish it to the Fu Yi account"
         ↓
    [Dispatch Agent] → breaks into 5 tasks, assigns to different Agents
         ↓
    1. [Topic Agent] → match topic → output: {question ID, angle}
         ↓ Human check: is the topic appropriate?
    2. [Writing Agent] → write draft → output: {title, body}
         ↓ Human check: terminology correct? persona aligned?
    3. [Review Agent] → check item by item → output: {issue list}
         ↓ Human confirmation: do all these issues need fixing?
    4. [Revision Agent] → fix issues one by one → output: {final draft}
         ↓ Human read-through
    5. [Publishing Agent] → publish → output: {publish link, status}
```

## Key Principles

### 1. Agents communicate via structured data

Agent A's output → not free text → it's JSON

```json
{
  "task": "topic matching",
  "selected": {
    "question_id": "12345",
    "angle": "Explaining workplace responsibility distribution through deviation theory",
    "confidence": 0.85
  },
  "alternatives": [...]
}
```

**Reason:** Free text leads to "semantic drift" — Agent B misinterprets Agent A's intent.

### 2. Each Agent's context window contains only what it needs

- Topic Agent: receives persona file + topic pool (does not receive writing guide)
- Writing Agent: receives persona file + selected topic + writing guide (does not receive review standards)
- Review Agent: receives final writing draft + review checklist (does not receive persona file)

**Reason:** The smaller the context, the more focused the Agent. This also naturally implements our persona file system — each file is designed for a specific Agent only.

### 3. There must be "human breakpoints" between Agents

After each Agent's output → human glances → confirms → next Agent.

**This is not an efficiency issue. This is quality control.** Human breakpoints don't require much time (1-2 minutes per breakpoint for daily publishing), but they catch semantic errors passed between Agents.

## Architecture Diagram

```
                    ┌─────────────────┐
                    │  Dispatch Agent  │
                    │ (human + LLM)    │
                    │ task breakdown / │
                    │ prioritization   │
                    └───────┬─────────┘
                            │
            ┌───────────────┼───────────────┐
            │               │               │
            ▼               ▼               ▼
    ┌──────────┐    ┌──────────┐    ┌──────────┐
    │ Writing  │    │ Review   │    │Publishing│
    │ Agent    │    │ Agent    │    │ Agent    │
    │(Fu Yi IP)│    │(generic) │    │(platform │
    │          │    │          │    │ adapter) │
    └─────┬────┘    └─────┬────┘    └─────┬────┘
          │               │               │
          │    ┌──────────┘               │
          │    │                          │
          ▼    ▼                          ▼
      [Human BP]                    [Human BP]
      (topic confirm)              (pre-publish read)
```

## When You Should Consider Multi-Agent

- ✅ Your task involves 3 or more independent steps
- ✅ You've discovered "context drift" between different steps (the output of one step is misinterpreted by the next)
- ✅ You need different "personas" or "professional standards" to handle different steps
- ❌ The task has only 1-2 steps, and the Agent's context window is fully sufficient

## The Cost of Multi-Agent

- High setup cost: each Agent needs its own prompt file
- Human breakpoints mean the human must be online — multi-Agent architecture requires human presence
- Data formats between Agents must be unified, otherwise the building blocks won't fit together

**If you need "fully automated," multi-Agent architecture is not for you. If you need "high quality + human control," multi-Agent is currently the only solution.**

---

[← Back to Map](../README.md)