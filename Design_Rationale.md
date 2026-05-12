# Leadership Portfolio: Design Rationale Document

**Submitted by:** Vidit Bansal  
**Date:** May 12, 2026  
Part A - Design Rationale

---

## Summary

This document explains the design decisions behind the Leadership Portfolio redesign, transforming it from a dashboard-style monitoring interface into a narrative-first career pitch deck. The working prototype demonstrates a chapter-style layout where data serves the story rather than dominating it, with clear visual hierarchy, prominent employee identity, and progressive disclosure of complexity.

---

## 1. Core Design Philosophy: Pitch Deck, Not Dashboard

### The Transformation

**From:** Metric widgets in a grid, all with equal visual weight  
**To:** Narrative chapters with a clear reading flow, where the headline tells the story and data provides proof

### Why This Matters

The portfolio follows an employee for their entire career via a permanent UID. It's not a monitoring tool for supervisors, it's a career artefact the employee owns and would show to a mentor or future employer. The design needed to feel **dignified, personal, and narrative-driven** rather than clinical and metric-heavy.

### Implementation Decisions

1. **Chapter-based scroll experience** - Each of the 6 sections feels like a chapter in a story, not a widget on a dashboard
2. **Story-first ordering** - Narrative paragraphs appear prominently with data as supporting evidence, not footnotes below charts
3. **Scroll progress indicator** - Subtle top bar showing reading progress, reinforcing the "document you read" rather than "dashboard you scan" mental model
4. **Side navigation with chapter numbers** - Desktop users get a persistent nav showing "01 Highlights", "02 Capability", etc., reinforcing the narrative arc

---

## 2. Design Challenges Addressed

### Challenge 1: The Signal (Most Critical)

**Problem:** What should the employee see in the first 3 seconds?

**Position Taken:** **Compelling headline + human narrative over raw composite score**

**Implementation:**
- Opening headline: "Regulatory blocker cleared. Facility 3 moves toward commercial launch."
- This is derived from analysing the narrative and contribution data to extract the most significant accomplishment
- Composite score (71/100) is present but secondary, shown as a bento-style card alongside employee identity
- A clear "Pace: Ahead" indicator provides the career trajectory signal without numerical anxiety

**Why This Works:**
- A headline like "Regulatory blocker cleared" immediately tells a story; it's something Rajan would be proud to share
- The composite score is available for those who want the number, but it doesn't dominate the page
- The narrative paragraph explains the **why** behind the score jump (64 → 71)

**Alternative Considered:** A large score ring (72/100) at the top, like Experiment 1  
**Why Rejected:** Felt too clinical, like a report card grade rather than a career story

---

### Challenge 2: Story vs Data Ordering

**Problem:** Should sections lead with narrative or data?

**Position Taken:** **Narrative-first for all sections, with data as visual proof**

**Implementation:**
- Each section starts with the `ChapterHeader` component showing index number, eyebrow label, title, and subtitle
- The narrative paragraph appears in a distinct "The Story" component with a subtle background and border
- Data visualisations, tables, and metrics appear **after** the narrative context is established
- Exception: Cover section shows identity + score bento **before** the executive narrative, because readers need to know "whose story is this?"

**Why This Works:**
- When Rajan opens his portfolio, he first reads "what's the story this month?" before diving into axis scores
- For supervisors reviewing the portfolio, the narrative provides context before the numbers
- Data without narrative is just numbers, narrative without data is just opinion. Story-first ordering gives both audiences what they need

**Tradeoff Acknowledged:**
Some supervisors may prefer numbers-first for efficiency during reviews. A future iteration could include a "Data View" toggle that reorders sections to lead with metrics.

---

### Challenge 3: Six Sections. Too Many?

**Problem:** Is six sections overwhelming for a monthly document?

**Position Taken:** **Keep all six, but create a clear visual hierarchy and progressive disclosure**

**Implementation:**
1. **Cover (Section 00)** - Hero section with identity + score + headline narrative  
2. **Highlights (Section 01)** - Featured win + deliverable throughput + IP commit timeline  
3. **Capability (Section 02)** - Radar chart + score breakdown + tabbed evidence (Frameworks / Processes / Rituals)  
4. **KPI Impact (Section 03)** - Tabbed view (All / Hits / Misses) with target vs actual bars  
5. **Constraints (Section 04)** - Resolution rate + type breakdown + top 5 constraint cards  
6. **Trajectory (Section 05)** - Career milestone timeline + gap drivers + time distribution

**Progressive Disclosure Strategy:**
- The Capability section uses **tabs** (Frameworks / Processes / Rituals) to collapse details without removing them
- KPI section uses **filter tabs** (All / Hits / Misses) to let users focus on what matters to them
- Constraint cards are **collapsible-style** with hover interaction, reducing visual weight until needed

**Why Six Sections Remain:**
Each section answers a distinct question:
1. Cover: "How am I doing overall?"
2. Highlights: "What did I ship?"
3. Capability: "How am I developing?"
4. KPIs: "Did I hit targets?"
5. Constraints: "What blocked me?"
6. Trajectory: "Where am I headed?"

Removing any section would leave a gap in the career narrative. The solution isn't fewer sections; it's better information architecture within each section.

---

### Challenge 4: The Constraint Section, Honesty Without Anxiety

**Problem:** How to present "what blocked me" without making the portfolio feel like a complaint document?

**Position Taken:** **Frame constraints as professional diagnostic data, not personal failures**

**Implementation:**
- Section title: "What blocked progress" (neutral, factual) rather than "Problems" or "Issues"
- Lead with **resolution rate** (62% resolved this month) to show action, not just obstacles
- Constraint type breakdown (budget, talent, internal support, etc.) presented as **categorical data**, like a Pareto chart
- Individual constraint cards show:
  - Ticket ID (CST-0421) for traceability
  - Type badge (assumptions, internal support, etc.)
  - Status badge (Resolved / Open) with appropriate colour treatment
  - Descriptive label that explains the blocker without blame

**Visual Tone:**
- Resolved constraints get a green checkmark icon, reinforcing that blockers were overcome
- Open constraints get a clock icon (not a red X) indicating "in progress" rather than "failure"
- The narrative explains **what was learned** from constraints (e.g., "Rajan resolved the regulatory bottleneck by switching to joint review sessions, which now saves 3 weeks per protocol")

**Why This Works:**
Constraints are reframed as **organisational learning opportunities** rather than personal shortcomings. The resolution rate and narrative show that raising constraints is a sign of professional maturity, not incompetence.

**Alternative Considered:** Hide constraints in a collapsed section by default  
**Why Rejected:** Constraints are essential diagnostic data. Hiding them implies shame, which contradicts the "physics-grade transparency" philosophy of PDGMS.

---

### Challenge 5: Portability and Identity

**Problem:** The portfolio must work inside and outside the organisation (permanent UID follows the employee)

**Position Taken:** **Prominent identity, plain-language labels, organisational context without jargon**

**Implementation:**

**Identity Prominence:**
- Employee name, role, program, organisation shown in a **dedicated identity card** on the cover
- Portfolio ID and UID displayed in **header utility bar** (always visible on scroll)
- Month period (2026-03-01 → 2026-03-31) and generation timestamp in footer
- GitHub link to assignment submission in footer (for this prototype)

**Jargon Translation:**
- "IP Commits" → **"Original Work"** (axis label on radar chart)
- "Deliverables" → **"Delivery"** (axis label on radar chart)
- "Rituals" → **"Engagement"** (axis label on radar chart)
- "QA Pending" → **"Pending QA"** (status label)
- Framework/Process scores shown as **"Evidence behind the scores"** with detail tabs

**Organisational Context (Retained):**
- V-level shown (V2, V3, etc.) because it's part of the employee's career identity
- Program name shown ("Facility 3 Commercialisation") because it contextualises the work
- Career ladder ID shown ("LADDER-MFG-001") for traceability

**Why This Balance:**
The portfolio needs to make sense to:
1. The employee themselves (primary audience)
2. A mentor outside the organisation (secondary audience)
3. A future employer reading it 5 years later (tertiary audience)

Plain-language labels make the axes understandable. Retaining V-levels and ladder IDs preserves the career scaffolding without requiring the reader to understand the full PDGMS 5×5 grid.

---

## 3. Custom Components and Technical Decisions

### Custom Radar Chart

**Why Built from Scratch:**
- The Recharts library could not reliably render asymmetric polygons; all vertices kept snapping to the threshold value (60)
- Needed pixel-perfect control over:
  - Score polygon (actual performance: 80, 74, 68, 52, 58, 85)
  - Threshold reference ring (dashed circle at 60)
  - Axis labels positioned outside the chart
  - Data-driven rendering (change scores in data → polygon updates automatically)

**Implementation:**
- Pure SVG with calculated polar-to-cartesian coordinate transforms
- Takes `data` array (axis names + scores) and `threshold` value as props
- Fully responsive to data changes, no hardcoded shapes

**Visual Design:**
- Score polygon: filled with `--primary` colour at 25% opacity, stroked at 100%
- Threshold ring: dashed stroke in `--muted-foreground` at 50% opacity
- Circular grid levels at 20, 40, 60, 80, 100
- Score dots at polygon vertices with a stroke for visibility

This ensures the radar chart **feels alive** when capability scores change in the data, the polygon shape visually reflects that asymmetry.

---

### Design System Integration

**Colour Variables (CSS custom properties):**
```css
--primary, --primary-foreground
--secondary, --secondary-foreground
--muted, --muted-foreground
--card, --border
--accent, --accent-foreground
--destructive
--background, --foreground
```

All UI elements reference these variables, so the entire colour scheme can be updated by editing the CSS file.

**Typography:**
- Font sizes specified inline via `style={{ fontSize: "..." }}` to override Tailwind defaults
- Font weights explicitly set where needed (600 for headings, 500 for labels)
- All text inherits from font faces defined in the design system CSS

**Component Primitives:**
- `ChapterHeader` - Consistent section header with icon, index, eyebrow, title, subtitle
- `Narrative` - Distinct card for story paragraphs with "The Story" label
- `Pill` - Reusable badge component with tone variants (neutral, positive, warning, negative)
- `Counter` - Animated count-up effect for all numeric displays
- `DonutGauge` - Circular completion percentage visualisation

---

## 4. What I Would Do Differently With More Time

### 1. Dynamic Headline Generation
**Current State:** Headline is hardcoded ("Regulatory blocker cleared...")  
**Ideal State:** Server-side analysis of contribution data to auto-generate a compelling headline using deterministic templates (not LLM)

**Approach:**
- If `completed deliverables > 80%` AND `compositeScore delta > 5`: "Strong delivery month"
- If `any KPI.status === 'hit'` AND `topCommit.description` contains breakthrough keyword: Extract that achievement as headline
- Fallback to composite score change narrative if no standout achievement

---

### 2. Constraint Impact Visualisation
**Current State:** Constraint resolution rate + type breakdown + top 5 list  
**Ideal State:** Visual timeline showing when constraints were raised vs resolved, with impact on deliverable velocity

**Mockup Concept:**
- Horizontal timeline of the month (Week 1-4)
- Constraint cards positioned at the raise date, with resolution shown as timeline completion
- Overlay deliverable completion rate to show correlation between constraint resolution and throughput

This would make the "8 raised, 5 resolved" stat feel more concrete and show the **operational impact** of blockers.

---

### 3. Comparison to Prior Months
**Current State:** Single-month view with delta from previous month (64 → 71)  
**Ideal State:** Sparkline trend of the last 6 months for each axis score

**Why:**
A 3-month upward trend in Framework score (45 → 48 → 52) tells a different story than a volatile pattern (60 → 42 → 52). Trends reveal growth trajectory better than single-month snapshots.

**Implementation Challenge:**
Requires `CareerRunrateSnapshot` history data, which exists in the backend but isn't currently fed into the portfolio response.

---

### 4. Mobile-First Responsive Refinement
**Current State:** Responsive breakpoints using Tailwind grid (`lg:col-span-7`, `md:grid-cols-2`)  
**Ideal State:** Mobile-optimised section order and chart simplification

**Specific Changes:**
- On mobile, show radar chart **score breakdown list only** (no SVG radar) easier to scan on small screens
- Collapse career timeline to vertical milestone list on mobile
- KPI bars stack vertically with targets shown inline, not as separate pills

---

### 5. Accessibility Enhancements
**Current State:** Basic semantic HTML, colour contrast meets WCAG AA  
**Ideal State:** Full keyboard navigation, ARIA labels, screen reader optimisation

**Specific Additions:**
- `aria-label` on the radar chart explaining each axis and score
- Keyboard shortcuts: `1-6` to jump to sections, `n/p` for next/prev month navigation
- High-contrast mode toggle (for users with visual impairments)
- Screen reader announcement: "Composite score 71, up 7 points from last month"

---

## 5. Assumptions Made About User Behaviour and Data

### User Behaviour Assumptions

1. **Employees open the portfolio monthly, not daily**  
   → Designed for **deep reading** (narrative paragraphs, scroll experience) rather than quick scanning (widget dashboard)

2. **Supervisors review 5-10 portfolios per session**  
   → Consistent structure across all portfolios (same 6 sections, same order) allows muscle-memory navigation

3. **Employees share portfolios with mentors outside the organisation**  
   → Jargon translated to plain language, organisational context (V-levels, programs) retained but explained

4. **The "pace ahead/behind" signal is emotionally significant**  
   → Prominently displayed on cover with positive tone ("Ahead by ~3 months") rather than buried in trajectory section

5. **Constraints are viewed as learning opportunities, not failures**  
   → Resolution rate highlighted first, individual constraints shown with type/status rather than blame language

---

### Data Assumptions

1. **Narratives are pre-generated by the backend**  
   → UI renders `narrative` field as-is. If the backend returns `null`, the section shows data without a narrative context

2. **Composite score always exists**  
   → Cover section assumes `compositeScore` and `previousMonthScore` are present. If missing, would need fallback UI

3. **Radar chart axes are always 6**  
   → Custom radar chart hardcoded for 6 axes (deliverables, IP, KPIs, frameworks, processes, rituals). Adding a 7th axis would require a code change

4. **Career milestones array contains exactly 5 levels (V1-V5)**  
   → Timeline visualisation assumes 5 evenly spaced milestones. Shorter or longer arrays would require layout adjustment

5. **At least one "featured win" exists in contribution data**  
   → Currently hardcoded to the first `recentCommits[0]`. If the array is empty, the section would show "No IP commits this month"

6. **Time distribution categories match enum exactly**  
   → Assumes `timeDistribution` object contains `operational`, `research`, `deep_work`, `coordination`, `meetings`, `planning_strategy`. no more, no less

---

## 6. Conclusion

This Leadership Portfolio redesign transforms a metric-heavy dashboard into a **narrative-first career artefact** that employees would be proud to share. The design prioritises:

**Story over data**: narratives lead, metrics support  
**Clear visual hierarchy**: one signal dominates (headline + score), detail is progressively disclosed  
**Portability**: plain language, prominent identity, works outside organisational context  
**Honesty without anxiety**: constraints shown as diagnostic data, not failures  
**Data fidelity**: every element maps to the backend data model, no invented fields  

The working prototype demonstrates that a pitch deck mindset, where data serves the story rather than being the story, is achievable within the technical constraints of the PDGMS data model.

---

**End of Design Rationale Document**

*contact: viditbansal2020@gmail.com*  
