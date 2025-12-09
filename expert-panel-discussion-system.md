# Expert Panel Discussion System
## Multi-Agent Reasoning Framework for Claude Code

**Version:** 1.12.0
**Date:** December 2025
**Status:** Production Ready

---

## Executive Summary

The Expert Panel Discussion System is a sophisticated multi-agent reasoning framework that simulates structured discussions between thought leaders to explore difficult questions from multiple perspectives.

**Key Innovation:** Instead of getting a single AI perspective, users assemble a panel of 3-5 expert personas (DHH, Martin Fowler, Kent Beck, etc.) who debate, discuss, and synthesize insights through structured multi-round conversations.

**Value Proposition:**
- See tradeoffs you wouldn't have considered alone
- Get high-confidence consensus findings
- Understand divergent perspectives with clear reasoning
- Receive actionable recommendations based on synthesis

---

## Architecture Overview

```
┌─────────────────────────────────────────────────────────────┐
│                    /expert-panel (Command)                   │
│                  User Entry Point & Orchestrator             │
└─────────────────────┬───────────────────────────────────────┘
                      │
                      ├─ Analyze topic & suggest experts
                      ├─ Confirm expert list (interactive)
                      ├─ Suggest discussion type
                      └─ Confirm type (interactive)
                      │
                      ▼
┌─────────────────────────────────────────────────────────────┐
│           expert-panel-discussion (Orchestrator Agent)       │
│             Manages Rounds & Synthesizes Findings            │
└─────────────────────┬───────────────────────────────────────┘
                      │
        ┌─────────────┴─────────────┬─────────────┐
        │                           │             │
        ▼                           ▼             ▼
┌───────────────┐         ┌───────────────┐  ┌───────────────┐
│expert-perspective│       │expert-perspective│ │expert-perspective│
│   (DHH 🔴)      │       │(Martin Fowler 🔵)│ │ (Kent Beck 🟢) │
│  Simulates expert│       │Simulates expert  │ │ Simulates expert│
│  voice & reasoning│      │voice & reasoning │ │ voice & reasoning│
└───────────────┘         └───────────────┘  └───────────────┘
        │                           │             │
        └─────────────┬─────────────┴─────────────┘
                      │
                      ▼
┌─────────────────────────────────────────────────────────────┐
│               Sequential Thinking Analysis                   │
│         Extract consensus, divergence, unique insights       │
└─────────────────────┬───────────────────────────────────────┘
                      │
                      ├─ Decision: Continue or Conclude?
                      │
                      ▼
        ┌─────────────┴──────────────┐
        │                            │
    Continue?                    Conclude?
        │                            │
        ▼                            ▼
   Round N+1                   Final Synthesis
 (with context)              (Consensus + Divergence
                              + Recommendations)
```

---

## Three-Tier Agent System

### 1. Command Layer (`/expert-panel`)
**Role:** User interface and coordination

**Responsibilities:**
- Parse user's topic/question
- Analyze domain and suggest appropriate experts
- Interactive confirmation of expert list
- Suggest discussion type based on topic characteristics
- Interactive confirmation of discussion type
- Launch orchestrator with full context

**Key Feature:** Two confirmation steps ensure user control

---

### 2. Orchestrator Layer (`expert-panel-discussion`)
**Role:** Multi-round management and synthesis

**Responsibilities:**
- Assign color codes to experts (🔴🔵🟢🟡🟣)
- Launch all expert agents in parallel (critical for performance)
- Collect and organize responses
- Use sequential thinking for analysis
- Decide whether to continue or conclude
- Generate comprehensive final synthesis

**Key Feature:** Uses MCP sequential-thinking tool for systematic analysis

---

### 3. Expert Layer (`expert-perspective`)
**Role:** Authentic expert simulation

**Responsibilities:**
- Embody specific expert's thinking style
- Respond in expert's characteristic voice
- Show authentic disagreement when warranted
- Adapt to discussion type and round number
- Maintain consistency across rounds

**Key Feature:** Color-coded for visual distinction and tracking

---

## Discussion Types

### Comparison Matrix

| Type | Rounds | Duration | Cost | Best For |
|------|--------|----------|------|----------|
| **round-table** | 1 | 5-10 min | ~$0.30 | Quick perspectives, no disagreement |
| **debate** | 2-3 | 10-20 min | ~$0.60-0.90 | Opposing views, clear tradeoffs |
| **consensus-seeking** | 1-3 | 10-30 min | ~$0.30-0.90 | Team alignment, decision needed |
| **deep-dive** | 3 | 20-40 min | ~$0.90 | Complex topics, strategic decisions |

### Detailed Breakdown

#### Round-table (Default)
- **Format:** Single round, all experts share complete perspective
- **When:** Quick viewpoints, exploring options
- **Output:** Synthesis of diverse perspectives
- **Example:** "What are the tradeoffs of different caching strategies?"

#### Debate
- **Format:** 2-3 rounds with opposing camps, rebuttals, synthesis
- **When:** Clear opposing views (X vs Y, Should we...)
- **Output:** Both positions clearly stated, tradeoffs identified
- **Example:** "Hotwire vs React for our frontend?"

#### Consensus-seeking
- **Format:** 1-3 rounds, iterative refinement toward agreement
- **When:** Decision needs team alignment
- **Output:** Consensus recommendations OR documented productive impasse
- **Example:** "Which authentication strategy should we use?"

#### Deep-dive
- **Format:** Exactly 3 rounds (surface → deep → nuanced)
- **When:** Complex topics with many facets
- **Output:** Comprehensive analysis including edge cases
- **Example:** "How should we approach technical debt?"

---

## How It Works: Step-by-Step

### Step 1: Topic Analysis
```bash
User: /expert-panel Should we migrate to microservices?

System:
- Identifies domain: Architecture, Rails, scaling
- Analyzes complexity: High (multiple valid approaches)
- Determines stakeholders: Technical team
```

### Step 2: Expert Suggestion
```
Suggested Experts:
1. DHH (Rails creator, monolith advocate)
2. Martin Fowler (Architecture, microservices patterns)
3. Sam Newman (Microservices expert)

Reasoning: Diverse perspectives, potential disagreement
```

### Step 3: Expert Confirmation
```
AskUserQuestion:
"I've suggested DHH, Martin Fowler, and Sam Newman.
 Would you like to modify the list?"

Options:
- Accept suggested experts (Recommended)
- Modify the list
- Add more experts
- Remove an expert
```

### Step 4: Discussion Type Suggestion
```
Suggested Type: debate

Reasoning: Clear opposing views (monolith vs microservices)
```

### Step 5: Type Confirmation
```
AskUserQuestion:
"What type of discussion would you like?"

Options:
- round-table: Single round (5-10 min)
- debate: 2-3 rounds with rebuttals (10-20 min) ← Recommended
- consensus-seeking: Until agreement (10-30 min)
- deep-dive: 3 rounds sequential (20-40 min)
```

### Step 6: Parallel Expert Invocation
```
Orchestrator launches 3 expert agents simultaneously:

Task 1: expert-perspective
  Role: DHH, Rails creator
  Color: 🔴
  Task: Microservices migration
  Context: Team of 10, 100k users
  Discussion Type: debate
  Round: 1

Task 2: expert-perspective
  Role: Martin Fowler
  Color: 🔵
  [same structure]

Task 3: expert-perspective
  Role: Sam Newman
  Color: 🟢
  [same structure]

⚡ All launched in SINGLE message for parallel execution
```

### Step 7: Round 1 Responses
```
🔴 DHH:
"Don't do it. The majestic monolith works for 95% of cases..."
[350 words, strong position]

🔵 Martin Fowler:
"It depends on your organizational readiness. Microservices
require mature DevOps..."
[400 words, balanced view]

🟢 Sam Newman:
"Microservices solve organizational problems at scale..."
[375 words, pro-microservices]
```

### Step 8: Sequential Thinking Analysis
```
Using mcp__sequential-thinking__sequentialthinking:

Thought 1: Extract key positions
- DHH: Anti-microservices (complexity trade)
- Fowler: Conditional (readiness required)
- Newman: Pro-microservices (scale benefits)

Thought 2: Identify consensus
- All agree: Not for small teams
- All agree: Requires DevOps maturity
Agreement rate: 67% (2/3 on key points)

Thought 3: Identify divergence
- DHH vs Newman: Fundamental philosophy difference
- Fowler: Middle ground, context-dependent

Thought 4: Decision - continue?
- Debate format: Need rebuttal round
- Synthesis incomplete: Continue to Round 2
```

### Step 9: Round 2 (if continuing)
```
Orchestrator provides context from Round 1:

"DHH argued against microservices due to complexity.
 Newman advocated for microservices at scale.
 Fowler took a context-dependent position.

For Round 2, respond to opposing views and defend your stance."

[Experts respond with rebuttals and refinements]
```

### Step 10: Final Synthesis
```
# Expert Panel Discussion Summary

Topic: Should we migrate to microservices?
Experts: 🔴 DHH, 🔵 Martin Fowler, 🟢 Sam Newman
Rounds: 2 (debate format)

## Consensus Findings (High Confidence)

### Not Appropriate for Small Teams
Agreement: 🔴🔵🟢 (3/3 experts)

All experts agreed that microservices are overkill for teams
under 15-20 developers. The coordination overhead outweighs benefits.

### Requires Mature DevOps
Agreement: 🔴🔵🟢 (3/3 experts)

Mandatory prerequisites:
- Automated deployment pipelines
- Comprehensive monitoring/observability
- Service mesh or equivalent
- Strong DevOps culture

## Divergent Perspectives (Needs Judgment)

### When to Consider Microservices

🔴 DHH's Position:
Almost never. Start monolith, stay monolith. Extract services
only with clear organizational boundaries.

🔵 Martin Fowler's Position:
When organizational scaling demands it. Multiple teams, different
deployment cycles, proven monolith architecture first.

🟢 Sam Newman's Position:
When scaling engineering teams past 50 developers. Enables
team autonomy and independent deployment.

Why They Disagree:
DHH prioritizes simplicity and developer happiness.
Newman prioritizes organizational scaling.
Fowler balances both with context-awareness.

## Unique Insights

🔵 Martin Fowler:
"MonolithFirst approach: Build monolith, identify natural
seams through real use, then extract only if needed."

## Actionable Recommendations

1. **Stick with Monolith** (High Confidence)
   - Your team size: 10 developers
   - User scale: 100k users
   - Consensus: Well-factored monolith is appropriate

2. **Invest in Modular Design** (Consensus)
   - Clear module boundaries
   - Domain-driven design
   - Makes future extraction easier if needed

3. **Build DevOps Foundation** (Divergence-informed)
   - Even if staying monolith, modern practices apply
   - Positions you well if you grow past 50 devs
   - Aligns with Fowler's readiness criterion

## Confidence Assessment

High Confidence:
- Don't migrate now (team too small)
- Build modular monolith with clear boundaries

Needs Judgment:
- When/if to reconsider (tied to org growth)
- Definition of "too complex" for monolith

Further Research:
- Specific module boundaries for your domain
- Cost analysis of microservices infrastructure
```

---

## Expert Selection Strategy

### Domain-to-Expert Mapping

#### Rails Architecture
- DHH (Pragmatic, monolith advocate)
- Martin Fowler (Balanced, patterns)
- Sandi Metz (Object-oriented design)
- Uncle Bob (Clean architecture)

#### Testing Philosophy
- Kent Beck (TDD pioneer)
- Uncle Bob (Test-first advocate)
- DHH (Pragmatic testing)
- Rich Hickey (Simple made easy)

#### Frontend/UI
- DHH (Hotwire/Turbo)
- Ryan Singer (Basecamp product)
- Alan Cooper (Interaction design)
- Rich Harris (Svelte, reactivity)

#### Business Strategy
- Seth Godin (Marketing, positioning)
- Peter Thiel (Zero to one, contrarian)
- Naval Ravikant (Leverage, first principles)
- Jason Fried (Bootstrapping, simplicity)

#### Product Design
- Ryan Singer (Shape Up methodology)
- Julie Zhuo (Facebook product design)
- Alan Cooper (About Face, personas)
- Jared Spool (UX research)

#### Security
- Troy Hunt (Web security)
- Tanya Janca (AppSec)
- Bruce Schneier (Security philosophy)
- Kelsey Hightower (Cloud security)

### Selection Principles

1. **Diversity:** Different schools of thought
2. **Relevance:** Known expertise in domain
3. **Disagreement Potential:** Productive tension expected
4. **Balance:** 3-5 experts (sweet spot is 3-4)

---

## Use Cases & Examples

### Use Case 1: Architecture Decision
**Scenario:** Team debating monolith vs microservices

**Setup:**
- Topic: "Should we migrate to microservices?"
- Experts: DHH, Martin Fowler, Sam Newman
- Type: Debate (2-3 rounds)

**Outcome:**
- Consensus: Not appropriate for team size
- Divergence: When/if to reconsider
- Unique: MonolithFirst approach (Fowler)
- Decision: Stay monolith, build modular

**Value:** Avoided premature optimization, saved months of work

---

### Use Case 2: Security Strategy
**Scenario:** SaaS app needs authentication design

**Setup:**
- Topic: "Best authentication strategy for our app?"
- Experts: Troy Hunt, Tanya Janca, DHH
- Type: Consensus-seeking (2 rounds)

**Outcome:**
- Consensus reached: Devise + 2FA, OAuth for enterprise
- Implementation path: Session-based over JWT
- Security priorities: Aligned across team

**Value:** High-confidence decision, team alignment

---

### Use Case 3: Strategic Planning
**Scenario:** Startup deciding growth channel

**Setup:**
- Topic: "Focus on SEO or paid ads?"
- Experts: Seth Godin, Naval Ravikant, Rand Fishkin
- Type: Deep-dive (3 rounds)

**Outcome:**
- Round 1: Surface-level pros/cons
- Round 2: CAC/LTV economics analysis
- Round 3: Long-term brand vs short-term growth
- Decision: SEO for foundation, paid for validation

**Value:** Comprehensive analysis avoided expensive mistake

---

### Use Case 4: Technical Debt
**Scenario:** Engineering team prioritizing refactoring

**Setup:**
- Topic: "How should we approach technical debt?"
- Experts: Martin Fowler, Uncle Bob, Sandi Metz
- Type: Round-table (1 round)

**Outcome:**
- Consensus: Boy Scout Rule (leave better than found)
- Divergence: How aggressive to prioritize
- Framework: Impact vs effort matrix

**Value:** Actionable framework, team consensus

---

## When to Use Expert Panels

### ✅ Good Use Cases

#### Important Decisions
- Multiple valid approaches exist
- High stakes (affects team/product long-term)
- Tradeoffs aren't obvious

#### Exploring Perspectives
- Need to challenge your thinking
- Want to see what you're missing
- Validating or rejecting hypothesis

#### Complex Topics
- Many facets to consider
- Different experts bring different angles
- No single "right" answer

#### Strategic Planning
- Long-term implications
- Organizational decisions
- Philosophy/culture alignment

### ❌ Skip For

#### Simple Questions
- Clear, obvious answer exists
- Best practice is well-established
- Just need execution guidance

#### Speed-Critical
- Need answer immediately
- Cost/time not justified
- Single perspective sufficient

#### Already Decided
- Just need validation
- Not open to changing mind
- Using as justification only

---

## Technical Implementation Highlights

### Parallel Invocation Pattern
```markdown
**CRITICAL:** All experts launched in SINGLE message

❌ Wrong (sequential):
Task 1: expert-perspective (DHH)
[wait for response]
Task 2: expert-perspective (Fowler)
[wait for response]
Task 3: expert-perspective (Beck)

✅ Correct (parallel):
Task 1: expert-perspective (DHH)
Task 2: expert-perspective (Fowler)
Task 3: expert-perspective (Beck)
[all launched simultaneously]

Speed: 3x faster
Cost: Same
User experience: Much better
```

### Sequential Thinking Integration
```markdown
Orchestrator uses sequential-thinking for:
- Extracting key findings per expert
- Identifying consensus (>80% agreement)
- Identifying divergence (disagreement)
- Calculating novelty (new insights per round)
- Decision logic (continue or conclude?)

NOT used for:
- Expert responses (they use authentic voice)
- Simple consensus checks (manual sufficient)
```

### Color Coding System
```markdown
Visual Distinction:
🔴 Red   - Expert 1
🔵 Blue  - Expert 2
🟢 Green - Expert 3
🟡 Yellow - Expert 4
🟣 Purple - Expert 5

Benefits:
- Easy to track across rounds
- Visual scanning of synthesis
- Consensus representation (🔴🔵🟢 = all agree)
```

### Context Management
```markdown
Round 1: Topic + Background (small)
Round 2: Round 1 + Expert responses (medium)
Round 3: Round 1 + 2 + Expert responses (large)

Strategy: Keep summaries concise (<500 words/expert)
```

---

## Cost & Performance

### Cost Breakdown

**Base Costs (3 experts):**
- Round-table: ~$0.30 (1 round)
- Debate: ~$0.60-0.90 (2-3 rounds)
- Consensus-seeking: ~$0.30-0.90 (1-3 rounds)
- Deep-dive: ~$0.90 (3 rounds)

**Scaling Factors:**
- +1 expert: +33% cost per round
- +1 round: +100% cost for that round
- Sequential thinking: ~$0.05 per analysis

**Example: Deep-dive with 5 experts**
- 5 experts × 3 rounds = 15 invocations
- Cost: ~$1.50
- Time: 20-40 minutes
- Value: Comprehensive strategic analysis

### Performance Characteristics

**Latency:**
- Parallel invocation: 3 experts ≈ 1 expert duration
- Sequential thinking: +10-20 seconds per round
- Total: 5-10 min for round-table, 20-40 min for deep-dive

**Quality:**
- More experts = more perspectives (diminishing returns past 5)
- More rounds = deeper analysis (diminishing returns past 3)
- Discussion type matters more than expert count

---

## Synthesis Quality Factors

### Consensus Indicators
- **100% agreement:** Strong consensus (all experts)
- **75-99% agreement:** Consensus (most experts)
- **50-74% agreement:** Weak consensus (majority)
- **<50% agreement:** Divergence (split opinions)

### Divergence Analysis
When experts disagree, synthesis explains:
- Each expert's position
- Why they disagree (fundamental vs contextual)
- What factors would shift the tradeoff
- How to make the decision for your context

### Unique Insights
Value proposition:
- One expert raises point others missed
- Often most actionable recommendation
- Shows breadth of perspective gathering

---

## Success Metrics

### System Succeeds If:
1. Users find panels MORE valuable than direct Claude questions
2. Divergent perspectives help users see tradeoffs they missed
3. Consensus findings give confidence for decisions
4. Actionable recommendations are specific enough to implement
5. Cost/time justified by decision quality improvement

### Red Flags:
- All experts always agree (personas not distinct)
- Responses feel generic (not authentic voices)
- Users ignore divergent perspectives (not presenting tradeoffs clearly)
- Users rarely proceed past Round 1 (multi-round value unclear)

---

## Future Enhancements (V2)

### Deferred Features
1. **Socratic discussion type** - Moderator asks probing questions
2. **Adversarial mode** - Devil's advocate challenges all
3. **Custom expert personas** - User defines persona via prompt
4. **Save/resume discussions** - Persist panel state across sessions
5. **Expert persona library** - Pre-built beyond famous figures
6. **Voting mechanism** - Experts vote on proposals with reasoning

### Potential Improvements
1. **Dynamic expert suggestion** - LLM suggests based on topic analysis
2. **Confidence scoring** - Numerical confidence per finding (0-100%)
3. **Export formats** - Markdown report, PDF brief, Notion doc
4. **Interactive mode** - User injects questions mid-discussion
5. **Multi-model experts** - Some backed by Codex, others by Gemini

---

## Comparison with Alternatives

### vs. Direct Claude Questions
| Aspect | Direct Question | Expert Panel |
|--------|----------------|--------------|
| Speed | ✅ Fastest | ⚠️ Slower (5-40 min) |
| Cost | ✅ Cheapest | ⚠️ More expensive |
| Depth | ⚠️ Single perspective | ✅ Multiple perspectives |
| Tradeoffs | ⚠️ May miss | ✅ Explicitly surfaced |
| Confidence | ⚠️ Uncertain | ✅ Consensus indicators |
| Best for | Simple questions | Important decisions |

### vs. External LLM Consultation
| Aspect | External LLMs | Expert Panel |
|--------|---------------|--------------|
| Models | Multiple AI models | Single model, multiple personas |
| Cost | $$$ (real API calls) | $$ (simulated experts) |
| Divergence | Model differences | Philosophy differences |
| Context | Limited | Full project context |
| Best for | Validation | Deep exploration |

### vs. Ultra-Options
| Aspect | Ultra-Options | Expert Panel |
|--------|---------------|--------------|
| Format | Solution options | Expert discussion |
| Depth | Sequential thinking | Multi-round debate |
| Output | 3-5 approaches | Consensus + divergence |
| Interaction | None | 2 confirmation steps |
| Best for | Solution design | Philosophy/strategy |

---

## Configuration Requirements

### Required MCP Server

```json
{
  "mcpServers": {
    "sequential-thinking": {
      "command": "npx",
      "args": ["-y", "@anthropic/mcp-sequential-thinking"]
    }
  }
}
```

Add to `~/.claude/settings.json`

### Optional Configuration

None required - system works out of the box.

---

## Presentation Talking Points

### Opening Hook
*"What if you could assemble DHH, Martin Fowler, and Kent Beck in a room to debate your architecture decision?"*

### Key Message
**Multi-perspective reasoning through structured expert discussions reveals tradeoffs single-perspective analysis misses.**

### Value Proposition (30 seconds)
- Important decisions need multiple perspectives
- Expert panels surface consensus (high confidence) and divergence (tradeoffs)
- Structured discussion types optimize for speed vs depth
- Actionable synthesis includes specific recommendations

### Demo Flow (5 minutes)
1. Show simple invocation: `/expert-panel "topic"`
2. Interactive expert selection
3. Discussion type choice with cost/time
4. Live panel discussion (or recording)
5. Final synthesis with color-coded experts
6. Highlight consensus, divergence, recommendations

### Technical Highlight (2 minutes)
- Three-tier architecture (Command → Orchestrator → Experts)
- Parallel invocation for performance
- Sequential thinking for systematic analysis
- Color-coding for visual tracking

### Use Case Stories (3 minutes each)
- **Architecture:** Avoided premature microservices migration
- **Security:** Aligned team on auth strategy
- **Strategy:** SEO vs paid ads with comprehensive analysis

### Closing
*"Expert panels transform difficult decisions from 'what should I do?' to 'here's what experts agree on, here's where they disagree and why, here's how to decide for your context.'"*

---

## Appendix: Command Reference

### Basic Usage
```bash
/expert-panel [topic or question]
```

### Arguments
- `[topic]` - Optional. If omitted, will prompt for topic.

### Examples
```bash
# Architecture decision
/expert-panel Should we migrate to microservices?

# Security strategy
/expert-panel What's the best authentication approach?

# Frontend choice
/expert-panel Hotwire vs React for our app?

# Business strategy
/expert-panel Focus on SEO or paid ads for growth?

# Testing philosophy
/expert-panel How much test coverage is enough?
```

### Agent Invocation (Advanced)
```bash
# Direct orchestrator invocation
agent expert-panel-discussion

# Direct expert simulation
agent expert-perspective
```

---

## Appendix: Research References

### Inspiration
- Multi-agent debate systems (Du et al., 2023)
- Chain-of-thought prompting (Wei et al., 2022)
- Constitutional AI (Anthropic, 2023)
- Socratic questioning methodologies

### Claude Code Integration
- Task tool for agent orchestration
- AskUserQuestion for interactive confirmation
- Sequential thinking MCP for systematic analysis
- Plugin architecture for extensibility

---

**End of Tutorial Document**

For questions or feedback: marketplace@it.majesticlabs.dev
