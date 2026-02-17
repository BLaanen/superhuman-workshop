# Presentation Redesign — Design Document

**Date:** 2026-02-17
**Goal:** Refine the Superhuman Workshop presentation to better explain ChatGPT limitations, context windows, team roles, and the GSD framework connection for a non-technical audience.

## Context

- **Format:** Presented live, then shared as a self-guided link
- **Audience:** Non-technical friends who want to build real projects with AI
- **Approach:** Empathy Narrative — start from their frustration, build understanding layer by layer
- **Scope:** Content restructure + visual design tweaks

## Slide Structure (~30 slides)

### Section 1: Opening (Slides 1-3)

**Slide 1 — Title**
- Title: "From Chatting to Building."
- Subtitle: "What happens when you stop asking AI questions and start building real things with it."
- Keep: SUPERHUMAN WORKSHOP label, current visual styling

**Slide 2 — Statement**
- "You've used ChatGPT. It's great for quick things — emails, brainstorming, explaining concepts. You type, it answers."

**Slide 3 — Statement**
- "But try building something *real* — a website, an app, a tool — and you hit a wall. Hard."

### Section 2: The Wall — ChatGPT Scenario (Slides 4-9)

**Slide 4 — Section Header**
- Label: "THE WALL"
- "Let's try building a website with ChatGPT."

**Slide 5 — Scenario Part 1** (styled as mock chat bubbles)
- You: "Make me a personal website"
- ChatGPT: gives you HTML code
- "Great! But... now what?"
- You have to: copy the code, find a text editor, create a file, paste it in, figure out how to open it in a browser
- Visual: mock ChatGPT-style chat bubbles (gray rounded rectangles)

**Slide 6 — Scenario Part 2**
- "Now change the headline."
- You paste the entire HTML back into ChatGPT
- It gives you a new version. Which parts changed? You can't tell.
- You replace the whole file and hope nothing broke.

**Slide 7 — Scenario Part 3**
- "A week later, you want to add a page."
- New conversation. ChatGPT has no idea what your site looks like.
- You're describing your own project from memory. Copy-pasting fragments.
- It gives you code that doesn't match what you already have.

**Slide 8 — The Four Limits** (summary)
- Now the four limits land because the audience just lived through them:
  1. Can't see your files (you were copy-pasting)
  2. Can't take action (you did all the manual work)
  3. Forgets everything (new conversation = start over)
  4. Freestyles (no consistent process)
- Visual: Same limit-row styling as current, but as a satisfying summary

**Slide 9 — Statement**
- "Chat AI is a brain in a jar. Smart — but no hands, no eyes, no workspace."

### Section 3: Context Windows (Slides 10-13)

**Slide 10 — Transition**
- "There's a deeper reason this happens."

**Slide 11 — The Whiteboard Metaphor**
- Label: "THE CORE CONSTRAINT"
- "The Context Window"
- "Every AI conversation is a whiteboard. You write on it as you talk. But the whiteboard has a fixed size. When it fills up, the AI starts erasing the oldest stuff to make room. That's why it 'forgets' — it's not dumb, it's running out of space."
- Visual: Animated bars (same as current but with whiteboard framing)
  - Quick question: 25% fill
  - Edit a page: 55% fill
  - Build entire website: overflows (red, fading out)

**Slide 12 — The Implication**
- "You can't describe an entire project in one conversation."
- "Not because the AI isn't smart enough — because it physically can't hold it all at once."

**Slide 13 — The Solution**
- "Break it into pieces that each fit."
- Visual: Four colored pieces (Homepage, Gallery, About, Deploy)
- "One conversation = one focused task. Not an entire project."

### Section 4: The Upgrade (Slides 14-16)

**Slide 14 — Statement**
- "We don't need a smarter chatbot. We need an AI that can actually work."

**Slide 15 — What We Need** (2x2 grid)
- See your files — Read the project, understand the structure
- Edit directly — Make changes in place, no copy-pasting
- Run commands — Test, build, deploy — actually do it
- Follow processes — Expert workflows, not freestyling

**Slide 16 — Evolution Stack**
- Chat/LLM → Agent → MCP & Tools → Claude Code → Spec-Driven → GSD (highlighted)
- Keep current visual styling

### Section 5: How Teams Build Software (Slides 17-20)

**Slide 17 — Section Header**
- Label: "THE PROFESSIONAL WAY"
- "How real products get built."

**Slide 18 — The Full Team** (2x4 grid with colored badges)
- Founder/CEO — Has the vision, sets the direction
- Product Manager — Translates vision into requirements, decides what to build
- Designer — Makes it look good and work well, user flows + visual design
- Architect — Plans the technical structure, how pieces connect
- Developer — Writes the actual code, implements the design
- QA/Tester — Breaks things on purpose to find bugs before users do
- DevOps — Gets it from "works on my computer" to live on the internet
- Project Manager — Tracks what's done, what's next, what's blocked

Color coding:
- Business roles: orange (accent)
- Product roles: purple
- Engineering roles: green
- QA roles: blue
- Operations: teal

**Slide 19 — The Process They Follow**
Show the flow:
1. Business defines vision and goals
2. Product researches and writes requirements
3. Design creates mockups and user flows
4. Architecture plans the technical approach
5. Development implements in sprints
6. QA tests against acceptance criteria
7. DevOps deploys to production
8. Everyone reviews and iterates

**Slide 20 — Statement**
- "This process works. It's how every app on your phone was built."
- "The problem? It requires an entire team and months of coordination."

### Section 6: GSD Does All Of This (Slides 21-24)

**Slide 21 — Anticipation**
- "What if one framework could replace this entire team?"

**Slide 22 — The Mapping** (two-column, staggered reveal)
| Traditional Team | You + GSD |
|---|---|
| Founder sets vision | You describe your vision |
| Product Manager writes requirements | /gsd:new-project interviews you |
| Project Manager scopes & sequences | Roadmap auto-generated |
| Designer + Architect plans approach | /gsd:plan-phase researches & plans |
| Developer writes & tests code | /gsd:execute-phase implements |
| QA verifies acceptance criteria | /gsd:verify-work checks results |
| DevOps deploys to production | git push → Vercel auto-deploys |

Each row staggers in with animation.

**Slide 23 — Statement**
- "From a team of 8 people to just you and a framework."
- "Same process. Same rigor."

**Slide 24 — GSD Hierarchy**
- Project → Milestone → Phases → Plans
- Keep current hierarchy visual + Plan → Build → Verify → Done flow

### Section 7: The System (Slides 25-27)

**Slide 25 — The Four Commands**
- /gsd:new-project — AI interviews you. Creates a project & roadmap.
- /gsd:plan-phase — Researches. Writes a detailed plan for your review.
- /gsd:execute-phase — Writes code. Makes commits. Runs checks.
- /gsd:progress — Where you are. Picks up where you left off.
- Session persistence rail (keep current visual)

**Slide 26 — The Tools**
- Claude Code — AI in your terminal. Reads files, edits code, runs commands.
- GitHub — Every change saved. Full history. You can always go back.
- Vercel — Push to GitHub, site deploys automatically. Free.

**Slide 27 — How Changes Go Live** (flow)
- You describe → Claude edits → Commit → Push → Live!

### Section 8: Walkthrough (Slide 28)

**Slide 28 — Empty Folder to Live Site** (timeline)
- /gsd:new-project — Claude asks creative questions
- Roadmap auto-generated — 4 phases scoped
- Plan → Build → Feedback → Refine — for each phase
- Deploy → Live URL — real website, zero code written by you

### Section 9: Close (Slides 29-31)

**Slide 29 — Universal**
- "This isn't just a software trick."
- "Vision → Break Down → Plan → Execute → Verify."
- "Whether you're building a website, launching a business, or renovating your apartment."

**Slide 30 — What You Walk Away With**
- A live personal website on your own URL
- The spec-driven methodology for any project
- A new mental model: orchestrating AI, not chatting with it
- Hands-on experience with Claude Code, GitHub, Vercel, GSD

**Slide 31 — Closing**
- "Ready to build?"
- Flow: Vision → Spec → Plan → Build → Verify → Ship
- "Let's go."

## Design Tweaks

### New visual elements:
1. **ChatGPT mock bubbles** — For slides 5-7, style text as gray rounded chat bubbles to visually evoke a ChatGPT conversation failing
2. **Team roles grid** — 2x4 grid with colored badge pills for each role (orange=business, purple=product, green=engineering, blue=QA, teal=ops)
3. **Two-column mapping** — For the GSD mapping slide, use a bridge/arrow layout between "Traditional Team" and "You + GSD" columns
4. **Staggered row reveals** — The mapping table rows animate in one by one for dramatic effect

### Refinements to existing:
- Context bars: reframe as "whiteboard filling up" (same visual, updated label language)
- Keep the warm dark palette (--bg: #0c0a09, --accent: #ff6b35)
- Keep Space Grotesk + Instrument Serif font pairing
- Keep all current animation patterns (stagger, popIn, growBar)

## What's Cut
- Comparison table (website vs apartment renovation) — replaced by statement slide
- "GitHub + Vercel" as separate detailed slide — consolidated into one tools slide
- Some redundant transition statements

## What's New
- 4 slides for ChatGPT failure scenario (slides 5-7 + summary)
- 1 slide for full team roster (8 roles grid)
- 1 slide for team process flow
- 1 slide for GSD anticipation ("What if one framework...")
- 1 slide for universal pattern statement
- Net: ~31 slides (up from 28)
