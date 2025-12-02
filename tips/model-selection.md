# Model Selection Guide (2025 Update)

[← Back to Main](../README.md)

## The 2025 Model Landscape

Five frontier models dominate AI coding in late 2025. Each has a distinct "cognitive profile" suited for specific tasks.

---

## Model Comparison

| Model | Primary Strength | Context | Speed | Cost | "Vibe" |
|-------|------------------|---------|-------|------|--------|
| **Claude 4.5 Opus** | Planning, reliability | 200K | Medium | $$$ | Strict Senior Dev |
| **GPT-5.1 Codex** | Execution, engineering | 128K | Medium | $$ | Pragmatic Doer |
| **Gemini 3 Pro** | Visuals, massive context | **2M** | Fast | $ | Creative Designer |
| **Kimi k2 Thinking** | Cost-effective reasoning | 256K | Medium | ¢ | Efficient Researcher |
| **Grok 4.1** | Personality, creative | 256K | Fast | $$ | Witty Collaborator |

---

## Benchmark Scores (SWE-bench 2025)

| Model | SWE-bench Score | Cost/Test | Best For |
|-------|-----------------|-----------|----------|
| GPT-5.1 Codex | Very High | $0.76 | Implementation |
| Claude 4.5 Sonnet | Very High | $1.68 | Thinking/Planning |
| Kimi k2 Thinking | High | $0.60 | Budget tasks |

> **Key Insight**: GPT-5.1 Codex is the "doer" - excels at first-pass working code. Claude 4.5 is the "thinker" - better for complex reasoning and planning.

---

## Claude 3.5 Sonnet

**The Gold Standard for Agentic Coding**

Claude 3.5 Sonnet has established itself as the benchmark for coding tasks within Cursor.

### Strengths

- Exceptional **instruction following**
- "Don't code yet, just analyze" → Actually obeys
- Superior adherence to negative constraints
- Handles large context windows with less "forgetfulness"
- More concise than GPT-4o (focuses on code, not conversation)
- Best model for Cursor's Background Agents

### Weaknesses

- More expensive than budget alternatives
- Can be overly cautious on edge cases

### Best For

```
✅ Complex system architecture
✅ Planning phase of large refactors
✅ Backend service design
✅ Code review and analysis
✅ Agentic workflows (Composer/Agent Mode)
```

### Prompting Tips

```
Claude excels when given constraints:
"Analyze the authentication flow.
Do NOT write code yet.
Create a detailed plan with edge cases."
```

---

## Claude 4.5 Opus

**The Deep Thinker**

### Strengths

- Massive context window (up to 200k-500k tokens)
- Exceptional for long-term memory tasks
- Can hold entire mid-sized repositories in working memory

### Best For

```
✅ Complex debugging across many files
✅ Recalling patterns from old code
✅ Deep architectural reasoning
```

---

## GPT-5.1 High Max

**The Balanced Engineer**

### Strengths

- Identifies constraints and risks like a "Senior Architect"
- Excellent diff-editing benchmarks
- Balances speed and reasoning depth
- "High Max" = full reasoning computation

### Weaknesses

- Less "creative" than Gemini
- Less strict than Claude

### Best For

```
✅ System design decisions
✅ Module contracts and trade-offs
✅ The "Clarify and Approach" phase
✅ General-purpose coding tasks
```

### Prompting Tips

```
GPT-5.1 works well with structured requests:
"First, analyze the trade-offs of approach A vs B.
Then recommend the best path forward.
Finally, implement the chosen approach."
```

---

## Gemini 2.0 Flash / Gemini 3 Pro

**The Heavy Context Specialists**

### Gemini 2.0 Flash - The Reader

Best for massive context operations:

```
Context Window: 1-2 MILLION tokens
Best For:
✅ Analyzing massive diffs
✅ Processing MP3 files for transcription
✅ "Long context" debugging across dozens of files
✅ Massive error dump analysis
```

### Agentic Limitations

```
⚠️ Gemini struggles as an "actor" in Agent Mode

Good at:
- Reading and analyzing code
- Generating code in Composer

Struggles with:
- Tool-calling stability
- Executing terminal commands
- Correctly parsing file paths
```

### Gemini 3 Pro - The Visual Giant

### Strengths

- **2 MILLION token context** (active reasoning!)
- Native multimodal (images, screenshots)
- Excellent for creative coding tasks
- Google Workspace integration

### Weaknesses

- Struggles with strict instruction following
- May "go rogue" and start coding when told to wait
- Less reliable for precise backend logic
- **Not recommended for Agent Mode execution**

### Best For

```
✅ Screenshot → Frontend code
✅ Analyzing massive codebases (>1M tokens)
✅ Creative/visual tasks
✅ Heavy context reading tasks
```

### Prompting Tips

```
Gemini excels with visual input:
"Here's a screenshot of the design.
Implement this UI using React and Tailwind.
Match the colors and spacing exactly."
```

### When to Use Gemini

```
Use Gemini for:
- Reading and understanding large codebases
- Visual/multimodal tasks
- Massive context analysis

Avoid Gemini for:
- Agent Mode autonomous execution
- Complex tool-calling workflows
- Precise terminal command execution
```

---

## Kimi k2 Thinking

**The Budget Powerhouse**

### Architecture

- 1 trillion parameters (MoE)
- Only 32B active at inference
- Trained as "thinking agent"

### Strengths

- **$0.60/M input** (vs $3+ for Claude)
- Handles 300+ sequential tool calls
- Open-source friendly
- Excellent for high-volume automation

### Weaknesses

- Not natively in Cursor dropdown (yet)
- Requires OpenRouter or Moonshot API setup
- Less polished than Western models

### Best For

```
✅ Cost-sensitive projects
✅ Automated pipelines
✅ High-volume tasks
✅ When budget > quality priority
```

### Integration

```
Via OpenRouter:
1. Get OpenRouter API key
2. Cursor Settings → API Keys → OpenRouter
3. Select "kimi-k2-thinking" from models
```

### Performance Reality Check

```
⚠️ Important Caveat:

Direct comparisons show Kimi k2 is:
- Significantly slower than Claude Sonnet
- More bug-prone in Agent Mode
- Less reliable for complex task completion

In Agent Mode tests:
- Kimi k2: Struggled with extreme slowness, failed tasks
- Claude Sonnet: Completed same tasks in minutes

Trade-off: Acceptable code at fraction of cost,
but higher latency and "management overhead"
```

### Prompting "Thinking" Models

**Don't over-prompt!** These models reason better with goals, not steps:

```
❌ Bad:
"Step 1: Read the file
Step 2: Find the function
Step 3: Modify line 45..."

✅ Good:
"Goal: Implement a resilient payment processor.
Reason about Stripe API failure modes.
Consider idempotency requirements.
Then output the implementation."
```

---

## Grok 4.1

**The Social Coder**

### Modes

- **Thinking** (quasarflux): Deep reasoning, internal tokens
- **Fast** (tensor): Speed-optimized, retuned for tool usage and low-latency inference

### Grok 4.1 Fast

The "Fast" variant is retuned specifically for tool usage:

```
Strengths:
✅ Excels at autonomously picking tools
✅ Outperforms GPT-5 and Claude in tool-calling scenarios
✅ Low-latency inference
✅ Great for iterative Agent Mode loops
```

### Strengths

- **Emotional intelligence** tuning
- Real-time X (Twitter) data integration
- Reduced hallucinations vs Grok 4.0
- Highest LMArena text scores (1483 Elo)

### Weaknesses

- Less backend-specialized than Claude
- X integration not useful for all projects

### ⚠️ Critical Warning

```
Grok 4.1 is "way too eager to make changes"

Reported issues:
- Hallucinating edits
- Overwriting functional code without verification
- Acting before thinking

Solution: Use with strict "Plan Mode" constraints
Always review before accepting changes
```

### Best For

```
✅ "Vibe Coding" - personality-driven apps
✅ User-facing copy and error messages
✅ Sentiment analysis applications
✅ Apps integrating social media data
✅ Fast iterative loops (with supervision)
```

### Integration Note

```
Native integration was delayed in late 2025.
Workaround: Use OpenRouter API key.
```

### Prompting Tips

```
Leverage Grok's personality:
"Write error messages for this login flow.
They should feel empathetic and helpful,
not robotic. Match the brand's friendly tone."

For Agent Mode, add constraints:
"STOP and create a plan before making changes.
Do NOT edit any files until I approve the plan."
```

---

## The Plan-Act Pattern

Optimal workflow using multiple models:

### Phase 1: PLAN

**Model**: Claude 4.5 Opus or GPT-5.1 High

```
"Analyze this request: [requirement]
Do NOT write code.
Create a detailed implementation plan in plan.md
Identify edge cases and potential regressions.
Ask clarifying questions if needed."
```

### Phase 2: CRITIQUE (Optional)

**Model**: Gemini 3 Pro

```
"Review plan.md for:
- Efficiency gaps
- Missing visual/UX considerations
- Alternative approaches"
```

### Phase 3: EXECUTE

**Model**: Composer (or GPT-5.1 Fast)

```
"Implement Step 1 of plan.md.
Run tests after implementation.
If tests pass, proceed to Step 2.
Stop and report if tests fail."
```

---

## Cost Optimization

### Pricing Reference (Late 2025)

| Model | Input/M | Output/M |
|-------|---------|----------|
| Claude 4.5 Opus | $3.00 | $15.00 |
| GPT-5.1 High Max | $2.50 | $10.00 |
| Gemini 3 Pro | Free preview / $0.50 | $1.50 |
| Kimi k2 Thinking | $0.60 | $2.00 |
| Grok 4.1 | $2.00 | $8.00 |

### Strategy

```
Daily Coding:
└── Pro Plan with "Auto" mode

Heavy Refactoring:
└── BYOK Claude 4.5 Opus (worth the cost)

Budget Tasks:
└── Kimi k2 via OpenRouter

Massive Codebase Analysis:
└── Gemini 3 Pro (free preview)

Hard Debugging:
└── GPT-5.1 High Max (balanced reasoning)

User-Facing Copy:
└── Grok 4.1 (personality)
```

### Pro Plan Economics

```
$20/month includes:
├── Credit pool (fast vs slow)
├── "Auto" mode (switches models automatically)
├── Unlimited slow requests
└── Enterprise: per-user spending limits
```

---

## Model Switching Rules

### Do

- Pick one model per conversation
- Use different models for different phases
- Start new chat when switching models

### Don't

- Switch models mid-conversation
- Expect context to transfer between models
- Use expensive models for simple tasks

---

## Quick Reference

| Task | Recommended Model |
|------|-------------------|
| Architecture planning | Claude 4.5 Opus |
| System design decisions | GPT-5.1 High Max |
| Screenshot → Code | Gemini 3 Pro |
| Massive codebase analysis | Gemini 3 Pro |
| Budget automation | Kimi k2 Thinking |
| User-facing copy | Grok 4.1 |
| Quick inline edits | Cursor-small / Composer |
| General coding | GPT-5.1 or Claude 3.5 |

---

[← Back to Main](../README.md)
