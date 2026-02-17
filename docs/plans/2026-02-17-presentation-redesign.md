# Presentation Redesign — Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Restructure the Superhuman Workshop presentation from 28 to ~35 slides, adding "The Moment" opening with stats/quotes, improving ChatGPT limitation narrative, context windows, team roles, GSD mapping reveal, and a Bo case study.

**Architecture:** Single-file HTML slide deck (`presentation.html`) with embedded CSS and JS. The existing slide engine (keyboard/touch/click navigation, progress bar, stagger animations) stays intact. We add new CSS components (chat bubbles, team grid, two-column mapping) and restructure the slide HTML content.

**Tech Stack:** Vanilla HTML/CSS/JS, Google Fonts (Space Grotesk + Instrument Serif)

**Design doc:** `docs/plans/2026-02-17-presentation-redesign-design.md`

---

### Task 0: Add "The Moment" CSS + Stats Slides (New Section 0)

**Files:**
- Modify: `presentation.html` — add CSS for stat cards and quote styling, then add 4 new slides after the title

**Step 1: Add stat/quote CSS styles**

Add before the `@media` query:

```css
/* ===== STAT CARDS ===== */
.stat-grid {
  display: grid; grid-template-columns: 1fr 1fr; gap: 20px;
  width: 100%; margin-top: 40px;
}

.stat-card {
  padding: 28px 24px; background: var(--surface);
  border: 1px solid var(--border); border-radius: 12px;
  text-align: center;
}

.stat-card .stat-num {
  font-size: 48px; font-weight: 700; color: var(--accent);
  line-height: 1; margin-bottom: 8px;
}

.stat-card .stat-label {
  font-size: 18px; color: var(--text-dim); line-height: 1.4;
}

/* ===== QUOTE BLOCKS ===== */
.quote-block {
  border-left: 3px solid var(--accent); padding: 20px 28px;
  margin-bottom: 20px; background: var(--accent-dim);
  border-radius: 0 12px 12px 0;
}

.quote-block .quote-text {
  font-family: var(--serif); font-style: italic;
  font-size: 28px; color: var(--text); line-height: 1.4;
  margin: 0 0 8px;
}

.quote-block .quote-attr {
  font-size: 16px; color: var(--text-faint); font-weight: 600;
  margin: 0;
}

/* ===== PROOF POINTS ===== */
.proof-point {
  padding: 16px 0; border-bottom: 1px solid var(--border);
  font-size: 24px; color: var(--text-dim);
}

.proof-point:last-child { border: none; }
.proof-point .proof-hl { color: var(--accent); font-weight: 700; }
```

**Step 2: Add slide 2 — quotes**

Insert after slide 1 (title):

```html
<!-- 2: THE MOMENT - QUOTES -->
<div class="slide">
  <div class="content stagger">
    <div class="label">The Moment</div>
    <h2>Something is <span class="hl">happening.</span></h2>
    <div style="margin-top: 32px;">
      <div class="quote-block">
        <p class="quote-text">"When will we see the first one-person billion-dollar company? <span class="hl">2026.</span>"</p>
        <p class="quote-attr">Dario Amodei, CEO of Anthropic (maker of Claude)</p>
      </div>
      <div class="quote-block">
        <p class="quote-text">"You'll have billion-dollar companies run by <span class="hl">two or three people</span> with AI."</p>
        <p class="quote-attr">Sam Altman, CEO of OpenAI</p>
      </div>
    </div>
  </div>
</div>
```

**Step 3: Add slide 3 — stats**

```html
<!-- 3: THE MOMENT - STATS -->
<div class="slide">
  <div class="content stagger">
    <div class="label">The Numbers</div>
    <h2>The numbers are <span class="hl">insane.</span></h2>
    <div class="stat-grid">
      <div class="stat-card">
        <div class="stat-num">41%</div>
        <div class="stat-label">of all code is now<br>AI-generated</div>
      </div>
      <div class="stat-card">
        <div class="stat-num">95%</div>
        <div class="stat-label">AI-generated codebases<br>at 25% of YC startups</div>
      </div>
      <div class="stat-card">
        <div class="stat-num">+24%</div>
        <div class="stat-label">App Store submissions<br>biggest wave since 2016</div>
      </div>
      <div class="stat-card">
        <div class="stat-num">92%</div>
        <div class="stat-label">of US developers use<br>AI coding tools daily</div>
      </div>
    </div>
  </div>
</div>
```

**Step 4: Add slide 4 — proof points / sleeping on it**

```html
<!-- 4: SLEEPING ON IT -->
<div class="slide">
  <div class="content stagger">
    <div class="label">Right Now</div>
    <h2>Most people are<br><span class="hl">sleeping on this.</span></h2>
    <div style="margin-top: 32px;">
      <div class="proof-point"><span class="proof-hl">Cursor</span> hit $1B revenue in 17 months &mdash; with fewer than 50 employees</div>
      <div class="proof-point"><span class="proof-hl">Replit</span> grew 2,352% in one year turning non-coders into builders</div>
      <div class="proof-point">A <span class="proof-hl">solo founder</span> sold his AI-built startup for $80M in 6 months</div>
      <div class="proof-point">MVP costs dropped from <span class="proof-hl">$80K / 4 months</span> to <span class="proof-hl">$2K / 8 days</span></div>
    </div>
    <p style="margin-top: 32px; font-size: 24px; color: var(--accent); font-weight: 600;">The tools you'll learn today are the ones making this happen.</p>
  </div>
</div>
```

**Step 5: Add slide 5 — transition**

```html
<!-- 5: TRANSITION -->
<div class="slide">
  <div class="content centered stagger">
    <p class="statement">And most people<br>are still using AI<br><span class="hl">like this...</span></p>
  </div>
</div>
```

**Step 6: Verify slides 1-5 in browser, commit**

```bash
git add presentation.html
git commit -m "content: add 'The Moment' opening slides with stats and quotes"
```

---

### Task 1: Add New CSS Components

**Files:**
- Modify: `presentation.html` — the `<style>` block (lines ~10-406)

**Step 1: Add chat bubble styles**

Add after the `.idea-strip` styles (around line 362), before the `@media` query:

```css
/* ===== CHAT BUBBLES (ChatGPT scenario) ===== */
.chat-scene { width: 100%; max-width: 700px; margin-top: 32px; }

.chat-bubble {
  padding: 18px 24px; border-radius: 18px;
  font-size: 22px; line-height: 1.5; margin-bottom: 14px;
  max-width: 85%; position: relative;
}

.chat-bubble.user {
  background: #2a5fdd; color: #fff;
  margin-left: auto; border-bottom-right-radius: 4px;
}

.chat-bubble.ai {
  background: #2a2723; color: var(--text-dim);
  border-bottom-left-radius: 4px; border: 1px solid var(--border);
}

.chat-bubble .chat-label {
  font-size: 13px; font-weight: 700; letter-spacing: 1px;
  text-transform: uppercase; margin-bottom: 6px; display: block;
}

.chat-bubble.user .chat-label { color: rgba(255,255,255,0.5); }
.chat-bubble.ai .chat-label { color: var(--text-faint); }

.chat-result {
  margin-top: 20px; padding: 16px 20px;
  border-left: 3px solid var(--accent);
  font-size: 24px; color: var(--text-dim); font-weight: 500;
}
```

**Step 2: Add team grid styles**

```css
/* ===== TEAM GRID ===== */
.team-grid {
  display: grid; grid-template-columns: 1fr 1fr;
  gap: 14px; width: 100%; margin-top: 36px;
}

.team-card {
  padding: 20px 24px; background: var(--surface);
  border-radius: 12px; border-left: 3px solid var(--text-faint);
  transition: transform 0.3s;
}

.team-card:hover { transform: translateX(4px); }

.team-card h4 {
  font-size: 22px; font-weight: 700; margin-bottom: 4px;
}

.team-card p {
  font-size: 18px; color: var(--text-dim); margin: 0; max-width: none;
}

.team-card.role-biz { border-left-color: var(--accent); }
.team-card.role-biz h4 { color: var(--accent); }

.team-card.role-prod { border-left-color: #c084fc; }
.team-card.role-prod h4 { color: #c084fc; }

.team-card.role-eng { border-left-color: #34d399; }
.team-card.role-eng h4 { color: #34d399; }

.team-card.role-qa { border-left-color: #38bdf8; }
.team-card.role-qa h4 { color: #38bdf8; }

.team-card.role-ops { border-left-color: #2dd4bf; }
.team-card.role-ops h4 { color: #2dd4bf; }
```

**Step 3: Add two-column mapping styles**

```css
/* ===== MAPPING TABLE (GSD reveal) ===== */
.map-row {
  display: flex; align-items: center; gap: 16px;
  padding: 18px 0; border-bottom: 1px solid var(--border);
}

.map-row:last-child { border: none; }

.map-col-left {
  flex: 1; font-size: 22px; color: var(--text-dim); text-align: right;
  padding-right: 16px;
}

.map-arrow {
  color: var(--accent); font-size: 24px; flex-shrink: 0; font-weight: 700;
}

.map-col-right {
  flex: 1; font-size: 22px; color: var(--accent); font-weight: 600;
  padding-left: 16px;
}
```

**Step 4: Add responsive overrides for new components**

Add inside the existing `@media (max-width: 900px)` block:

```css
.team-grid { grid-template-columns: 1fr; }
.chat-bubble { max-width: 95%; }
.map-col-left, .map-col-right { font-size: 18px; }
```

**Step 5: Verify in browser**

Open `presentation.html` in a browser. Existing slides should look identical (no regressions). New styles won't be visible yet.

**Step 6: Commit**

```bash
git add presentation.html
git commit -m "style: add chat bubble, team grid, and mapping table CSS"
```

---

### Task 2: Restructure Opening Slides (Slides 1-3)

**Files:**
- Modify: `presentation.html` — slide 1 (the `active` slide), slides 2-3

**Step 1: Update slide 1 (title)**

Replace the content of slide 1 (currently "From Chatbots to Conductors"):

```html
<!-- 1: TITLE -->
<div class="slide active">
  <div class="content centered stagger">
    <div class="label">Superhuman Workshop</div>
    <h1>From Chatting<br>to <span class="hl">Building.</span></h1>
    <p style="margin-top: 24px;">What happens when you stop asking AI questions<br>and start building real things with it.</p>
  </div>
</div>
```

**Step 2: Keep slide 2 but update copy**

```html
<!-- 2 -->
<div class="slide">
  <div class="content centered stagger">
    <p class="statement">You've used ChatGPT. It's great for quick things &mdash; emails, brainstorming, explaining concepts. You type, it answers.</p>
  </div>
</div>
```

**Step 3: Keep slide 3 but update copy**

```html
<!-- 3 -->
<div class="slide">
  <div class="content centered stagger">
    <p class="statement">But try building something <span class="hl">real</span> &mdash; a website, an app, a tool &mdash; and you hit a wall. <span class="hl">Hard.</span></p>
  </div>
</div>
```

**Step 4: Verify slides 1-3 in browser**

Navigate with arrow keys. Check title renders correctly, stagger animations work.

**Step 5: Commit**

```bash
git add presentation.html
git commit -m "content: update opening slides — from chatting to building"
```

---

### Task 3: Build ChatGPT Scenario Slides (Slides 4-9)

**Files:**
- Modify: `presentation.html` — replace current slides 4-7

**Step 1: Replace slide 4 with section header**

Replace the current slide 4 ("Chat AI has four hard limits"):

```html
<!-- 4: THE WALL -->
<div class="slide">
  <div class="content stagger">
    <div class="label">The Wall</div>
    <h2>Let's try building a website<br>with <span class="hl">ChatGPT.</span></h2>
  </div>
</div>
```

**Step 2: Replace slide 5 with scenario part 1**

Replace the current slide 5 (limits 1-2):

```html
<!-- 5: SCENARIO 1 -->
<div class="slide">
  <div class="content stagger">
    <div class="chat-scene">
      <div class="chat-bubble user">
        <span class="chat-label">You</span>
        Make me a personal website. Clean, modern, professional.
      </div>
      <div class="chat-bubble ai">
        <span class="chat-label">ChatGPT</span>
        Sure! Here's a complete HTML file for a modern personal website...
        <span style="display:block;margin-top:8px;font-family:monospace;font-size:16px;color:var(--text-faint);">&lt;!DOCTYPE html&gt;<br>&lt;html lang="en"&gt;<br>&lt;head&gt;...<br><br>...247 lines of code</span>
      </div>
    </div>
    <div class="chat-result">Great! But... now what?<br><span style="font-size:20px;color:var(--text-faint);">Copy the code. Find a text editor. Create a file. Paste it in. Figure out how to open it in a browser.</span></div>
  </div>
</div>
```

**Step 3: Replace slide 6 with scenario part 2**

Replace the current slide 6 (limits 3-4):

```html
<!-- 6: SCENARIO 2 -->
<div class="slide">
  <div class="content stagger">
    <div class="chat-scene">
      <div class="chat-bubble user">
        <span class="chat-label">You</span>
        Now change the headline to something catchier.
      </div>
      <div class="chat-bubble ai">
        <span class="chat-label">ChatGPT</span>
        Here's the updated version with a new headline...
        <span style="display:block;margin-top:8px;font-family:monospace;font-size:16px;color:var(--text-faint);">&lt;!DOCTYPE html&gt;<br>&lt;html lang="en"&gt;<br>...the entire file again</span>
      </div>
    </div>
    <div class="chat-result">Which parts changed? You can't tell.<br><span style="font-size:20px;color:var(--text-faint);">Replace the whole file and hope nothing broke.</span></div>
  </div>
</div>
```

**Step 4: Replace slide 7 with scenario part 3**

Replace the current slide 7 ("brain in a jar"):

```html
<!-- 7: SCENARIO 3 -->
<div class="slide">
  <div class="content stagger">
    <div class="chat-scene">
      <div class="chat-bubble user">
        <span class="chat-label">You (a week later)</span>
        I want to add an About page to my website.
      </div>
      <div class="chat-bubble ai">
        <span class="chat-label">ChatGPT</span>
        I'd be happy to help! Could you share your current website code so I can match the style?
      </div>
      <div class="chat-bubble user">
        <span class="chat-label">You</span>
        <span style="color:rgba(255,255,255,0.5);">Um... let me go find it and paste it all in...</span>
      </div>
    </div>
    <div class="chat-result">New conversation. Zero memory.<br><span style="font-size:20px;color:var(--text-faint);">You're describing your own project from memory. Copy-pasting fragments. It gives you code that doesn't match.</span></div>
  </div>
</div>
```

**Step 5: Add slide 8 — four limits summary**

Insert a new slide after the scenario:

```html
<!-- 8: FOUR LIMITS SUMMARY -->
<div class="slide">
  <div class="content stagger">
    <div class="label">Sound Familiar?</div>
    <h2>Four <span class="hl">hard limits.</span></h2>
    <div style="margin-top: 24px;">
      <div class="limit-row">
        <div class="l-num">1</div>
        <div>
          <h3>Can't see your files</h3>
          <p>You were copy-pasting everything. It never saw your actual project.</p>
        </div>
      </div>
      <div class="limit-row">
        <div class="l-num">2</div>
        <div>
          <h3>Can't take action</h3>
          <p>You did all the manual work &mdash; finding files, pasting code, switching apps.</p>
        </div>
      </div>
      <div class="limit-row">
        <div class="l-num">3</div>
        <div>
          <h3>Forgets everything</h3>
          <p>Every new conversation started from zero. A week later? Gone.</p>
        </div>
      </div>
      <div class="limit-row">
        <div class="l-num">4</div>
        <div>
          <h3>Freestyles every answer</h3>
          <p>No process. No methodology. Just whatever it comes up with.</p>
        </div>
      </div>
    </div>
  </div>
</div>
```

**Step 6: Add slide 9 — brain in a jar**

```html
<!-- 9: STATEMENT -->
<div class="slide">
  <div class="content centered stagger">
    <p class="statement">Chat AI is a brain in a jar.<br>Smart &mdash; but <span class="hl">no hands, no eyes, no workspace.</span></p>
  </div>
</div>
```

**Step 7: Verify slides 4-9 in browser**

Check: chat bubbles render correctly, stagger works, scenario reads naturally, limits summary has the right visual weight.

**Step 8: Commit**

```bash
git add presentation.html
git commit -m "content: add ChatGPT failure scenario slides 4-9"
```

---

### Task 4: Restructure Context Window Slides (Slides 10-13)

**Files:**
- Modify: `presentation.html` — replace current slides 8-9

**Step 1: Add slide 10 — transition**

```html
<!-- 10: TRANSITION -->
<div class="slide">
  <div class="content centered stagger">
    <p class="statement">There's a deeper reason<br>this <span class="hl">happens.</span></p>
  </div>
</div>
```

**Step 2: Add slide 11 — whiteboard metaphor + bars**

```html
<!-- 11: CONTEXT WINDOW -->
<div class="slide">
  <div class="content stagger">
    <div class="label">The Core Constraint</div>
    <h2>The context window.</h2>
    <p>Every AI conversation is a <span class="hl" style="color:var(--accent);">whiteboard.</span> You write on it as you talk. But the whiteboard has a fixed size. When it fills up, the AI starts erasing the oldest stuff to make room.</p>
    <div class="ctx-bars">
      <div class="ctx-bar"><div class="fill" style="width:25%"></div><span class="bar-label">Quick question</span></div>
      <div class="ctx-bar"><div class="fill" style="width:55%"></div><span class="bar-label">Edit a page</span></div>
      <div class="ctx-bar overflow"><div class="fill" style="width:150%"></div><span class="bar-label" style="left:auto;right:16px;">Build a website &mdash; doesn't fit</span></div>
    </div>
  </div>
</div>
```

**Step 3: Add slide 12 — implication**

```html
<!-- 12: IMPLICATION -->
<div class="slide">
  <div class="content centered stagger">
    <p class="statement">You can't describe an entire project in one conversation.<br><br>Not because the AI isn't <span class="hl">smart</span> enough &mdash; because it can't <span class="hl">hold</span> it all at once.</p>
  </div>
</div>
```

**Step 4: Add slide 13 — break into pieces**

```html
<!-- 13: SOLUTION -->
<div class="slide">
  <div class="content centered stagger">
    <h2>The solution:</h2>
    <h2 style="margin-top:8px;"><span class="hl">Break it into pieces</span> that each fit.</h2>
    <div class="ctx-pieces" style="margin-top: 48px;">
      <div class="ctx-piece">Homepage</div>
      <div class="ctx-piece">Gallery</div>
      <div class="ctx-piece">About</div>
      <div class="ctx-piece">Deploy</div>
    </div>
    <p style="margin-top: 32px;">One conversation = one focused task. Not an entire project.</p>
  </div>
</div>
```

**Step 5: Verify slides 10-13**

Check: transition, whiteboard explanation reads naturally, bars animate, pieces show correctly.

**Step 6: Commit**

```bash
git add presentation.html
git commit -m "content: restructure context window slides with whiteboard metaphor"
```

---

### Task 5: Upgrade Section + Evolution (Slides 14-16)

**Files:**
- Modify: `presentation.html` — replace current slides 10-12

**Step 1: Add slide 14 — statement**

```html
<!-- 14: STATEMENT -->
<div class="slide">
  <div class="content centered stagger">
    <p class="statement">We don't need a smarter chatbot.<br>We need an AI that can actually <span class="hl">work.</span></p>
  </div>
</div>
```

**Step 2: Add slide 15 — what we need grid**

```html
<!-- 15: WHAT WE NEED -->
<div class="slide">
  <div class="content stagger">
    <div class="label">The Upgrade</div>
    <h2>What we actually need.</h2>
    <div class="need-grid">
      <div class="need-item">
        <h3>See your files</h3>
        <p>Read the project. Understand the structure. No copy-pasting.</p>
      </div>
      <div class="need-item">
        <h3>Edit directly</h3>
        <p>Make changes in place. Write code, update content, fix bugs.</p>
      </div>
      <div class="need-item">
        <h3>Run commands</h3>
        <p>Test, build, deploy. Not just talk about it &mdash; actually do it.</p>
      </div>
      <div class="need-item">
        <h3>Follow processes</h3>
        <p>Expert workflows, not freestyling. Consistent results.</p>
      </div>
    </div>
  </div>
</div>
```

**Step 3: Add slide 16 — evolution stack**

```html
<!-- 16: EVOLUTION -->
<div class="slide">
  <div class="content stagger">
    <div class="label">The Evolution</div>
    <h2>How we got here.</h2>
    <div class="evo-stack">
      <div class="evo-row">
        <div class="evo-stage">Chat / LLM</div>
        <div class="evo-desc">Knowledge, writing &mdash; but can only talk</div>
      </div>
      <div class="evo-row">
        <div class="evo-stage">Agent</div>
        <div class="evo-desc">Multi-step reasoning &mdash; but sandboxed</div>
      </div>
      <div class="evo-row">
        <div class="evo-stage">MCP &amp; Tools</div>
        <div class="evo-desc">Calls APIs, reads email &mdash; but cloud only</div>
      </div>
      <div class="evo-row">
        <div class="evo-stage">Claude Code</div>
        <div class="evo-desc">Read, write, run, test in your terminal</div>
      </div>
      <div class="evo-row">
        <div class="evo-stage">Spec-Driven</div>
        <div class="evo-desc">Structured specs replace freestyling</div>
      </div>
      <div class="evo-row current">
        <div class="evo-stage">GSD &rarr;</div>
        <div class="evo-desc">You become the conductor.</div>
      </div>
    </div>
  </div>
</div>
```

**Step 4: Verify slides 14-16, commit**

```bash
git add presentation.html
git commit -m "content: add upgrade and evolution slides 14-16"
```

---

### Task 6: Expanded Team Section (Slides 17-20)

**Files:**
- Modify: `presentation.html` — replace current slides 16-18

**Step 1: Add slide 17 — section header**

```html
<!-- 17: TEAMS HEADER -->
<div class="slide">
  <div class="content stagger">
    <div class="label">The Professional Way</div>
    <h2>How real products<br>get <span class="hl">built.</span></h2>
    <p style="margin-top:16px;">Every app on your phone. Every website you use. Every tool you rely on. They were all built by a team following a process.</p>
  </div>
</div>
```

**Step 2: Add slide 18 — full team grid (8 roles)**

```html
<!-- 18: THE TEAM -->
<div class="slide">
  <div class="content stagger">
    <div class="label">The Team</div>
    <h2>Meet the crew.</h2>
    <div class="team-grid">
      <div class="team-card role-biz">
        <h4>Founder / CEO</h4>
        <p>Has the vision. Sets the direction.</p>
      </div>
      <div class="team-card role-prod">
        <h4>Product Manager</h4>
        <p>Translates vision into requirements. Decides what to build.</p>
      </div>
      <div class="team-card role-prod">
        <h4>Designer</h4>
        <p>Makes it look good and work well. User flows + visual design.</p>
      </div>
      <div class="team-card role-eng">
        <h4>Architect</h4>
        <p>Plans the technical structure. How pieces connect.</p>
      </div>
      <div class="team-card role-eng">
        <h4>Developer</h4>
        <p>Writes the actual code. Implements the design.</p>
      </div>
      <div class="team-card role-qa">
        <h4>QA / Tester</h4>
        <p>Breaks things on purpose to find bugs before users do.</p>
      </div>
      <div class="team-card role-ops">
        <h4>DevOps</h4>
        <p>Gets it from "works on my computer" to live on the internet.</p>
      </div>
      <div class="team-card role-prod">
        <h4>Project Manager</h4>
        <p>Tracks what's done, what's next, what's blocked.</p>
      </div>
    </div>
  </div>
</div>
```

**Step 3: Add slide 19 — the process**

```html
<!-- 19: THE PROCESS -->
<div class="slide">
  <div class="content stagger">
    <div class="label">Their Process</div>
    <h2>What they do.</h2>
    <div style="margin-top: 32px;">
      <div class="team-step">
        <div class="ts-role biz">Business</div>
        <div class="ts-action">Defines the vision and goals</div>
      </div>
      <div class="team-step">
        <div class="ts-role prod">Product</div>
        <div class="ts-action">Researches and writes detailed requirements</div>
      </div>
      <div class="team-step">
        <div class="ts-role prod">Design</div>
        <div class="ts-action">Creates mockups and user flows</div>
      </div>
      <div class="team-step">
        <div class="ts-role eng">Architecture</div>
        <div class="ts-action">Plans the technical approach</div>
      </div>
      <div class="team-step">
        <div class="ts-role eng">Development</div>
        <div class="ts-action">Implements in focused sprints</div>
      </div>
      <div class="team-step">
        <div class="ts-role qa">QA</div>
        <div class="ts-action">Tests against acceptance criteria</div>
      </div>
      <div class="team-step">
        <div class="ts-role" style="color:#2dd4bf;">DevOps</div>
        <div class="ts-action">Deploys to production</div>
      </div>
    </div>
  </div>
</div>
```

**Step 4: Add slide 20 — the problem statement**

```html
<!-- 20: STATEMENT -->
<div class="slide">
  <div class="content centered stagger">
    <p class="statement">This process works. It's how every app on your phone was built.<br><br>The problem? It requires <span class="hl">an entire team</span> and months of coordination.</p>
  </div>
</div>
```

**Step 5: Verify slides 17-20, commit**

```bash
git add presentation.html
git commit -m "content: add expanded team roles and process slides 17-20"
```

---

### Task 7: GSD Bridge — The Climax (Slides 21-24)

**Files:**
- Modify: `presentation.html` — replace current slides 19-21

**Step 1: Add slide 21 — anticipation**

```html
<!-- 21: ANTICIPATION -->
<div class="slide">
  <div class="content centered stagger">
    <p class="statement">What if one framework could<br>replace this <span class="hl">entire team?</span></p>
  </div>
</div>
```

**Step 2: Add slide 22 — the mapping (staggered reveal)**

```html
<!-- 22: GSD MAPPING -->
<div class="slide">
  <div class="content stagger">
    <div class="label">The Breakthrough</div>
    <h2>GSD does <span class="hl">all of this.</span></h2>
    <div style="margin-top: 32px;">
      <div class="map-row">
        <div class="map-col-left">Founder sets vision</div>
        <div class="map-arrow">&rarr;</div>
        <div class="map-col-right">You describe your vision</div>
      </div>
      <div class="map-row">
        <div class="map-col-left">Product Manager writes reqs</div>
        <div class="map-arrow">&rarr;</div>
        <div class="map-col-right">/gsd:new-project</div>
      </div>
      <div class="map-row">
        <div class="map-col-left">Project Manager scopes work</div>
        <div class="map-arrow">&rarr;</div>
        <div class="map-col-right">Roadmap auto-generated</div>
      </div>
      <div class="map-row">
        <div class="map-col-left">Designer + Architect plans</div>
        <div class="map-arrow">&rarr;</div>
        <div class="map-col-right">/gsd:plan-phase</div>
      </div>
      <div class="map-row">
        <div class="map-col-left">Developer writes &amp; tests</div>
        <div class="map-arrow">&rarr;</div>
        <div class="map-col-right">/gsd:execute-phase</div>
      </div>
      <div class="map-row">
        <div class="map-col-left">QA verifies criteria</div>
        <div class="map-arrow">&rarr;</div>
        <div class="map-col-right">/gsd:verify-work</div>
      </div>
      <div class="map-row">
        <div class="map-col-left">DevOps deploys</div>
        <div class="map-arrow">&rarr;</div>
        <div class="map-col-right">git push &rarr; Vercel</div>
      </div>
    </div>
  </div>
</div>
```

**Step 3: Add slide 23 — impact statement**

```html
<!-- 23: STATEMENT -->
<div class="slide">
  <div class="content centered stagger">
    <p class="statement">From a team of <span class="hl">8 people</span><br>to <span class="hl">just you</span> and a framework.<br><br>Same process. Same rigor.</p>
  </div>
</div>
```

**Step 4: Add slide 24 — GSD hierarchy**

```html
<!-- 24: GSD HIERARCHY -->
<div class="slide">
  <div class="content centered stagger">
    <div class="label">The GSD Framework</div>
    <h2>Get Shit Done.</h2>
    <div class="hierarchy">
      <div class="h-node"><div class="h-label">Project</div><div class="h-desc">"My portfolio website"</div></div>
      <div class="h-connector"></div>
      <div class="h-node"><div class="h-label">Milestone</div><div class="h-desc">v1: The core site</div></div>
      <div class="h-connector"></div>
      <div class="h-node"><div class="h-label">Phases</div><div class="h-desc">Logical chunks of work</div></div>
      <div class="h-connector"></div>
      <div class="h-branch">
        <div class="h-node"><div class="h-label">Phase 1</div><div class="h-desc">Homepage</div></div>
        <div class="h-node"><div class="h-label">Phase 2</div><div class="h-desc">Gallery</div></div>
        <div class="h-node"><div class="h-label">Phase 3</div><div class="h-desc">Deploy</div></div>
      </div>
    </div>
    <div class="flow-row" style="margin-top: 40px;">
      <div class="flow-node">Plan</div>
      <div class="flow-arrow">&rarr;</div>
      <div class="flow-node">Build</div>
      <div class="flow-arrow">&rarr;</div>
      <div class="flow-node">Verify</div>
      <div class="flow-arrow">&rarr;</div>
      <div class="flow-node hl-node">Done</div>
    </div>
  </div>
</div>
```

**Step 5: Verify slides 21-24, commit**

```bash
git add presentation.html
git commit -m "content: add GSD mapping reveal and hierarchy slides 21-24"
```

---

### Task 8: The System — Commands, Tools, Flow (Slides 25-27)

**Files:**
- Modify: `presentation.html` — replace current slides 22-15

**Step 1: Add slide 25 — four commands**

```html
<!-- 25: COMMANDS -->
<div class="slide">
  <div class="content stagger">
    <div class="label">The Commands</div>
    <h2>Four commands. That's it.</h2>
    <div style="margin-top: 32px;">
      <div class="cmd-row">
        <div class="cmd-code">/gsd:new-project</div>
        <div class="cmd-desc">AI interviews you. Creates a project &amp; roadmap.</div>
      </div>
      <div class="cmd-row">
        <div class="cmd-code">/gsd:plan-phase</div>
        <div class="cmd-desc">Researches. Writes a detailed plan for your review.</div>
      </div>
      <div class="cmd-row">
        <div class="cmd-code">/gsd:execute-phase</div>
        <div class="cmd-desc">Writes code. Makes commits. Runs checks.</div>
      </div>
      <div class="cmd-row">
        <div class="cmd-code">/gsd:progress</div>
        <div class="cmd-desc">Where you are. Picks up where you left off.</div>
      </div>
    </div>
    <div class="sessions">
      <div class="s-card"><h5>Session 1</h5><p>Homepage</p></div>
      <div class="s-card"><h5>Session 2</h5><p>Projects page</p></div>
      <div class="s-card"><h5>Session 3</h5><p>Deployed</p></div>
    </div>
    <div class="s-persist">State persists between sessions</div>
  </div>
</div>
```

**Step 2: Add slide 26 — the tools (consolidated)**

```html
<!-- 26: TOOLS -->
<div class="slide">
  <div class="content stagger">
    <div class="label">The Tools</div>
    <h2>Your toolkit.</h2>
    <div class="tool-feature" style="margin-top:32px;">
      <div class="tool-icon">&#9000;</div>
      <div>
        <h3>Claude Code</h3>
        <p>AI in your terminal. Reads your files, edits your code, runs your commands. Your entire production crew.</p>
      </div>
    </div>
    <div class="tool-feature" style="margin-top:24px;">
      <div class="tool-icon">&#128187;</div>
      <div>
        <h3>GitHub</h3>
        <p>Every change saved with a label. Full history. You can always go back.</p>
      </div>
    </div>
    <div class="tool-feature" style="margin-top:24px;">
      <div class="tool-icon">&#9650;</div>
      <div>
        <h3>Vercel</h3>
        <p>Push to GitHub, site deploys automatically. Real URL, live in 30 seconds. Free.</p>
      </div>
    </div>
  </div>
</div>
```

**Step 3: Add slide 27 — flow**

```html
<!-- 27: FLOW -->
<div class="slide">
  <div class="content centered stagger">
    <div class="label">The Flow</div>
    <h2>How changes go live.</h2>
    <div class="flow-row">
      <div class="flow-node">You describe</div>
      <div class="flow-arrow">&rarr;</div>
      <div class="flow-node">Claude edits</div>
      <div class="flow-arrow">&rarr;</div>
      <div class="flow-node">Commit</div>
      <div class="flow-arrow">&rarr;</div>
      <div class="flow-node">Push</div>
      <div class="flow-arrow">&rarr;</div>
      <div class="flow-node hl-node">Live!</div>
    </div>
    <p style="margin-top: 32px;">From idea to the real internet. Minutes, not days.</p>
  </div>
</div>
```

**Step 4: Verify slides 25-27, commit**

```bash
git add presentation.html
git commit -m "content: add commands, tools, and flow slides 25-27"
```

---

### Task 9: Walkthrough + Closing (Slides 28-31)

**Files:**
- Modify: `presentation.html` — replace current slides 23-28

**Step 1: Add slide 28 — walkthrough timeline**

```html
<!-- 28: WALKTHROUGH -->
<div class="slide">
  <div class="content stagger">
    <div class="label">The Walkthrough</div>
    <h2>Empty folder &rarr; <span class="hl">live site.</span></h2>
    <div class="walk-steps">
      <div class="walk-step">
        <h4><span class="hl">/gsd:new-project</span></h4>
        <p>Claude asks: "What do visitors feel? Who's your audience?"</p>
      </div>
      <div class="walk-step">
        <h4>Roadmap auto-generated</h4>
        <p>Homepage &rarr; Gallery &rarr; About + Contact &rarr; Polish + Deploy</p>
      </div>
      <div class="walk-step">
        <h4>Plan &rarr; Build &rarr; Feedback &rarr; Refine</h4>
        <p>"The font feels too heavy." Claude adjusts in seconds.</p>
      </div>
      <div class="walk-step">
        <h4>Repeat for each phase</h4>
        <p>Same rhythm. New session? GSD picks up exactly where you left off.</p>
      </div>
      <div class="walk-step">
        <h4>Deploy &rarr; Live URL</h4>
        <p>Real website. Built from conversations. Zero code written by you.</p>
      </div>
    </div>
  </div>
</div>
```

**Step 2: Add slide 29 — universal pattern**

```html
<!-- 29: UNIVERSAL -->
<div class="slide">
  <div class="content centered stagger">
    <p class="statement">This isn't just a software trick.<br><br><span class="hl">Vision &rarr; Break Down &rarr; Plan &rarr; Execute &rarr; Verify.</span><br><br>Whether you're building a website, launching a business, or renovating your apartment.</p>
  </div>
</div>
```

**Step 3: Add slide 30 — what else + takeaways**

```html
<!-- 30: WHAT ELSE + TAKEAWAYS -->
<div class="slide">
  <div class="content stagger">
    <div class="label">What You'll Walk Away With</div>
    <h2>Today's output.</h2>
    <div style="margin-top: 32px;">
      <div class="output-item">
        <div class="o-marker"></div>
        <div><h4>A live personal website</h4><p>Deployed on Vercel. Your own URL.</p></div>
      </div>
      <div class="output-item">
        <div class="o-marker"></div>
        <div><h4>The spec-driven methodology</h4><p>For any project &mdash; digital or physical.</p></div>
      </div>
      <div class="output-item">
        <div class="o-marker"></div>
        <div><h4>A new mental model</h4><p>Orchestrating AI agents, not chatting with them.</p></div>
      </div>
      <div class="output-item">
        <div class="o-marker"></div>
        <div><h4>Hands-on experience</h4><p>Claude Code, GitHub, Vercel, GSD &mdash; used for real.</p></div>
      </div>
    </div>
  </div>
</div>
```

**Step 4: Add slide 31 — closing**

```html
<!-- 31: CLOSING -->
<div class="slide">
  <div class="content centered stagger">
    <h1>Ready to<br><span class="hl">build?</span></h1>
    <div class="flow-row" style="margin-top: 56px;">
      <div class="flow-node">Vision</div>
      <div class="flow-arrow">&rarr;</div>
      <div class="flow-node">Spec</div>
      <div class="flow-arrow">&rarr;</div>
      <div class="flow-node">Plan</div>
      <div class="flow-arrow">&rarr;</div>
      <div class="flow-node">Build</div>
      <div class="flow-arrow">&rarr;</div>
      <div class="flow-node">Verify</div>
      <div class="flow-arrow">&rarr;</div>
      <div class="flow-node hl-node">Ship</div>
    </div>
    <p style="margin-top: 48px; color: var(--text-faint); font-size: 20px;">Let's go.</p>
  </div>
</div>
```

**Step 5: Update the slide counter in the nav hint**

Change the JS `slideCount` reference — it auto-calculates from `slides.length`, so no JS change needed. Just update the static text:

```html
<div class="nav-hint">
  <span id="slideCount">1 / 31</span>
</div>
```

**Step 6: Verify all slides 28-31 and the full deck end-to-end**

Navigate through all 31 slides. Check:
- All slides render correctly
- Stagger animations fire on each slide
- Progress bar reaches 100% on last slide
- No broken layouts
- Chat bubbles look right
- Team grid is readable
- Mapping reveal has visual weight

**Step 7: Commit**

```bash
git add presentation.html
git commit -m "content: add walkthrough and closing slides 28-31, complete redesign"
```

---

### Task 10: Add Bo Case Study Slide (after Walkthrough)

**Files:**
- Modify: `presentation.html` — add one slide after the walkthrough (slide 28) and before the universal pattern

**Step 1: Add the case study slide**

Insert after the walkthrough slide:

```html
<!-- CASE STUDY: BO -->
<div class="slide">
  <div class="content stagger">
    <div class="label">Case Study</div>
    <h2>Meet <span class="hl">Bo.</span></h2>
    <div style="margin-top: 32px;">
      <!-- PLACEHOLDER: Fill in Bo's specific details -->
      <div class="walk-steps">
        <div class="walk-step">
          <h4>Week 1</h4>
          <p>[What Bo started with / first project]</p>
        </div>
        <div class="walk-step">
          <h4>Week 2-3</h4>
          <p>[What he built / key milestones]</p>
        </div>
        <div class="walk-step">
          <h4>Today</h4>
          <p>[Where he is now / what he's accomplished]</p>
        </div>
      </div>
    </div>
    <p style="margin-top: 24px; font-size: 24px; color: var(--accent); font-weight: 600;">No coding experience. Just these tools and this process.</p>
  </div>
</div>
```

**Step 2: Verify, commit**

```bash
git add presentation.html
git commit -m "content: add Bo case study slide (placeholder)"
```

---

### Task 11: Final Polish Pass

**Files:**
- Modify: `presentation.html`

**Step 1: Full visual review in browser**

Open the presentation and click through all 31 slides. Note any:
- Text that's too long for the slide
- Layouts that feel cramped
- Animations that need timing adjustments
- Stagger children that exceed 8 (the CSS limit)

**Step 2: Fix any issues found**

Address each issue with targeted edits.

**Step 3: Final commit**

```bash
git add presentation.html
git commit -m "polish: final visual pass on presentation redesign"
```

---

## Execution Notes

- **The entire implementation is in one file** (`presentation.html`). Each task replaces a contiguous block of slides.
- **The safest approach:** Work top-to-bottom through the file. Each task corresponds to a section of the slide deck in order.
- **The slide engine (JS) doesn't need changes** — it auto-detects `.slide` elements and handles navigation.
- **CSS additions go before the `@media` query** at the end of the `<style>` block.
- **Removed slides:** The "what else you can build" slide (current 26) and the comparison table (current 25) are cut. "What else" content is absorbed into the universal pattern statement.

**CORRECTION:** Looking at the design doc again, "What else you can build" is kept (slide 30 was going to have it, but the plan above merged it with takeaways). If we want a separate "What else" slide, we'd add it between slides 29 and 30, making 32 total. Decision: keep it merged with takeaways for tighter pacing.
