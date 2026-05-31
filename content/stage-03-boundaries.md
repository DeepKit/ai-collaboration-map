# ⚔️ Stage 3: The Boundaries Period

> **"It's not that AI can't do it. It's that I put AI in the wrong place. Draw the lines right, and both sides feel at ease."**

**Time Window:** 12-24 months

**One-line definition:** You've learned to delineate the human-machine boundary — not by intuition, but by rules. Behind every boundary is a painful failure.

---

## 📊 Data

- Starting from month 13, we gradually established **7 hard boundaries**
- Projects that violated boundaries had a rework rate **3.2 times** that of projects that respected them
- The most critical boundary: **control flow decisions must be made by humans; AI only executes**
- Boundaries aren't drawn once and done — on average, each boundary went through **2-3 rounds of renegotiation**

---

## The Seven Hard Boundaries

These are not theories. Behind each one is at least a month of painful debugging.

| # | Boundary | Meaning | Consequence of Violation |
|---|----------|---------|--------------------------|
| 1 | **Control flow belongs to humans** | Task ordering, branching logic, termination conditions — determined by deterministic code or humans, not AI | AI will "get lost" — looping infinitely within a task or jumping to an irrelevant direction |
| 2 | **Direction belongs to humans** | An article's core argument, a product's core value proposition — set by humans, expanded by AI | You'll get fluent but mediocre content with no sharp perspective |
| 3 | **Review belongs to humans** | Any AI-produced external-facing content must undergo human read-through. Not a glance, but word by word | Hidden errors and logical breaks will surface at the worst possible moment |
| 4 | **Decisions belong to humans** | Architecture choices, pricing strategy, launch timing — AI provides analysis, humans make decisions | AI will offer fake decisions like "choose A because A looks safest" |
| 5 | **Cognitive sovereignty belongs to humans** | Key theoretical concepts, core narrative frameworks — humans must be able to articulate them in their own words | You lose control of your own knowledge system — you appear to understand, but you actually don't |
| 6 | **State belongs to humans** | Agent execution state (session liveness, cookie validity, last publishing point) — maintained and checked by humans | Agents run continuously in an unaware state, producing massive amounts of wasted work |
| 7 | **Failure belongs to humans** | When an Agent fails — don't just tell it "try again"; have a human decide: retry, change strategy, or abandon | Agents repeatedly attempt the same error, wasting tokens and time |

---

## 🔴 Three Predicaments

### Predicament 1: "I've become dependent on AI and I'm afraid to write on my own"

This is a cognitive withdrawal symptom. When you're accustomed to the speed of AI assistance, pure human writing becomes extraordinarily difficult — not because your ability has atrophied (though it has, somewhat), but because you've grown used to the workflow of "first see what AI writes, then edit."

**Our experience:** Early in the Boundaries Period, we tried "pure human days" — no AI, write on your own for a full day. Day one's output was only a third of AI-assisted output. But the quality — depth of insight, logical consistency, personal voice — far exceeded AI-assisted work. This discovery helped us establish the first boundary.

### Predicament 2: "The boundaries are drawn too tightly, and AI becomes useless"

After the pain of the Illusion Period, you might overcompensate — imposing too many constraints on AI. AI goes from "doing everything" to "doing nothing."

**Our experience:** For a period, we required every paragraph AI produced to cite sources and reasoning chains. This led to "over-annotation" — AI output was filled with formal citations, but the core arguments were drowned out.

### Predicament 3: "The same boundary works differently across different tasks"

Writing boundaries ≠ coding boundaries ≠ architecture decision boundaries.

A concrete example: in content creation, we allow AI to freely generate first drafts (Boundary 2 relaxed); in code generation, we require AI to generate only unit functions, not module structures (Boundary 2 tightened). Same principle, different execution.

**Core insight:** Boundaries are not switches (on/off). They are sliders. Different tasks need different slider positions.

---

## 🟢 Three Breakthroughs

### Breakthrough 1: Establish the "human defines the DAG, AI fills the nodes" working model

This is the most important engineering practice of the Boundaries Period.

**DAG (Directed Acyclic Graph)** = the sequence and branching logic of tasks, defined by humans.
**Nodes** = each step in the DAG, executed by AI, with humans checking between nodes.

Real example — our content publishing workflow:
```
[Human decides] What to publish today? → Zhihu Q&A: Fu Yi × 2 + MaLiHuiJu × 1 + ZhiTianMing × 1
        ↓
[AI executes] Topic matching: match 4 questions from the topic pool based on each IP's persona
        ↓
[Human checks] Topic confirmation: is the timing right for these four questions today?
        ↓
[AI executes] Draft writing: four Agents each write their own piece
        ↓
[Human checks] Read-through review: read every piece word by word
        ↓
[AI executes] Formatting + layout
        ↓
[Human executes] Manual publishing (not a technical limitation — a deliberately preserved review checkpoint)
```

**How to get there:** Draw your current most complex AI workflow as a flowchart. After every AI step, forcibly insert a human check point. Run for two weeks, recording which checkpoints actually caught problems and which were just formalities. Delete the formal ones, reinforce the ones that found problems.

### Breakthrough 2: Discovering the "clarify mode"

When AI encounters uncertainty, it shouldn't guess — it should proactively ask the human.

This is the most elegant implementation of boundaries. Not "AI cannot do X," but "AI can do X, but when X's boundaries are fuzzy, AI must stop and ask."

**Our clarify rules:**
- Operations involving monetary amounts → must clarify
- Operations involving user privacy → must clarify
- Content for external publication → must clarify
- Two consecutive tool call failures → must clarify

### Breakthrough 3: Accepting that "boundaries need constant renegotiation"

AI's capabilities are changing (every single month), and your capabilities are changing too. A boundary drawn six months ago may be too loose or too tight today.

We developed a habit: quarterly "boundary calibration" — review the past month's AI collaboration log and identify:
1. Which boundary was breached and caused a problem?
2. Which boundary is too tight, limiting AI's effective use?
3. Are there new boundaries that need to be established?

---

## ⚠️ The Biggest Trap

> **Treating boundaries as permanent.**

Boundaries are alive. They are an **ongoing negotiation** between you and AI.

When GPT-4 arrives, when Claude Sonnet arrives, when your own abilities evolve — old boundaries become new shackles.

**How to avoid it:** Quarterly boundary calibration. Not checking whether AI has gotten stronger — checking whether **the division of labor between you and AI** is still correct.

---

## 🔗 Signal That You're Entering the Next Stage

You stop spending time arguing about "can AI do X?"

You spend time designing "the verification mechanism for when AI does X."

When your daily conversation shifts from "let's have AI try this" to "let AI do this, but I'll check at step 3 and step 7" — you've entered the Collaboration Period.

---

[← Previous Stage: The Illusion Period](stage-02-illusion.md) | [← Back to Map](../README.md) | [Next Stage: The Collaboration Period →](stage-04-collaboration.md)