---
name: write-blog-post
description: "Draft a blog post for The Present of Coding Substack. Walks through topic, structure, and voice before writing. Use when you want to write a new blog post, draft a Substack article, or outline a piece of writing."
allowed-tools: Read, Write, Edit, Glob, Grep, AskUserQuestion
---

# Write a Blog Post for The Present of Coding

You are helping draft a blog post for The Present of Coding, Abigail Haddad's Substack. Before writing anything, you MUST gather context by asking questions. Use the brand skill in `skills/present-of-coding-brand/SKILL.md` for all voice, tone, and structural guidance.

## Step 1: Find the heart of the post

Ask the user these questions (use AskUserQuestion). The first two are the most important — get these right and everything else follows:

1. **What's the heart of this post?** Not the topic — the *point*. The reason you're writing this, the core thing you want a reader to walk away with. "I built an eval pipeline" is a topic. "Most people skip evaluation because it feels impossible to measure, but you can get surprisingly far with simple heuristics" is a heart. Push the user to articulate this clearly — it becomes the organizing principle for everything else.

2. **What are the stories that support this?** What are the 2-4 specific moments, examples, or experiences that make this point land? These are the concrete beats the post is built around. Not abstractions — actual things that happened. "The time I ran my pipeline on real data and 40% of the outputs were wrong" is a story. "Evaluation is important" is not.

3. **Which post pattern fits best?**
   - "Here's what I built" — Walk through a project you made. Most common pattern.
   - "Here's how to do X" — Tutorial or guide. Uses the Problem → How it works → My implementation → When to use it structure.
   - "Here's how to think about X" — Career advice, opinion, or reflection. Starts with a personal story.

4. **What went wrong or surprised you?** This is non-negotiable for the brand. Every post needs at least one honest moment about difficulty, failure, or unexpected lessons. (This may already be covered by the stories above — if so, note which story serves this role.)

5. **Who's the audience?** Are you writing for people who already know the domain, or explaining from scratch?

## Step 2: Draft an outline

Based on the answers, draft an outline following the structural pattern from the skill:

- For "what I built": Opening hook → The thing itself (with subheadings per component) → What went wrong → Takeaway
- For "how to do X": Framing → Sections with Problem/How/Implementation/When → Honest scoping
- For "how to think about X": Personal story → Specific practical advice → Acknowledgment of limits

Present the outline to the user and ask if they want to adjust anything before you draft.

## Step 3: Write the draft

Write the full post following these rules from the brand skill:

- First person, active voice
- Stories over abstractions — lead with concrete examples
- Dry humor embedded in narrative, not forced jokes
- Practical and opinionated — state what you think and why
- Subheadings should be conversational and specific, not generic
- Include footnotes for tangents and jokes
- Target 1,500-3,000 words (tutorials can go longer)
- Use `##` for major sections, `###` sparingly

**Voice check:** Read every sentence and ask "Would Abigail actually say this out loud?" If it sounds like LinkedIn or a press release, rewrite it.

## Step 4: Self-review

After drafting, check against these brand anti-patterns:
- No "passionate about" or "excited to share"
- No "leverage," "cutting-edge," "synergy"
- No thesis-statement openings — start with a concrete situation
- No generic subheadings ("Background," "Discussion," "Conclusion")
- At least one section on what went wrong
- The subheading scan test: can someone read just the subheadings and get the gist?

Write the post as a markdown file. Ask the user where they want it saved.
