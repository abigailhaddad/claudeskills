---
name: make-slides
description: "Build a presentation using Slidev with The Present of Coding brand identity. Asks about your talk, then generates branded slides. Use when you want to create a slide deck, presentation, or talk."
allowed-tools: Read, Write, Edit, Glob, Grep, Bash, AskUserQuestion
---

# Build a Slide Deck with Slidev

You are helping build a presentation using Slidev. Before writing slides, gather context. Use the brand skill in `skills/present-of-coding-brand/SKILL.md` for voice and visual guidance.

## Tech stack

This is the stack — not Marp, not Google Slides, not PowerPoint:

- **Slidev** (`@slidev/cli`). Vue-powered, markdown-based, ships as a dev server and exports to PDF.
- **Tailwind / UnoCSS utility classes** for all layout (grid, flexbox, spacing, text sizing). No custom CSS unless absolutely necessary.
- **Shiki** for code syntax highlighting.
- **PDF export** configured in frontmatter.

## Step 1: Understand the talk

Ask the user these questions (use AskUserQuestion):

1. **What's the talk about?** Not the title — the core argument. What should the audience walk away thinking or knowing?

2. **Who's the audience?** Technical level, what they already know, what they're hoping to learn.

3. **How long is the talk?** This determines slide count. Roughly 1 minute per slide, so a 30-minute talk is ~30-40 slides (many are just an image + heading).

4. **Do you have content already?** A blog post to adapt, an outline, raw notes, or starting from scratch?

5. **Do you have images/illustrations?** The talks lean heavily on custom illustrations and screenshots. If you have them, point me at the directory. If not, we'll use placeholder references and you can add them later.

## Step 2: Plan the structure

Based on the answers, draft a slide-by-slide outline. The structure follows a pattern established in past talks:

### Talk structure pattern

1. **Title slide.** Name, talk title, subtitle. Clean.
2. **Attention-grabber.** Right after the title — something punchy that reframes expectations or makes the audience laugh. One big statement, centered. (Example from past talk: "THIS IS NOT ABOUT RAG" in huge text with warning emoji.)
3. **Context / the problem (3-5 slides).** Set up what you were dealing with and why it matters. Use images, grids of examples, or short bullet lists. This is where you show the audience "you have this problem too."
4. **Agenda slide.** List the parts of the talk. Keep it simple — emoji + section name per line.
5. **Content sections.** Each section gets:
   - A **section divider** slide (`layout: section`) with just the section title
   - **3-8 content slides** per section
   - At least one image-heavy slide per section (screenshot, illustration, diagram)
6. **Results / payoff.** Show the numbers. Use big bold text in a grid layout.
7. **Closing slide.** Links to website, GitHub, Substack, the presentation repo. No "Questions?" slide — just stop.

Present the outline and ask the user to confirm before writing slides.

## Step 3: Write the slides

Generate a Slidev markdown file (`slides.md`) with proper frontmatter and slide content.

### Frontmatter template:

```yaml
---
theme: default
highlighter: shiki
lineNumbers: false
drawings:
  persist: false
transition: slide-left
title: "Your Talk Title"
mdc: true
download: true
exportFilename: your-talk-filename
export:
  format: pdf
  timeout: 30000
  withClicks: false
---
```

### Brand theme CSS

Create a `style.css` file in the project root that Slidev will pick up, or include via `<style>` at the end of `slides.md`. This applies the brand identity from the skill to all slides:

```css
@import url('https://fonts.googleapis.com/css2?family=DM+Sans:wght@400;500;600;700&family=Source+Sans+3:wght@400;500;600&family=JetBrains+Mono:wght@400;500&display=swap');

:root {
  --slidev-theme-primary: #2D6A4F;
  --slidev-theme-background: #FFF8F0;
}

/* Base slide styling */
.slidev-layout {
  font-family: 'Source Sans 3', sans-serif;
  background: #FFF8F0;
  color: #3D2B1F;
}

/* Headings */
h1, h2, h3, h4 {
  font-family: 'DM Sans', sans-serif;
  color: #3D2B1F;
  letter-spacing: -0.01em;
}

/* Links */
a {
  color: #2D6A4F;
}

/* Code blocks */
.slidev-code {
  font-family: 'JetBrains Mono', monospace;
}
pre {
  background: #2A211A !important;
  border-radius: 0.5rem;
}

/* Section divider slides — forest green background */
.slidev-layout.section {
  background: #2D6A4F;
  color: #FFF8F0;
}
.slidev-layout.section h1 {
  color: #FFF8F0;
}

/* Borders and cards use brand tan */
.border, .border-2 {
  border-color: #E8DDD0;
}
.rounded-lg {
  border-radius: 0.5rem;
}

/* Muted text */
.text-gray-500, .text-gray-600 {
  color: #7A6E62;
}
```

The key points:
- **Backgrounds:** Warm white (#FFF8F0), not Slidev's default white. Section dividers in forest green (#2D6A4F).
- **Fonts:** DM Sans for headings, Source Sans 3 for body, JetBrains Mono for code. Imported from Google Fonts.
- **Text:** Dark brown (#3D2B1F), not black. Muted text in warm gray (#7A6E62), not cold gray.
- **Links/accents:** Forest green (#2D6A4F).
- **Code blocks:** Warm dark brown (#2A211A) background, not blue-black.
- **Borders:** Light tan (#E8DDD0), not gray.

### Slide design rules

These come from studying actual talks, not theory:

**Text per slide:**
- Most slides are a heading + an image. That's it.
- Bullet slides have 3-5 items max, each one line.
- If a slide has more than ~40 words of text (not counting code), split it.
- One idea per slide. Second idea = second slide.

**Layouts to use:**
- `layout: default` — heading + content. The workhorse.
- `layout: center` — single centered element. For images, big statements, or punchlines.
- `layout: section` — section divider. Just a title, acts as a visual break.
- `layout: two-cols` — left/right split with `::right::` separator. Good for text left / image right, or comparison.

**Grid layouts with Tailwind:**
Use Tailwind grids when presenting categories, results, or options:

```html
<!-- 3-column grid for categories or results -->
<div class="grid grid-cols-3 gap-8 mt-12">
  <div class="text-center p-6">
    <div class="text-7xl mb-4">🏥</div>
    <p class="text-2xl font-semibold">Category Name</p>
  </div>
  <!-- ... -->
</div>
```

```html
<!-- Big number results -->
<div class="grid grid-cols-3 gap-8 mt-12 text-center">
  <div class="border-2 rounded-lg p-6">
    <div class="text-6xl font-bold">33,647</div>
    <div class="text-2xl">Label</div>
    <div class="text-gray-500">(94%)</div>
  </div>
  <!-- ... -->
</div>
```

**Images:**
- Images are central to the talks. Many slides are just `# Heading` + `<img>`.
- Use inline styles or Tailwind classes for sizing: `class="w-90 h-90"` or `style="width: 70%; height: auto;"`.
- Center images with `<div class="flex flex-col items-center justify-center">`.
- Reference images from `/images/` directory (served from `public/images/` in Slidev).
- If images don't exist yet, use descriptive placeholder filenames and note what each image should show.

**Emoji:**
- Used as visual hierarchy, not decoration. A big emoji (text-7xl) acts as an icon for a category.
- Fine on agenda slides, category grids, and scaling-up/lesson slides.
- Don't sprinkle emoji into body text randomly.

**Code snippets:**
- Keep them short — 3-5 lines max on a slide. The audience can't read more than that.
- Use the code for the punchline, not the full implementation.
- Slidev handles syntax highlighting via Shiki automatically with fenced code blocks.

**Voice in slides:**
- First person, casual. "I built" / "I tried" / "I learned."
- Direct address to audience when relevant: "Your documents," "Your constraints."
- Humor embedded naturally — the format carries the joke (e.g., building a gibberish detector, then debugging the gibberish detector, then just using Gemini for $0.07).

**Numbers and results:**
- Present big and bold. `text-6xl font-bold` for the number, smaller text below for the label.
- Use a grid layout for multiple metrics side by side.
- Include the percentage in parentheses in muted text below.

### Slide separators

Use `---` between slides. Add layout/class directives between the separators:

```markdown
---
layout: section
---

# Part 2: The Larger Problem

---
layout: two-cols
---

# Left Side Heading

Content here

::right::

<div class="flex items-center justify-center h-full">
  <img src="/images/thing.png" class="max-w-sm" />
</div>
```

### Package.json

Also generate a `package.json`:

```json
{
  "name": "your-talk-name",
  "version": "1.0.0",
  "private": true,
  "scripts": {
    "dev": "slidev --open",
    "build": "slidev build",
    "export": "slidev export"
  },
  "dependencies": {
    "@slidev/cli": "^0.49.0",
    "@slidev/theme-default": "^0.25.0"
  },
  "devDependencies": {
    "playwright-chromium": "^1.55.0"
  }
}
```

### Image directory

Create a `public/images/` directory. If the user has images, reference them. If not, create a `public/images/README.md` listing what images are needed with descriptions of what each should show, so they can be created or sourced later.

## Step 4: Review

After generating, check:

**Content:**
- Is any slide over ~40 words? Cut it.
- Are most slides heading + image or heading + short list? (They should be.)
- Is there an attention-grabber right after the title?
- Is there a "Questions?" slide? Remove it.
- Does the closing slide have links to website, GitHub, Substack?
- Are code snippets 3-5 lines max?
- Would the images/code be readable from the back of a room?

**Brand:**
- Is the brand CSS included (style.css or `<style>` block)?
- Are slide backgrounds warm white (#FFF8F0), not pure white?
- Are section dividers forest green (#2D6A4F)?
- Are headings in DM Sans, body in Source Sans 3?
- Is text dark brown (#3D2B1F), not black?
- Are code blocks warm dark (#2A211A), not cold blue-black?

**Runs:**
- Can you run `npm install && npm run dev` and see the slides?

Tell the user how to preview (`npm run dev`) and export to PDF (`npm run export`).
