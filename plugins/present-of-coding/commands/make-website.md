---
name: make-website
description: "Build a personal website or landing page using The Present of Coding brand identity. Asks what you need, then generates a fully styled HTML page. Use when you want to create or redesign a personal site, portfolio, project page, or landing page."
allowed-tools: Read, Write, Edit, Glob, Grep, Bash, AskUserQuestion
---

# Build a Branded Website

You are helping build a website using The Present of Coding brand identity. Before writing any code, you MUST gather context by asking questions. Use the brand skill in `skills/present-of-coding-brand/SKILL.md` for all visual and voice guidance.

## Step 1: Understand what they need

Ask the user these questions (use AskUserQuestion):

1. **What kind of site is this?**
   - Personal portfolio site (like abigailhaddad.netlify.app)
   - Project landing page (for a specific tool or repo)
   - Data site / dashboard (for presenting data or analysis)
   - Something else (describe it)

2. **What sections do you need?** For a portfolio site, the default is: intro/hero, projects, writing, talks, experience, contact. For other sites, describe what you want.

3. **Do you have content ready?** Projects, descriptions, links, etc. — or should I use placeholder content that matches the brand voice?

4. **Any specific requirements?** Dark mode support, responsive/mobile, specific deployment target (Netlify, GitHub Pages, etc.)?

## Step 2: Plan the structure

Based on the answers, present a brief plan:
- Which sections, in what order
- Whether it's single-page scrolling or multi-page
- Key components needed (project cards, timeline, nav, etc.)

Ask the user to confirm before building.

## Step 3: Build the site

Generate a complete, working HTML file (or set of files) following the brand skill:

### Visual identity (from the skill):
- Use the CSS variables block from the skill as the foundation
- Warm White (#FFF8F0) backgrounds, never pure white
- Forest Green (#2D6A4F) for links and interactive elements
- DM Sans for headings, Source Sans 3 for body, JetBrains Mono for code
- Import all three fonts from Google Fonts
- Cards with 1px #E8DDD0 borders, 0.5rem radius, amber hover
- Max 720px for text content, 1100px for card layouts
- 4rem section padding, minimal shadows

### Layout rules (from the skill):
- Hero is left-aligned, not centered. No full-viewport splash.
- Project cards in 2-column grid on desktop, 1 on mobile
- Breakpoint at 768px
- No hero gradients, no parallax, no stock photos
- Body text left-aligned. Only headings can be centered.

### Voice (for any copy):
- First person, specific, honest
- "I build X" not "Passionate about X"
- Lead with what you did and built, not abstract descriptions
- Include one beat of "why this was harder than it sounds" in project descriptions

### Anti-patterns to avoid:
- No pure white or pure black
- No blue/indigo corporate palette
- No stock photography
- No "passionate about technology" hero copy
- No tech stack shield badges
- No testimonial carousels
- No giant hero text with gradient backgrounds

Generate clean, semantic HTML with embedded CSS (using the brand CSS variables). Make it fully responsive. Include dark mode if requested.

## Step 4: Review

After generating, check:
- Does it feel like a personal project or a corporate landing page? (Should be personal.)
- Would you read this hero copy out loud? (If it sounds like LinkedIn, rewrite.)
- Are interactive elements clearly hoverable?
- Does the mobile layout work?

Save the file(s) and tell the user how to preview locally.
