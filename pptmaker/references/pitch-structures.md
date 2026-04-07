# Presentation Structures Reference

A comprehensive guide for AI-assisted presentation generation with reveal.js. This document provides specific slide-by-slide structures for different presentation scenarios.

---

## Part 1: General Principles

Foundational frameworks that apply across all presentation types.

### 1.1 Rule of Three

**Core Rule:** Limit primary messages to exactly 3 pillars. Audiences reliably retain 3 points; retention degrades sharply at 5 or more.

**Application:**
- Core message pillars: Structure presentations around 3 main ideas
- Proof points: 3 supporting examples per claim
- Action items: Never exceed 3 asks per slide
- Content blocks: Divide presentations into 3 major sections

**Why it works:** Cognitive load theory shows 3 creates pattern completion; it feels "right" and complete to audiences.

**Red flags:**
- 5+ bullet points on one slide
- More than 4 key takeaways
- More than 2 concurrent CTAs

---

### 1.2 Minto Pyramid Principle (SCQA)

**Structure:** Lead with conclusion, then build supporting arguments.

**Framework (SCQA):**
1. **Situation** — Shared context both parties understand
2. **Complication** — Tension, change, or problem introduced
3. **Question** — Implicit question raised by complication
4. **Answer** — Your position, stated upfront (not at end)

**Slide-Level Application:**
- Slide 1: State conclusion/recommendation clearly
- Slides 2-3: Establish shared situation
- Slides 4-5: Present complication/challenge
- Slides 6+: Build supporting arguments in parallel groups of 3

**Best For:**
- Executive briefings (C-suite expects answer first)
- Consulting presentations
- Strategy proposals
- Technical decision documents
- Board updates

**Presentation Flow:**
```
Hook: "We should acquire CompanyX" (minute 0)
   ↓
Context: Market, timing, competitive landscape (minutes 1-3)
   ↓
Why: Risk of inaction, opportunity window (minutes 4-5)
   ↓
Evidence: Financial model, market data, team fit (minutes 6-10)
```

**Danger:** Sounds prescriptive. Use when audience trusts you or time is limited. Add emotional arc if decision affects people.

---

### 1.3 Nancy Duarte's Sparkline

**Core Concept:** Oscillate between "what is" (current reality) and "what could be" (future vision). The presenter is the mentor (Yoda); the audience is the hero.

**Structure:**
- **Thesis opening:** State the transformation you're inviting
- **Oscillation pattern:** Reality → Possibility → Reality → Possibility...
  - Reality: Status quo, pain, cost, limitation
  - Possibility: Vision, benefit, freedom, transformation
- **Escalating tension:** Each oscillation raises stakes
- **Resolution:** Call to adventure—specific next step for audience
- **Final image:** A moment of aspiration or proof

**Slide Pattern (25-30 min keynote):**
1-2. Opening with transformation thesis (1-2 min)
3-5. Current reality (what is broken) (2-3 min)
6-8. What if we could... (vision) (2-3 min)
9-11. Obstacles in current state (2-3 min)
12-14. New possibility (2-3 min)
15-17. Evidence this is possible (2-3 min)
18-20. Call to adventure (1-2 min)
21. Final aspirational image or proof (30 sec)

**Best For:**
- Keynote presentations
- Product launches
- Organizational change management
- Fundraising (when seeking mission alignment)
- Inspiring internal teams

**Emotional Arc:**
```
Start: We have a problem we haven't said aloud
   ↓ (Rise)
Possibility: What if we did X differently?
   ↓ (Dip)
Reality: Here's why we haven't done it
   ↓ (Rise)
Vision: Imagine what becomes possible
   ↓ (Dip)
Challenge: This requires you
   ↓ (Rise)
Resolution: Here's exactly what you do
```

**Critical:** Audience should feel the hero's journey, not a sales pitch.

---

### 1.4 Assertion-Evidence Slide Design

**Core Rule:** Slide title = complete sentence assertion, not topic label. Slide body = visual evidence, not bullet points.

**What This Means:**

| Bad (Topic) | Good (Assertion) |
|---|---|
| "Revenue Trends" | "Revenue grew 34% YoY driven by SMB expansion" |
| "Team Capabilities" | "Three engineers have shipped 5+ production systems at scale" |
| "Market Analysis" | "TAM grew from $2B to $8B in 18 months due to regulatory change" |

**Slide Body Rules:**
- Single visual per slide (chart, diagram, photo, video, screenshot)
- No bullets unless essential (maximum 2-3 short lines)
- White space is not wasted space
- Every visual element supports the assertion

**Why It Works:**
- Title previews the conclusion
- Audience processes visual + assertion simultaneously
- Reduces cognitive load
- Improves memory retention by 65%

**Best For:**
- Technical conference talks
- Academic presentations
- Research proposals
- Engineering reviews
- Data-heavy pitches

**Implementation Checklist:**
- [ ] Title is 1-2 sentences, contains the insight
- [ ] Body has one dominant visual
- [ ] Visual directly supports the assertion
- [ ] No redundancy between title and visual
- [ ] Claim is specific, not vague ("X increased" vs. "X is important")

---

### 1.5 Storytelling Arc

**Structure:** Three-act dramatic arc adapted for business.

**Act 1: Setup (Establish Stakes)**
- Who is the audience? (the hero)
- What is their world like?
- What is at stake for them?

**Act 2: Conflict (Present Challenge)**
- What problem interrupts their world?
- What if nothing changes? (consequences)
- Why is now the time to act?

**Act 3: Resolution (Solution and Proof)**
- Here's what becomes possible
- Proof it works (case study, demo, data)
- Your role: call to action (what you want them to do)

**Slide Distribution (20-30 min talk):**
- Slides 1-4: Setup (5-6 min) — Establish audience's world
- Slides 5-12: Conflict (8-10 min) — Build tension, show pain
- Slides 13-25: Resolution (8-10 min) — Solution, proof, CTA

**Best For:**
- Sales presentations
- Customer success stories
- Product pitches
- Fundraising
- Internal change initiatives

**Audience Psychology:**
Humans don't forget facts; we remember stories. The audience should see themselves in the "hero" role, not see your product as hero.

```
"You're building a team. Hiring is broken. What if you could identify
talent 10X faster? Here's how Company Z did it. You can too. Start here."

NOT: "Our product is great. Here are features. Buy it."
```

---

## Part 2: Startup Investment Pitch

Three canonical frameworks synthesized into universal guidance.

### 2.1 Guy Kawasaki 10/20/30

**Rules:** 10 slides, 20 minutes, minimum 30pt font.

**Slide Sequence:**

1. **Title Slide**
   - Company name (large)
   - One-liner tagline (15-20 words max)
   - Company logo

2. **Problem/Opportunity**
   - State the pain (make it visceral)
   - Who feels this pain?
   - How big is the problem?

3. **Value Proposition**
   - What unique value do you deliver?
   - Why you, not incumbent?
   - One sentence if possible

4. **Underlying Magic**
   - The "secret sauce" or insight
   - Patent? Unique data? Team insight?
   - Why is this defensible?

5. **Business Model**
   - How do you make money?
   - Unit economics (simple)
   - Pricing model

6. **Go-to-Market Strategy**
   - How do you acquire customers?
   - Sales model (direct, channel, viral)?
   - Customer acquisition cost

7. **Competitive Analysis**
   - Who are the competitors?
   - Why are you different?
   - Market position

8. **Team**
   - Founders and key 3 people
   - Why are they the ones to win?
   - Key credential per person

9. **Financials**
   - 3-year projection (revenue, margin)
   - Key assumptions clearly stated
   - Unit growth indicators

10. **Status and Ask**
    - Current stage (pre-launch, beta, revenue)
    - Specific ask amount
    - How will you use the capital?
    - When?

**Timing Breakdown:**
- Problem/Solution: 4 minutes
- Market/Model: 6 minutes
- Competition/Team: 4 minutes
- Financials/Ask: 4 minutes
- Flex buffer: 2 minutes

---

### 2.2 Sequoia Capital Format

**Structure:** 10 slides following investor decision-making logic.

**Slide Sequence:**

1. **Company Purpose (One Sentence)**
   - Mission, not feature list
   - Example: "Eliminate password friction globally"

2. **Problem**
   - Current pain point (quantified)
   - Who has this problem?
   - Cost of status quo

3. **Solution**
   - How you solve it (not how product works)
   - Why you're positioned to solve it

4. **Why Now (CRITICAL SLIDE)**
   - What changed recently that enables this?
   - Regulatory, technology, market shift?
   - Why not 2 years ago? Why not 2 years from now?

5. **Market Size**
   - TAM (Total Addressable Market)
   - SAM (Serviceable Available Market)
   - SOM (Serviceable Obtainable Market)
   - Realistic path to $100M+ revenue

6. **Competition**
   - Direct competitors (name them)
   - Why you win (different axis, better execution, network effect)

7. **Product**
   - What does it do (show > tell)
   - Demo or screenshots
   - Key differentiators

8. **Business Model**
   - Revenue model (subscription, transaction, etc.)
   - Customer lifetime value (LTV)
   - Gross margin target

9. **Team**
   - Founders and key hires (3-4 people)
   - Why this team wins at this specific problem

10. **Financials**
    - Revenue to date
    - Burn rate and runway
    - 3-year projections (topline, margin)
    - Key metrics (retention, CAC, LTV)

**Presenter Note:** Sequoia emphasizes "why now" as the hinge pin. If you can't answer it credibly, the pitch fails.

---

### 2.3 Y Combinator Format

**Principles:** 10-12 slides, one idea per slide, large fonts (28pt+), clean design.

**Slide Sequence:**

1. **Title + One-Liner**
   - Company name, founder names
   - Tagline (< 15 words, benefit-focused)

2. **Problem (Vivid)**
   - Show the pain, don't list features
   - Help investors *feel* the problem
   - Use metaphor, analogy, or story

3. **Solution (Show Don't Tell)**
   - Demo or screenshot if possible
   - Clear product positioning
   - How it solves the problem

4. **Traction (Most Important Post-Launch)**
   - User growth chart (going up and to the right)
   - Revenue curve if available
   - Retention metrics
   - Customer testimonial or quote

5. **Market**
   - TAM is a starting point, not the end
   - Show evidence of market demand

6. **Business Model**
   - Unit economics
   - Pricing strategy
   - LTV:CAC ratio (target 3:1+)

7. **Competition**
   - Honest assessment
   - Why you win (not "no competition")

8. **Team**
   - Key founder strengths (why you're uniquely positioned)
   - Any "unfair advantage" (industry background, prior success, unique insight)

9. **Financial Projections**
   - 3-year revenue projections
   - Key assumptions (customer count, ARPU, churn)
   - Margin path

10. **The Ask**
    - Specific funding amount
    - What milestones will you hit?
    - Use of capital breakdown

11. **Timeline (Optional)**
    - When do you close the round?
    - When do you start?

12. **Appendix**
    - Backup slides for tough questions

**Design Rules (Strict):**
- White background default
- One visual per slide (no clutter)
- Minimum 28pt font for body, 44pt for titles
- No animations (slide transition OK)
- No company logo on every slide (title only)

---

### 2.4 Universal Investor Pitch Structure (Synthesis)

**Recommended Sequence (11-12 slides, 18-22 minutes):**

| Slide | Title | Duration | Key Elements |
|-------|-------|----------|--------------|
| 1 | Title + One-Liner | 30 sec | Company, founders, tagline (< 15 words) |
| 2 | Problem (Vivid) | 2 min | Make investor *feel* the pain. Quantify if possible. |
| 3 | Solution (Show, Don't Tell) | 1.5 min | Demo/screenshot showing how problem is solved. |
| 4 | Why Now | 1 min | What changed recently that makes this solvable/necessary? |
| 5 | Market Size | 1 min | TAM (total), SAM (serviceable), SOM (realistic). |
| 6 | Business Model | 1 min | Revenue model, pricing, unit economics. |
| 7 | Traction | 2 min | Growth curve, revenue, retention, customer validation. |
| 8 | Competition | 1 min | Direct competitors, differentiation (not "no competition"). |
| 9 | Team | 1.5 min | Founders + 2-3 key people. Why they win at this problem. |
| 10 | Financial Projections | 1.5 min | 3-year revenue path, margin path, key assumptions. |
| 11 | The Ask | 1 min | Amount, use of capital (product/sales/marketing %), timeline. |
| 12 | Appendix | Buffer | Backup slides for questions (not presented upfront). |

**Total Time:** 18-22 minutes + 10-15 min Q&A = 30-37 min slot.

**Slide Design Rules (Universal):**
- Minimum 26pt font for body text
- One idea per slide
- Titles as assertions (not "Market Size" → "Total addressable market is $8B and growing 25% YoY")
- Visual evidence over bullet points (charts, screenshots, data)
- High contrast (dark text on light, or vice versa)
- Single color accent (not rainbow)
- No animation beyond simple slide transition

**Content Guardrails:**

| Do | Don't |
|---|---|
| Lead with the problem, not your product | Start with company history or origin story |
| Show growth curve (hockey stick) as proof | Claim "no competition" |
| Use real customer names (if permitted) or quotes | Use vague language ("very big opportunity") |
| Show 3-year projections with assumptions | Project earnings (only revenue for early stage) |
| Ask for specific amount and use of funds | Ask for undefined "capital" |

**Critical Flow:**
1. Problem must be *felt* (1-2 minutes spent here)
2. Solution must be *shown* (demo or screenshot)
3. Why now must be *credible* (not "market is ready for this")
4. Traction must be *visible* (growth curve, not anecdotes)
5. Team must be *credible* (real credential, not "passionate")
6. Ask must be *specific* (amount, milestones, timeline)

**Pitch Killer Mistakes:**
- Spending < 1 minute on problem (investors won't care about solution if problem isn't real)
- No traction mentioned until asked
- "We have no competition" (signals inexperience)
- Financial projections without assumptions (not credible)
- Team slide that lists titles only (need "why you")
- Asking for money without clear use ("We need $2M") vs. ("We need $2M: $1.2M engineering, $500K sales/marketing, $300K runway")

---

## Part 3: Internal Business Presentations

### 3.1 Project Status Update

**Context:** Regular check-in with stakeholders on progress. Tone: transparent, focused on decisions needed.

**Length:** 6-10 slides, 10-20 minutes (depends on audience level).

**Slide-by-Slide Structure:**

| Slide | Title | Content | Timing |
|-------|-------|---------|--------|
| 1 | Project Title + Status | RAG indicator (Red/Amber/Green). One-sentence status. | 1 min |
| 2 | Executive Summary (BLUF) | Bottom Line Up Front: What's the headline? Are we on track? Do you need a decision? | 1 min |
| 3 | Progress vs. Plan | Milestone table (milestone name, planned date, actual date, status). Show what's on track, delayed, at-risk. | 2 min |
| 4 | Key Accomplishments | 3-5 measurable wins since last update. Use data. | 1.5 min |
| 5 | Issues & Blockers | Prioritized list (high/medium/low). Owner assigned per issue. Impact if unresolved. | 2 min |
| 6 | Risks & Dependencies | Things that could go wrong. External dependencies blocking us. Mitigation plan per risk. | 1.5 min |
| 7 | Budget & Resource Status | Spend vs. budget. Headcount. Any overages or concerns? | 1 min |
| 8 | Next Period Plan | 3-5 key milestones for next period. | 1 min |
| 9 | Decisions Required | Specific decisions needed from leadership. Recommendations provided. | 1.5 min |

**Content Rules:**
- RAG indicator on slide 1 sets tone (green = brief, amber = dig in, red = deep dive)
- BLUF slide 2 must answer: "Are we on track? What do you need from me?"
- Milestone table: show dates, avoid vague "in progress" status
- Issues: prioritize ruthlessly (high, medium, low; don't list 10)
- One decision per bullet point; one recommendation per decision
- No surprises in a status update (stakeholders should have been notified in real-time if something critical changed)

**Audience Adaptation:**
- Executive sponsor: slides 1-3, 5, 9 (2-5 min version)
- Project team: all slides, deeper dives on 4-8
- Steering committee: slides 1-3, 5-9 (core version)

---

### 3.2 Technical Proposal (ADR-Based)

**Context:** Proposing a technical decision (architecture, tool selection, framework, etc.). Tone: analytical, options-oriented.

**Length:** 8-14 slides, 20-40 minutes.

**Slide-by-Slide Structure:**

| Slide | Title | Content | Timing |
|-------|-------|---------|--------|
| 1 | Title + Decision Statement | "ADR: Should we adopt microservices architecture?" (Clear question form.) | 1 min |
| 2 | Context & Background | What's the current state? What prompted this decision? | 2 min |
| 3 | The Problem | What pain or risk are we addressing? Why must we decide now? | 2 min |
| 4 | Option A (with equal depth to others) | Name it clearly. How does it work? Key benefits. | 3 min |
| 5 | Option B | Name it clearly. How does it work? Key benefits. | 3 min |
| 6 | Option C (if applicable) | Name it clearly. How does it work? Key benefits. | 2-3 min |
| 7 | Evaluation Criteria | What matters? (performance, cost, maintainability, risk). Assign weights if needed. | 2 min |
| 8 | Comparison Matrix | Options (rows) × Criteria (columns). Score each. Transparently show trade-offs. | 2 min |
| 9 | Recommended Option + Rationale | Which option wins and why. Address top trade-offs. | 2 min |
| 10 | Architecture Diagram | Visual showing how recommended option works in context. | 1.5 min |
| 11 | Trade-Offs & Risks | What are we giving up with this choice? What could go wrong? | 2 min |
| 12 | Implementation Plan | Phased approach. Timeline. Rollback plan. | 2 min |
| 13 | Success Metrics | How will we know this was the right choice? (performance targets, cost, team satisfaction) | 1.5 min |
| 14 | Decisions Required | Do we proceed? Any concerns before we start? | 1 min |

**Content Rules:**
- Decision statement as question, not assertion (invites discussion)
- Options treated equally (don't bury your non-preferred option)
- Comparison matrix shows numbers, not opinion (score each criterion 1-5)
- Recommended option justified by weighted criteria, not gut feel
- Trade-offs section: what are we accepting to get this choice?
- Success metrics define "right decision" before you're locked in
- Implementation plan includes rollback (shows you've thought through failure)

**Red Flags:**
- "This is the only option" (means you haven't thought hard enough)
- Comparison matrix shows one option clearly winning on all fronts (probably a rigged comparison)
- No risk mitigation plan (architects should assume things go wrong)

---

### 3.3 Quarterly Business Review (QBR)

**Context:** Executive review of quarterly performance, key metrics, OKRs, and forward planning. Tone: candid, data-driven, strategic.

**Length:** 12-18 slides, 45-75 minutes (includes discussion).

**Slide-by-Slide Structure:**

| Slide | Title | Content | Timing |
|-------|-------|---------|--------|
| 1 | Quarter Headline | "Q2 2026: Growth accelerated, unit economics improved, 3 hires completed" | 1 min |
| 2 | Executive Summary | Performance vs. plan. OKRs (summary RAG). Key wins and misses. One-page leadership brief. | 3 min |
| 3 | OKR Scorecard | Objectives (rows) × Status (RAG). Include % completion. | 2 min |
| 4 | Key Metrics Dashboard | 4-6 primary KPIs (revenue, churn, CAC, LTV, NPS, engagement). Show 4+ quarters trend. | 3 min |
| 5 | Highlights & Wins | 3-4 major accomplishments. Quantified impact. Team call-outs. | 2 min |
| 6 | Misses & Learnings | What didn't go as planned. Why? What did we learn? (Candor builds trust.) | 2 min |
| 7-8 | Deep Dive 1 | One strategic area (e.g., "Product roadmap execution"). Slides with context, results, implications. | 5-7 min |
| 9-10 | Deep Dive 2 | Another strategic area (e.g., "Sales pipeline and conversion"). Context, results, implications. | 5-7 min |
| 11 | Competitive & Market Update | Market share position. Competitive moves. Regulatory or macro shifts. | 3 min |
| 12 | Next Quarter Objectives | OKRs for Q3. How do they build on Q2 success? Stretch goals? | 3 min |
| 13 | Strategic Priorities | Top 3-5 initiatives for next quarter. Resource allocation. | 2 min |
| 14 | Risks & Dependencies | What could derail next quarter? External dependencies? Mitigation? | 2 min |
| 15 | Budget & Resource Request | Headcount plans. Budget needs. Explain why. | 2 min |
| 16 | Decisions & Actions | What decisions do we need? What actions are you taking as a result of this QBR? | 1 min |
| 17 | Appendix | Detailed metric tables, competitive analysis, financial models (presented if needed). | — |

**Content Rules:**
- Headline slide sets narrative (don't make audience hunt for the story)
- OKR scorecard: use RAG (red/amber/green), not percentages alone (% complete ≠ on track)
- Metrics dashboard: show trend lines (4+ quarters), not just current quarter
- Misses section proves honesty (no executive trusts QBRs with only wins)
- Deep dives address "so what?" — not just what happened, but implications
- Next quarter OKRs ladder up to annual strategy
- Decisions must be specific and actionable

**Storytelling Arc:**
1. Here's where we were (Q2 opening state)
2. Here's what we accomplished (highlights + OKRs)
3. Here's where we fell short (misses, learnings)
4. Here's what changed in the market (context)
5. Here's where we're going (Q3 priorities)
6. Here's what we need from you (decisions, resources, support)

**Red Flags:**
- QBR with zero misses (either you didn't stretch hard enough or you're not being candid)
- Next quarter priorities unrelated to Q2 learnings (not building on data)
- Metrics showing 4 quarters but no context for what changed (trend without story)

---

## Part 4: Conference and Tech Talks

### 4.1 Lightning Talk (5-7 slides, 5 minutes)

**Context:** Ultra-short format. One insight, one call to action. Maximum impact, minimum time.

**Slide-by-Slide Structure:**

| Slide | Title | Content | Timing |
|-------|-------|---------|--------|
| 1 | Title + Who You Are | Name, company, what you're about (1-sentence bio) | 20 sec |
| 2 | The Problem or Question | State a pain or provocative question. Make it relatable. | 60 sec |
| 3 | Key Insight | Your core insight or aha moment. The thing the audience didn't expect. | 90 sec |
| 4 | Why It Matters | Implication: what changes because of this insight? | 60 sec |
| 5 | Where to Go Next | How does the audience apply this? One specific action or resource. | 30 sec |

**Content Rules:**
- Slide 1: introduce yourself in 1-2 sentences (name, company, expertise area)
- Slide 2: problem should be something the audience has felt
- Slide 3: insight is the "wow" moment (spend most time here)
- Slide 4: connect insight to audience benefit
- Slide 5: specific call-to-action (not "Google this")
- No more than 1-2 lines of text per slide
- Use visuals (not text) wherever possible

**Timing Breakdown:**
```
Intro (20 sec) → Problem (60 sec) → Insight (90 sec) → 
Implication (60 sec) → CTA (30 sec) = 300 seconds
```

**Red Flags:**
- Spending more than 60 sec on intro (time is precious)
- Insight that feels obvious or already known
- CTA that's generic ("Check out our website")

---

### 4.2 Standard Conference Talk (20-35 slides, 25-30 minutes)

**Context:** Main session or workshop talk. Deep dive on one topic. Balance teaching with engagement.

**Slide-by-Slide Structure:**

| Section | Slides | Duration | Content |
|---------|--------|----------|---------|
| **Opening** | 1-2 | 1-2 min | Title slide. Hook (provocative claim or surprising stat). Set expectation. |
| **Hook** | 3-4 | 2-3 min | Make it urgent/interesting. Why should they care? |
| **Context** | 5-8 | 3-5 min | Background, terminology, current landscape. Make audience caught up. |
| **Core Block 1** | 9-14 | 5-7 min | First major concept. Explain, example, implication. |
| **Core Block 2** | 15-20 | 5-7 min | Second major concept. Explain, example, implication. |
| **Core Block 3** | 21-25 | 4-5 min | (Optional) Third concept or deeper dive into one of above. |
| **Synthesis** | 26-28 | 2-3 min | Tie blocks together. How do they relate? What's the bigger picture? |
| **Conclusion** | 29-30 | 1-2 min | Takeaways (max 3). Final thought. |
| **Call to Action** | 31 | 30 sec | What action does audience take? Resources/contact info. |

**Slide Design:**
- Each core block: concept slide → example slide → implication slide
- Use assertion-evidence (title is the claim, body is visual proof)
- Diagrams, screenshots, code samples where possible (not bullet points)
- One idea per slide (resist cramming 3 ideas on one slide)

**Content Pattern for Each Core Block:**
```
Slide 1: Introduce the concept (title as assertion)
Slide 2: Show real example (screenshot, diagram, code)
Slide 3: What you can do with this concept (application)
Slide 4: Common mistake (what NOT to do)
Slide 5: Best practice (how to do it right)
Slide 6: Audience implication (why this matters to them)
```

**Red Flags:**
- Spending > 5 min on context (audience is impatient, teach as you go)
- Core blocks that are unrelated (talk should have coherent arc)
- No examples (abstract talks lose audiences)
- Synthesis missing (audience left to figure out how pieces fit)

**Engagement Tactics:**
- Ask a question at minute 10 (break monotony)
- Live demo (risky but high engagement if it works)
- Audience poll or raise-of-hands question (minute 15)
- Relatable anecdote in opening (makes speaker human)

---

### 4.3 Workshop / Tutorial (15-30 slides + exercises, 60-180 minutes)

**Context:** Hands-on learning. Ratio: 40% instruction, 50% practice, 10% framing.

**Structure Pattern:**
```
Opening (10 min) → Instruction Block 1 (10 min) → Exercise 1 (10 min) → 
Debrief 1 (5 min) → Instruction Block 2 (10 min) → Exercise 2 (10 min) → 
Debrief 2 (5 min) → ... → Capstone Exercise (20-30 min) → Wrap-up (5 min)
```

**Slide-by-Slide (per block):**

| Slide | Content | Timing |
|-------|---------|--------|
| 1 | Block title (what skill will they learn?) | 1 min |
| 2-3 | Learning objectives (measurable, behavior-based) | 1 min |
| 4-6 | Concept explanation (with examples) | 4 min |
| 7 | Exercise prompt (clear steps, expected outcome) | — |
| — | *Participants work on exercise* | 8-12 min |
| 8 | Debrief slide (common mistakes, key insight) | 3-5 min |

**Red Flags:**
- More than 5 minutes of instruction before first exercise (people zone out)
- Exercises that don't apply concept just taught (disconnect)
- No capstone exercise (people don't retain if they don't synthesize)
- Ambiguous exercise prompt (people get lost)

**Exercise Design:**
- **Pre-requisites slide** (non-negotiable): "You should have X installed, account Y created, file Z downloaded"
- **Expected outcome slide**: Show what a correct answer looks like
- **Troubleshooting section**: "If you see error X, do Y" (anticipate common failures)
- **Extension exercise**: "If you finish early, try this harder version"

**Capstone Exercise Requirements:**
- Synthesizes all skills taught
- Takes 20-30 min for average participant
- Clear success criteria
- Bonus extension for fast participants
- Debrief shows multiple valid solutions (not one right answer)

---

## Part 5: Sales and Product Demo

### 5.1 Problem-Agitation-Solution (PAS)

**Context:** Direct sales presentation. Goal: create urgency and position product as obvious answer.

**Length:** 8-10 slides, 20-30 minutes.

**Slide-by-Slide Structure:**

| Slide | Title | Content | Timing |
|-------|-------|---------|--------|
| 1 | Welcome + Agenda | Your name, company. What you'll cover. | 1 min |
| 2 | Their World (Day in the Life) | Paint a vivid picture of how your buyer works today. Make it relatable. | 2 min |
| 3 | The Specific Problem | The exact pain they experience. Quantify if possible (time lost, money wasted, risk). | 2 min |
| 4 | Cost of Status Quo (Agitation 1) | If nothing changes, what's the cost? Annual impact? Risk? | 2 min |
| 5 | Compounding Risk (Agitation 2) | If they wait, what gets worse? Speed of change in market? Competitive threat? | 1.5 min |
| 6 | Introducing the Solution | Here's how we solve it. Why us (credibility signal). | 1.5 min |
| 7 | How It Works (Demo or Walkthrough) | Show the product solving the problem. Live demo preferred if stable. | 5 min |
| 8 | Proof & Social Proof | Case study snippet or customer testimonial. Numbers (cost savings, time saved). | 2 min |
| 9 | Call to Action | Next step: trial, meeting, pilot. Make it specific and easy. | 1 min |

**Content Rules:**
- Problem statement: specific to *their* situation (not generic)
- Agitation: two separate concerns (cost + risk, or efficiency + growth)
- Solution introduction: establish credibility before diving into product (awards, customers, patents)
- Demo shows end-user value, not technical features (how they benefit, not how it works)
- Proof is *their peer* (case study from similar company), not random testimonial
- CTA is immediate action, not "let's talk" (trial, pilot, next meeting scheduled in this call)

**Timing Breakdown:**
```
Relationship building (1 min) → Problem/agitation (5.5 min) → 
Solution introduction (1.5 min) → Demo (5 min) → Proof (2 min) → 
CTA (1 min) = 16 minutes + 4-6 min for their questions
```

**Red Flags:**
- Problem definition is generic (doesn't feel tailored to *their* situation)
- Demo focuses on cool features, not solving stated problem
- Case study is from different industry (low credibility)
- No specific CTA (vague "we'll follow up")

---

### 5.2 Feature Showcase (10-16 slides, 30-45 minutes)

**Context:** Detailed product walkthrough showing capabilities. Usually post-discovery conversation. Buyer already knows they have a problem; you're now proving your solution is best.

**Slide-by-Slide Structure:**

| Slide | Title | Content | Timing |
|-------|-------|---------|--------|
| 1 | Agenda | What you'll cover (features + outcomes). | 1 min |
| 2 | Discovery Recap | Recap conversation from last meeting. "Here's what we heard..." | 1 min |
| 3 | Product Overview | 30,000-foot view of how product is structured. 3 main modules/capabilities. | 1 min |
| 4-8 | Feature Deep Dive (Feature 1) | Feature name → Problem it solves → How it works (screenshot/demo) → Outcome for buyer | 3-4 min |
| 9-12 | Feature Deep Dive (Feature 2) | Same pattern as Feature 1 | 3-4 min |
| 13-14 | Feature Deep Dive (Feature 3) | Same pattern (if applicable) | 2-3 min |
| 15 | Integration & Compatibility | What systems does it integrate with? Support for their tech stack? | 1 min |
| 16 | Security & Compliance | Data privacy, encryption, certifications. Address buyer concern. | 1 min |
| 17 | Implementation & Onboarding | How hard is it to set up? Training? Support? | 1 min |
| 18 | Pricing Overview | Transparent pricing model. Tiers if applicable. | 1 min |
| 19 | Customer Proof | Customers using this. Case study numbers. Customer quote. | 1 min |
| 20 | Next Steps | Timeline, trial offer, pilot plan, decision criteria. | 1 min |

**Feature Deep Dive Pattern (per feature):**
```
Slide A: Problem this feature solves (assertion: "Feature X reduces manual data entry by 80%")
Slide B: How it works (screenshot or video walkthrough)
Slide C: Outcome for them (time saved, cost reduced, accuracy improved)
Slide D: Optional—comparison to how they do it today (shows improvement)
```

**Content Rules:**
- Feature showcase *not* the same as PAS (discovery already happened; focus is on detailed product)
- Each feature must tie back to their stated need (from discovery)
- Screenshots/demos should match their environment (same industry, same problem domain)
- Implementation timeline and support level are selling points (not afterthoughts)
- Pricing should be transparent (don't hide costs; builds trust)

**Red Flags:**
- Feature deep dives that don't relate to stated problem (doesn't prove you listened)
- Demo slides that are too small to see (kills credibility)
- Implementation section that's vague ("we'll help you set up")
- Pricing model buried or missing (buyer will ask anyway; be proactive)

---

### 5.3 Customer Case Study Presentation

**Context:** Proof that your solution works for customers like them. Goal: reduce buyer risk by showing similar customer success.

**Length:** 8-12 slides, 10-20 minutes.

**Slide-by-Slide Structure:**

| Slide | Title | Content | Timing |
|-------|-------|---------|--------|
| 1 | Customer Introduction | Company name, industry, size. Logo. "They're like you..." | 1 min |
| 2 | The Situation | Customer's business context. What they were trying to do. | 1 min |
| 3 | The Challenge | Specific problem they faced. Quantify pain (cost, time, risk). | 1.5 min |
| 4 | Why They Chose You | What made them pick your solution vs. alternatives? (Builds credibility) | 1 min |
| 5 | Implementation Journey | How long did it take? Any bumps? How did your team help? (Realism) | 1.5 min |
| 6 | Feature in Action | Walkthrough of how they use your product day-to-day. Screenshot/demo. | 2 min |
| 7 | The Results (Before/After) | Quantified impact. Time saved, cost reduced, revenue increased, risk mitigated. | 2 min |
| 8 | Customer Voice | Direct quote from customer. Why they recommend you. Video testimonial ideal. | 1 min |
| 9 | Broader Impact | How did success with your solution create secondary benefits? (Expanded use, team adoption, etc.) | 1 min |
| 10 | Applicable to You | How does this apply to their situation? What can they expect? | 1 min |
| 11 | Next Steps | Pilot offer, timeline to implementation, support during onboarding. | 1 min |

**Content Rules:**
- Customer must be **similar to buyer** (same industry or problem, same scale)
- Challenge must be **specific and relatable** (not generic)
- Results must be **quantified** (not "we saved time"; give a number)
- Customer voice is **powerful** (direct quote or video kills objections)
- Implementation journey shows **realism** (no case study where it was effortless)
- "Applicable to You" is critical (don't make buyer guess; spell out why this proves it works for them)

**Case Study Proof Checklist:**
- [ ] Metric 1: Time/efficiency (reduced from X to Y)
- [ ] Metric 2: Cost (saved $X per year)
- [ ] Metric 3: Quality/risk (reduced errors by X%, compliance achieved)
- [ ] Timeline: "Results achieved in X weeks/months"
- [ ] Quote: Customer name, title, company
- [ ] Applicability: "If you have X problem like they did, you can expect Y")

**Red Flags:**
- Customer too large or too small relative to buyer (not credible)
- Results are only soft metrics ("improved team morale") — need hard numbers
- No implementation timeline (buyer can't gauge difficulty)
- Generic case study that applies to anyone (loses persuasive power)

---

## Part 6: Educational and Training

### 6.1 Lecture Format (20-30 slides, 50 minutes)

**Context:** Academic or training setting. Goal: transfer knowledge, check understanding.

**Structure Pattern:**
```
Opening (5 min) → Block 1 (10 min) → Check 1 (3 min) → 
Block 2 (10 min) → Check 2 (3 min) → Block 3 (10 min) → 
Check 3 (3 min) → Wrap-up (5 min) = 50 minutes
```

**Slide-by-Slide (per block):**

| Slide | Content | Timing |
|-------|---------|--------|
| 1 | Learning objectives (measurable, behavior-based) | 2 min |
| 2-5 | Concept explanation (with examples, visuals) | 5 min |
| 6 | Application example (real-world context) | 2 min |
| 7 | Comprehension check (question for class to answer) | 1 min |

**Content Rules:**
- Learning objectives stated at block start (e.g., "By the end, you'll be able to identify X and apply Y")
- Assertion-evidence on every content slide (title = claim, body = proof)
- Each block self-contained (could be understood independently)
- Comprehension checks every 10 minutes (keeps attention, reveals gaps)
- Examples from student's domain (not hypothetical)
- Visual examples always (reduce cognitive load from text)

**Comprehension Check Types:**
- Multiple choice (show 3-4 options, ask for raise of hands)
- Think-pair-share (students discuss answer with neighbor)
- Quick write (students answer on paper)
- Concept map (draw relationships between ideas)

**Red Flags:**
- Block with zero examples (abstract, hard to follow)
- No comprehension checks (can't tell if anyone is learning)
- Slides packed with text (students read, not listen)
- Learning objectives that are vague ("understand X" vs. "identify 3 properties of X")

---

### 6.2 How-To / Tutorial Format (10-20 slides, 10-60 minutes)

**Context:** Step-by-step skill-building. Goal: audience can replicate process independently.

**Structure Pattern:**
```
Opening (2 min) → Prerequisites (1 min) → Intro Block (2 min) → 
Step 1 (2 min) → Step 2 (2 min) → Step 3 (2 min) → ... → 
Capstone Exercise (5-10 min) → Troubleshooting (2 min) → Wrap-up (2 min)
```

**Slide-by-Slide (per step):**

| Slide | Content | Timing |
|-------|---------|--------|
| 1 | Step name and why it matters | 30 sec |
| 2 | Step instructions (numbered, clear, one action per line) | 1 min |
| 3 | Expected output (screenshot showing correct result) | 1 min |
| 4 | Common mistake (what if they do it wrong?) + Fix | Optional, 30 sec |

**Prerequisites Slide (Non-Negotiable):**
- Software/tools needed (with versions)
- Files to download or create
- Account setup (API keys, logins)
- Hardware or system requirements
- Estimated time to complete

**Troubleshooting Section (Content, Not Optional):**
```
Error 1: "X failed"
→ Cause: You skipped step Y
→ Fix: Go back and do step Y, then retry

Error 2: "Y is not found"
→ Cause: File in wrong location or wrong name
→ Fix: Check that file is named exactly Z and in folder W
```

**Capstone Exercise Slide:**
- Clear prompt (what should they create/do?)
- Success criteria (how do they know they got it right?)
- Screenshot of correct result
- Extension: bonus version if they finish early

**Red Flags:**
- Prerequisites unclear or scattered (people get stuck before starting)
- Expected output not shown (people don't know what "correct" looks like)
- Steps that are multi-part ("Now do X, Y, and Z") instead of single-action steps
- No troubleshooting section (creates frustration)
- Capstone exercise unrelated to steps taught (disconnect)

**Expected Output Slides Are Critical:**
Show exactly what the screen should look like after they complete the step. Include:
- Full screenshot or close-up detail
- Annotations calling out key elements
- Value/data they should see

---

## Part 7: Quick Reference

### 7.1 Slide Count and Timing Summary

**Presentation Type Reference Table:**

| Presentation Type | Slides | Duration | Audience | Pace |
|---|---|---|---|---|
| Lightning Talk | 5-7 | 5 min | Conference attendees | 1 slide per 45 sec |
| Investor Pitch | 11-12 | 18-22 min | VCs, Angels | 1-2 min per slide |
| Sales PAS | 8-10 | 20-30 min | Single prospect or small group | 2-3 min per slide |
| Feature Showcase | 15-20 | 30-45 min | Prospect post-discovery | 1.5-2.5 min per slide |
| Case Study | 8-12 | 10-20 min | Sales conversation | 1-2 min per slide |
| Project Status | 6-10 | 10-20 min | Steering committee | 1-2 min per slide |
| Technical Proposal | 8-14 | 20-40 min | Engineering team | 2-3 min per slide |
| QBR | 12-18 | 45-75 min | Executive leadership | 3-4 min per slide |
| Conference Talk | 25-35 | 25-30 min | 50-500 person audience | 45-60 sec per slide |
| Workshop (60 min) | 15-25 + exercises | 60 min | 20-30 person group | 50% instruction, 50% practice |
| Lecture (50 min) | 20-30 | 50 min | 30+ students | 3 comprehension checks |
| Tutorial | 10-20 | 10-60 min | Self-paced or small group | 1 action per slide + output shown |

---

### 7.2 Principle-to-Scenario Mapping

**Which framework to use when:**

| Framework | Best Applied To | Core Benefit | Why Use It |
|---|---|---|---|
| **Rule of Three** | All scenarios | Memorability, cognitive load | Humans retain 3 points reliably; 5+ degrades rapidly |
| **Minto Pyramid (SCQA)** | Executive briefings, consulting, strategy proposals | Respect for time, credibility | Answers first; builds supporting logic; high trust |
| **Duarte Sparkline** | Keynotes, fundraising, change management | Emotional engagement, behavior change | Oscillates between current reality and vision; inspires |
| **Assertion-Evidence** | Technical talks, academic, proposals, data-heavy | Comprehension, memory retention | Title claims, visuals prove; 65% better retention |
| **Storytelling Arc** | Sales, customer stories, internal change | Relatability, hero (not hero) positioning | Audience sees themselves; solution is tool, not protagonist |
| **PAS (Problem-Agitation-Solution)** | Sales, cold outreach, demos | Creates urgency, obvious answer | Agitation deepens pain; solution feels inevitable |
| **ADR (Architecture Decision Record)** | Technical proposals, tool selection, strategy | Demonstrable rigor, transparency | Equal options treatment, weighted criteria, documented trade-offs |
| **Kawasaki 10/20/30** | Startup pitches to any investor | Crisp, memorable, polished | Constraint forces discipline; 30pt font = focus on big idea |
| **Sequoia Format** | Investor pitch (mid to late stage) | Answer investor's actual question | "Why now?" as hinge pin; shows market timing instinct |
| **YC Format** | Investor pitch (any stage) | Clean design, traction focus | Emphasis on metrics; minimal fluff; one idea per slide |

---

### 7.3 Universal Slide Design Rules

**Rules that apply to every presentation type (no exceptions):**

| Rule | Rationale | How to Implement |
|---|---|---|
| **One idea per slide** | Cognitive overload kills retention | Limit slide to single claim, supported by one visual |
| **Slide title as full assertion, not topic label** | Preview the conclusion; helps audience follow logic | "Revenue grew 34% YoY due to SMB expansion" not "Revenue Trends" |
| **Minimum 24pt font for body, 44pt for titles** | Readability in medium-sized room | Test: can someone in back row read it easily? |
| **Visual evidence over bullets** | Images are processed 60,000x faster than text | Every data-heavy slide should have chart/diagram, not list |
| **One dominant visual per slide** | Clutter degrades comprehension | One chart, one screenshot, one diagram per slide (not three) |
| **Contrast for emphasis** | Highlighting with color/size focuses attention | Use accent color sparingly; bold key numbers |
| **Consistent template across deck** | Reduces cognitive load; feels professional | Same fonts, color palette, layout (headings always top-left) |
| **Final slide = summary or CTA (not "Thank You")** | Last slide is most memorable; use it | Summary of 3 key points OR specific next action for audience |
| **No more than 3 lines of text per slide** | Bullets kill engagement; people zone out | Each bullet = one complete thought; single line ideal |
| **Negative space is not wasted space** | Breathing room makes slides readable | Aim for 50% white space minimum |
| **No animation beyond simple fade/wipe transition** | Animation is distraction, not enhancement | Reveal bullets if necessary; no spinning, flying, or bouncing |
| **High contrast between text and background** | Accessibility + readability | Dark text on light (or vice versa); avoid mid-tone text on mid-tone background |
| **Every slide answers "So what?"** | Facts without implication bore audiences | Even data slides should state why this matters |
| **Color palette max 3 colors** | More colors = less cohesion | Primary + accent + neutral (white/gray); brand color is primary |

---

## Part 8: Implementation Guidance

### Content Creation Checklist (All Presentations)

Before you start building slides:

- [ ] **Audience analysis:** Who is watching? What do they need? What's their background?
- [ ] **Clear objective:** One sentence goal for this presentation (e.g., "Get funding commitment", "Approve technical direction", "Teach MySQL basics")
- [ ] **Constraints:** How much time do I have? How many slides? Live demo or safe mode?
- [ ] **Framework selection:** Which principle/structure best fits this scenario?
- [ ] **Outline:** Slide-by-slide outline (titles only) before creating any slides
- [ ] **Visuals planned:** What visual or screenshot goes on each slide? (Plan before creating)
- [ ] **Narrative arc:** Does the presentation have a beginning, middle, end? (Not just sequential)
- [ ] **CTA clarity:** What's the single action you want audience to take after?

### Review Checklist (Before Presenting)

- [ ] **Font legibility:** Every slide readable from back of room (24pt+ body, 44pt+ titles)
- [ ] **One idea per slide:** No slide tries to convince on 2+ ideas
- [ ] **Titles are assertions:** Every title is a full sentence claim, not topic label
- [ ] **Visuals support titles:** Every visual proves the assertion (not just decorative)
- [ ] **Transitions simple:** Only fade or wipe; no spinning or flying text
- [ ] **Color contrast:** Text is readable against background (not teal on green)
- [ ] **Template consistent:** Fonts, colors, layout same across all slides
- [ ] **Final slide is CTA or summary:** Not "Thank You"
- [ ] **Timing rehearsed:** Practiced entire presentation; know where to expand/trim
- [ ] **Demo safety plan:** If live demo, have screenshot backup (just in case)
- [ ] **Appendix ready:** Backup slides for tough questions (not presented unless asked)

---

## Part 9: Presentation Type Decision Tree

**Use this flowchart to pick the right structure:**

```
START: What's the primary goal?

├─ RAISE MONEY?
│  ├─ Early stage (pre-revenue/seed)?
│  │  └─ Use: YC Format or Kawasaki 10/20/30
│  └─ Later stage (Series A+)?
│     └─ Use: Sequoia Format + Investor Pitch Synthesis
│
├─ MAKE A SALE?
│  ├─ Cold prospect or initial conversation?
│  │  └─ Use: PAS (Problem-Agitation-Solution)
│  ├─ Post-discovery conversation (deep dive)?
│  │  └─ Use: Feature Showcase
│  └─ Proof for hesitant buyer?
│     └─ Use: Case Study
│
├─ INTERNAL BUSINESS DECISION?
│  ├─ Technical choice?
│  │  └─ Use: ADR-based Technical Proposal
│  ├─ Project status?
│  │  └─ Use: Project Status Update
│  └─ Executive review (quarterly)?
│     └─ Use: QBR (Quarterly Business Review)
│
├─ TEACH / TRAIN?
│  ├─ Academic lecture (50 min)?
│  │  └─ Use: Lecture Format + Assertion-Evidence
│  ├─ Step-by-step skill building?
│  │  └─ Use: How-To Tutorial
│  └─ Hands-on workshop (60+ min)?
│     └─ Use: Workshop Structure (40% teach, 50% practice)
│
├─ CONFERENCE / PUBLIC TALK?
│  ├─ Lightning round (5 min)?
│  │  └─ Use: Lightning Talk
│  ├─ Main stage (20-30 min)?
│  │  └─ Use: Standard Conference Talk + Assertion-Evidence
│  └─ Keynote (45-60 min)?
│     └─ Use: Duarte Sparkline
│
└─ END: Apply universal rules from Part 7.3
```

---

## Appendix: Glossary and Abbreviations

- **ADR:** Architecture Decision Record — Structured document for technical decisions
- **BLUF:** Bottom Line Up Front — State conclusion first, details second
- **CAC:** Customer Acquisition Cost — Marketing spend per new customer
- **LTV:** Lifetime Value — Total revenue from customer over relationship
- **OKR:** Objectives and Key Results — Goal-setting framework
- **PAS:** Problem-Agitation-Solution — Sales presentation framework
- **QBR:** Quarterly Business Review — Executive review of quarterly performance
- **RAG:** Red/Amber/Green — Status indicator (red = stopped, amber = at-risk, green = on track)
- **SAM:** Serviceable Available Market — Realistic addressable market segment
- **SCQA:** Situation-Complication-Question-Answer — Minto Pyramid structure
- **SOM:** Serviceable Obtainable Market — Conservative estimate of achievable market
- **TAM:** Total Addressable Market — Entire possible market for solution
- **Assertion-Evidence:** Title = claim, body = visual proof (not bullets)
- **Sparkline:** Oscillating narrative between current state and future vision
- **Rule of Three:** Limit core points to 3; retention degrades at 5+

---

**Document Version:** 1.0  
**Last Updated:** April 2026  
**Use Case:** AI-assisted presentation generation with reveal.js
