# Present of Coding — Claude Code Plugin

Brand identity, writing voice, and starter commands for [The Present of Coding](https://presentofcoding.substack.com/) (Abigail Haddad's personal brand).

## What's in here

**Skill:** Complete brand identity — voice, colors, typography, layout rules, illustration style, and content-type-specific guidelines for websites, data sites, blog posts, and presentations.

**Commands:**

| Command | What it does |
|---------|-------------|
| `/write-blog-post` | Asks for the heart of your post and supporting stories, then drafts a Substack piece |
| `/make-website` | Asks what you need, then generates a fully styled HTML page |
| `/make-data-site` | Reads your existing pipeline code, then builds a frontend with DataTables and D3 |
| `/make-slides` | Asks about your talk, then generates a Slidev presentation with brand theming |

Each command asks questions first before generating anything, so you get something tailored rather than generic.

## Installation

Add this plugin to your Claude Code setup:

```bash
claude plugin add https://github.com/abigailhaddad/claudeskills
```

Or clone it and point Claude Code at the directory:

```bash
git clone https://github.com/abigailhaddad/claudeskills.git
claude --plugin-dir ./claudeskills
```

## Structure

```
claudeskills/
├── .claude-plugin/
│   └── plugin.json              # Plugin manifest
├── skills/
│   └── present-of-coding-brand/
│       └── SKILL.md             # Full brand identity skill
├── commands/
│   ├── write-blog-post.md       # /write-blog-post
│   ├── make-website.md          # /make-website
│   ├── make-data-site.md        # /make-data-site
│   └── make-slides.md           # /make-slides
└── README.md
```
