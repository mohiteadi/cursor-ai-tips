# Model Selection Guide (2025 Update)

[← Back to Main](../README.md)

## The 2025 Model Landscape

Five frontier models dominate AI coding in late 2025. Each has a distinct "cognitive profile" suited for specific tasks.

---

## Model Comparison

| Model | Primary Strength | Context | Speed | Cost | "Vibe" |
|-------|------------------|---------|-------|------|--------|
| **Claude 4.5 Opus** | Planning, reliability | 200K | Medium | $$$ | Strict Senior Dev |
| **GPT-5.1 High Max** | Architecture, balance | 128K | Medium | $$ | Pragmatic Architect |
| **Gemini 3 Pro** | Visuals, massive context | **2M** | Fast | $ | Creative Designer |
| **Kimi k2 Thinking** | Cost-effective reasoning | 256K | Medium | ¢ | Efficient Researcher |
| **Grok 4.1** | Personality, real-time data | 256K | Fast | $$ | Witty Collaborator |

---

## Claude 4.5 Opus

**The Architect's Choice**

### Strengths

- Exceptional **instruction following**
- "Don't code yet, just analyze" → Actually obeys
- Long-lived backend system design
- Cross-service coordination

### Weaknesses

- Expensive ($3/M input, $15/M output)
- Can be overly cautious

### Best For

```
✅ Complex system architecture
✅ Planning phase of large refactors
✅ Backend service design
✅ Code review and analysis
```

### Prompting Tips

```
Claude excels when given constraints:
"Analyze the authentication flow.
Do NOT write code yet.
Create a detailed plan with edge cases."
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

## Gemini 3 Pro

**The Visual Giant**

### Strengths

- **2 MILLION token context** (active reasoning!)
- Native multimodal (images, screenshots)
- Excellent for creative coding tasks
- Google Workspace integration

### Weaknesses

- Struggles with strict instruction following
- May "go rogue" and start coding when told to wait
- Less reliable for precise backend logic

### Best For

```
✅ Screenshot → Frontend code
✅ Analyzing massive codebases (>1M tokens)
✅ Creative/visual tasks
✅ "Voxel art eagle riding a tricycle" type prompts
```

### Prompting Tips

```
Gemini excels with visual input:
"Here's a screenshot of the design.
Implement this UI using React and Tailwind.
Match the colors and spacing exactly."
```

### Context Window Usage

```
Gemini 3 Pro can hold:
- Entire large monorepos
- Full documentation sets
- Complete git history + current code

Use @Codebase liberally with Gemini.
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
- **Fast** (tensor): Speed-optimized, 2M context

### Strengths

- **Emotional intelligence** tuning
- Real-time X (Twitter) data integration
- Reduced hallucinations vs Grok 4.0
- Highest LMArena text scores (1483 Elo)

### Weaknesses

- Less backend-specialized than Claude
- X integration not useful for all projects

### Best For

```
✅ "Vibe Coding" - personality-driven apps
✅ User-facing copy and error messages
✅ Sentiment analysis applications
✅ Apps integrating social media data
```

### Prompting Tips

```
Leverage Grok's personality:
"Write error messages for this login flow.
They should feel empathetic and helpful,
not robotic. Match the brand's friendly tone."
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
