# Claude Code Custom Skills

Custom skills for Claude Code that combine death awareness (memento mori) with modern productivity frameworks (GTD) to create actionable life roadmaps.

## Skills Overview

Two **completely independent** skills combining GTD principles with memento mori philosophy - use one or both:

**1. Deathbed Clarity Roadmap** (63 questions) - **RECOMMENDED**
- Complete life transformation: death awareness + life vision → 90-day action plan
- Fully self-contained, includes all GTD concepts it needs
- The comprehensive option

**2. GTD Process Project** (33 questions) - **ALTERNATIVE**
- Simpler project analysis using GTD's 6 altitude levels
- No death work, just project/life analysis
- The lighter option

**Key Point:** Both skills work standalone. Deathbed is like a scientific calculator (has everything), GTD is like a basic calculator. Delete either one - the other still works perfectly.

---

### 1. Deathbed Clarity Roadmap ⭐ **(The Unified Skill)**

**Location:** `deathbed-clarity-roadmap/SKILL.md`
**Version:** 2.0.0
**Type:** Integrated Life Planning

A profound skill that unites death awareness with life vision to create practical 90-day action plans.

**What it does:**
- Guides you through a "24 hours to live" exercise to reveal true priorities
- Helps you define your wild success vision (3-5 years)
- Checks alignment between what matters facing death vs what you're building toward
- Generates detailed 90-day time-blocked roadmap with daily practices and commitment resolution

**The 5-Phase Journey:**

1. **Phase 1: Temporal Grounding** (Q1-5)
   - Current reality check
   - Past practices that worked
   - Energy and capacity assessment

2. **Phase 2: Memento Mori** (Q6-32)
   - Your ideal final 24 hours (hour by hour)
   - Bernard Fripp test (cramming vs continuing)
   - Deathbed panic list (incomplete commitments)
   - Distinction between panic items vs carried burdens

3. **Phase 3: Life Vision** (Q33-40)
   - Wild success in 3-5 years (where/with whom/doing what)
   - Vivid painting of ideal life
   - Negative vision (what to avoid)
   - Resonance, achievability, and energy tests

4. **Phase 4: Alignment Alchemy** (Q41-46) ✨ **THE SACRED UNION**
   - **Critical Question:** "If living your vision, would final 24 hours change?"
   - Reveals misalignment between aspirations and true priorities
   - Three-way integration (past-death-vision)
   - Keystone practice identification

5. **Phase 5: The 90-Day Roadmap** (Q47-63)
   - Keystone practice design (with MVP version)
   - Incomplete commitment action plans
   - Vision-aligned growth work
   - Resistance protocols and support structures
   - Detailed week-by-week calendar with specific time blocks

**Output:** A comprehensive org-mode document with:
- Executive summary
- Hour-by-hour final day breakdown
- Wild success vision painted vividly
- Alignment analysis
- 90-day calendar (Days 1-90, specific times and dates)
- Daily/weekly/monthly tracking tools
- Resistance protocols for when you don't want to continue
- Celebration milestones

**Use when:**
- Feeling unclear about life direction
- Wanting to align daily life with what truly matters
- Having incomplete commitments creating anxiety
- Ready for profound life transformation
- Need practical 3-month action plan

---

### 2. GTD Process Project

**Location:** `gtd-process-project/SKILL.md`
**Version:** 1.0.0
**Type:** Project/Life Analysis

A comprehensive GTD analysis tool using David Allen's 6 altitude levels (Runway to 50,000 feet).

**What it does:**
- Processes projects or life areas through 33 questions
- Checks vertical alignment from purpose → actions
- Provides priority rating (A-E)
- Generates detailed project analysis documents

**Two Types of Roadmap:**

**A. LIFE ROADMAP** - Analyzing how a project fits into your life structure
- **Areas** = Ongoing operational divisions of YOUR LIFE
- Examples: Spiritual Teaching, Financial Management, Health & Fitness, Publishing
- Use when: Understanding life-level priorities and balance

**B. PROJECT ROADMAP** - Analyzing internal structure of a specific project
- **Areas** = Functional domains WITHIN the project
- Examples: WHO (Personnel), WHERE (Locations), WHEN (Timing), HOW (Methods)
- Use when: Planning complex project execution

**The 6 Altitude Levels:**

- **50,000 ft:** Life purpose and principles (why you exist)
- **40,000 ft:** 3-5 year vision (where you're going)
  - Includes "Wild Success" questions: Where/with whom/doing what?
- **30,000 ft:** 1-2 year goals (major objectives)
- **20,000 ft:** Areas of focus (ongoing responsibilities)
- **10,000 ft:** Current projects (multi-step outcomes)
- **Runway:** Next physical actions (concrete, context-tagged)

**Key Features:**
- Physical action emphasis (truly doable right now)
- Dependency recognition (can't do X until Y is done)
- WHO-WHERE-WHEN-HOW framework for project areas
- Vertical alignment checking
- Priority assessment with decision recommendations

**Output:** Org-mode document with:
- Complete 6-level analysis
- Vertical integration assessment
- Priority rating (A-E)
- Decision recommendation (proceed/modify/defer/delete)
- Next physical actions with context tags

**Use when:**
- Starting a new project
- Feeling project misalignment
- Unclear about project priorities
- Need to check if project serves life purpose
- Want systematic project analysis

---

## How They Work Together

```
GTD Process Project          Deathbed Clarity Roadmap
(Project Analysis)           (Life Transformation)
       |                              |
       |                              |
       v                              v
  6 Altitude Levels    →→→→→    5-Phase Integration
  Vision Questions     →→→→→    Death Awareness
  Areas Framework      →→→→→    Alignment Check
       |                              |
       |                              |
       v                              v
  Project Document              90-Day Roadmap
  (Analysis)                    (Action Plan)
```

**The Relationship:**

- **GTD Process Project** provides the framework and questions for vision work
- **Deathbed Clarity Roadmap** integrates those questions with death awareness
- Together they ensure: What you're building (vision) = What matters (death priorities)

**The Critical Union:**

The Deathbed Clarity Roadmap asks the question that unites both concepts:

> *"If you were living your wild success vision (from GTD) and then got '24 hours to live' notice, would your final hours be DIFFERENT from the ones you described in your deathbed scenario?"*

- **If NO:** Perfect alignment → proceed with confidence
- **If YES:** Misalignment revealed → revise vision or deepen death awareness

---

## Installation & Usage

### Prerequisites

- [Claude Code](https://claude.com/claude-code) installed
- Skills directory: `~/.claude/skills/`

### Installing These Skills

1. **Clone this repository:**
   ```bash
   cd ~/.claude/skills/
   git clone <repository-url> .
   ```

2. **Or copy manually:**
   ```bash
   cp -r /path/to/deathbed-clarity-roadmap ~/.claude/skills/
   cp -r /path/to/gtd-process-project ~/.claude/skills/
   ```

3. **Verify installation:**
   ```bash
   ls ~/.claude/skills/
   # Should show: deathbed-clarity-roadmap/ gtd-process-project/
   ```

### Using the Skills

**In Claude Code CLI:**

```bash
# For life transformation and 90-day planning
/deathbed-clarity-roadmap

# For project analysis
/gtd-process-project
```

**Or via natural language:**
```
"I want to process my life using the deathbed clarity exercise"
"Analyze this project using GTD principles"
"Create a 90-day roadmap based on my deathbed priorities"
```

---

## Examples

### Example 1: Life Transformation (Deathbed Clarity Roadmap)

**User:** "I want to create a 90-day plan based on what truly matters"

**Agent guides through:**
1. Current life assessment
2. Final 24 hours scenario (reveals: morning practice, beach walks, calling son)
3. Wild success vision (living in Alicante, serving through books)
4. Alignment check → Perfect alignment discovered
5. 90-day roadmap generated:
   - Daily: 6:30-8:00 AM spiritual practice
   - Month 1-2: Complete NYC pilgrimage
   - Month 3: Establish sustainable practice

**Output:** Complete roadmap document + tracking tools

---

### Example 2: Project Analysis (GTD Process Project)

**User:** "Analyze my magazine distribution project using GTD"

**Agent asks:** "Is this a Life Roadmap or Project Roadmap?"
**User:** "Project Roadmap"

**Agent guides through:**
- **Runway:** Next physical actions (order stickers @computer)
- **10,000 ft:** Success = distribute all magazines
- **20,000 ft:** Areas = WHO (personnel), WHERE (10 distribution channels), WHEN (timing), HOW (methods)
- **30,000 ft:** No larger goal (tactical project)
- **40,000 ft:** No 3-5 year vision needed
- **50,000 ft:** Core value = SEVA (service)

**Alignment Check:** Bottom-up → Top-down
**Priority:** A - Critical (magazines printed 7 years ago!)
**Decision:** Proceed with full commitment

**Output:** Project analysis document with action plan

---

### Example 3: Combined Use

**Scenario:** User wants both project clarity AND life alignment

**Step 1:** Use `gtd-process-project` to analyze specific project
- Gets project structure
- Identifies areas and actions
- Checks alignment with purpose

**Step 2:** Use `deathbed-clarity-roadmap` for life integration
- Does project appear in deathbed priorities?
- Does it align with wild success vision?
- Should it be in the 90-day roadmap?

**Result:** Project analyzed AND integrated into life transformation plan

---

## Key Concepts

### Memento Mori (Remember You Will Die)
Ancient Stoic practice of contemplating mortality to clarify priorities. Used in Phase 2 to reveal what truly matters.

### Bernard Fripp Test
From 1968 film where character tries to cram meaningful life into 30 minutes before death. Test measures: Are you CRAMMING (desperate) or CONTINUING (peaceful)?

### Keystone Practice
The ONE practice that appears in: (1) what worked before, (2) final 24 hours, (3) ideal future, and (4) is missing from current life. Becomes the foundation of the 90-day roadmap.

### Alignment Alchemy
The sacred union between deathbed priorities and life vision. Ensures you're not building toward something that won't matter when facing death.

### GTD 6 Altitude Levels
David Allen's framework for vertical alignment:
- Higher levels (purpose, vision) inform lower levels
- Lower levels (actions, projects) should serve higher levels
- Misalignment at any level creates drift or overwhelm

### WHO-WHERE-WHEN-HOW Framework
For Project Roadmaps, areas are often functional divisions:
- WHO: Personnel and team
- WHERE: Locations and channels
- WHEN: Timing and scheduling
- HOW: Methods and execution

### Minimum Viable Practice (MVP)
The smallest version of a practice that still "counts." Week 1 starts with MVP to build momentum before expanding.

---

## File Structure

```
.claude/skills/
├── README.md (this file)
├── .gitignore
├── deathbed-clarity-roadmap/
│   └── SKILL.md (v2.0 - 1072 lines - 63 questions)
└── gtd-process-project/
    └── SKILL.md (v1.0 - 33 questions)
```

---

## Philosophy

### The Core Insight

**Most people live according to:**
- What they think they "should" do
- What society expects
- What brings status or money
- Vague future plans

**But facing death reveals:**
- What ACTUALLY matters
- Who they TRULY want with them
- What practice brings REAL peace
- What they GENUINELY regret leaving incomplete

**The Problem:** By the time you face death, it's too late to change.

**The Solution:** Face death NOW (mentally) to gain clarity, THEN build life that honors that clarity.

**The Test:** If you got "24 hours to live" notice after completing the 90-day roadmap, you'd simply CONTINUE what you're already doing. No panic. No regret. No desperate cramming.

---

## Contributing

This is a personal skill repository, but if you fork it:

1. **Maintain the integration** - Don't break the connection between death awareness and vision work
2. **Keep questions profound** - Surface questions get surface answers
3. **Preserve the structure** - 5 phases build on each other
4. **Test thoroughly** - These questions go deep; ensure your changes maintain psychological safety
5. **Document well** - Clear examples help users understand the process

---

## Credits

**Inspired by:**
- David Allen - Getting Things Done (GTD) methodology
- Marcus Aurelius - Memento mori practice
- Stoic philosophy - Death awareness for life clarity
- "30 is a Dangerous Age, Cynthia" (1968) - Bernard Fripp character

**Created with:**
- Claude Code (claude.com/claude-code)
- Claude Sonnet 4.5
- Human insight and lived experience

---

## License

These skills are provided as-is for personal use. The frameworks (GTD, Stoicism) are in public domain. The specific integration and question structure is original work.

---

## Version History

### v2.0.0 - Deathbed Clarity Roadmap (2026-01-08)
- Complete rewrite with 5-phase integration
- Added Phase 1: Temporal Grounding (past practices)
- Enhanced Phase 2: Hour-by-hour death scenario (Q6-Q32)
- Enhanced Phase 3: Wild success vision with tests (Q33-Q40)
- Added Phase 4: Alignment Alchemy - the sacred union (Q41-Q46)
- Enhanced Phase 5: Detailed 90-day calendar with time blocks
- Total: 63 questions across 5 integrated phases

### v1.0.0 - GTD Process Project (2026-01-07)
- Initial release
- 33 questions across 6 altitude levels
- Life Roadmap vs Project Roadmap distinction
- WHO-WHERE-WHEN-HOW framework
- Wild Success vision questions
- Physical action emphasis

---

## Quick Start Guide

**For Life Transformation:**
```bash
# Start the profound journey
/deathbed-clarity-roadmap

# Answer honestly (30-60 minutes)
# Receive comprehensive 90-day roadmap
# Begin Day 1 tomorrow
```

**For Project Analysis:**
```bash
# Analyze any project
/gtd-process-project

# Choose: Life Roadmap or Project Roadmap
# Answer 33 questions
# Receive priority rating and decision
```

**The Goal:**
> In 90 days, if death comes, there's no panic.
> Just peaceful continuation of a life well-lived.

---

**Repository:** `~/.claude/skills/`
**Contact:** Created for personal use with Claude Code
**Last Updated:** 2026-01-08
