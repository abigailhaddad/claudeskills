---
name: make-data-site
description: "Build a data site or dashboard from an existing pipeline using The Present of Coding brand identity. Reads your data code first, then builds a frontend with D3 charts and DataTables. Use when you have a data pipeline and want to create a web viewer, dashboard, or tracker."
allowed-tools: Read, Write, Edit, Glob, Grep, Bash, AskUserQuestion
---

# Build a Branded Data Site

You are helping build a web frontend for an existing data pipeline. There is ALWAYS code already — your job is to understand it first, then build a site that presents the data well. Use the brand skill in `skills/present-of-coding-brand/SKILL.md` for all visual guidance.

## Tech stack

These are not suggestions — this is the stack:

- **DataTables** for all tabular data. Use DataTables' built-in functionality as much as possible — column filtering, sorting, search, pagination, CSV export. Don't build custom filter dropdowns when DataTables already does it. Column-specific search inputs, header click sorting, the search box — lean on all of it.
- **D3** for charts and visualizations. Not Chart.js, not Plotly, not canvas-based libraries.
- **Vanilla HTML/CSS/JS.** No React, no build step, no bundler. The site should be a static HTML file (or small set of files) that loads data from JSON/CSV and renders client-side.
- **Shareable filter URLs.** Filter state goes in query parameters. When someone applies filters, the URL updates. When someone loads a URL with query params, the filters apply on load. This includes DataTables filter state.
- **Don't repeat code.** If multiple pages share the brand CSS, table styles, or utility functions, extract them into shared files. Don't copy-paste the same 200 lines of CSS into every HTML file.

## Step 1: Understand the existing code

Ask the user to point you at their code. Then READ IT before asking anything else.

Ask (use AskUserQuestion):

1. **Where's your code?** Point me at the repo, directory, or key files. I need to read the code before we talk about the site.

Then go read it. You're looking for:

### What to look for in the code

- **Output data shape:** What does the final output look like? CSV columns, JSON structure, dataframe shape. What are the actual field names and types? This determines your DataTables columns and D3 data bindings.
- **Key metrics and aggregations:** Is the code computing counts, percentages, averages, year-over-year changes? These become KPIs at the top and D3 chart data. Note exactly how they're calculated so the frontend matches.
- **Filters and dimensions:** What are the categorical fields? These become DataTables column filters. Figure out which fields have a small number of unique values (good for dropdown filters) vs. many (better as free text search).
- **Time dimensions:** Is there a date/time field? What granularity — daily, monthly, yearly? Is there a comparison period? This determines D3 chart x-axes and any time-based filtering.
- **Data volume:** How many rows? If under ~10K rows, everything can load client-side into DataTables at once. If larger, you may need server-side processing or pre-aggregated summary files for charts with the full data in a downloadable CSV.
- **Data source and update frequency:** Where does the raw data come from? Is this a one-time snapshot or a pipeline that runs on a schedule? Affects "last updated" display and data source attribution.
- **Existing output files:** Does the code already produce output files (CSV, JSON) that the site can consume directly? Or do you need to add a data export step to the pipeline?
- **Edge cases and caveats:** Data quality notes in comments, deduplication logic, fields that changed meaning over time, missing data periods. These become caveats displayed near the relevant chart or table on the site.

After reading the code, summarize what you found back to the user: "Here's what I see — X rows, these fields, these seem like the main metrics, these seem like natural DataTables column filters, this field would make a good D3 chart axis." Let them correct you.

## Step 2: Ask about the site

Now that you understand the code, ask:

1. **What's the main question this site answers?** "How many federal jobs were posted this month?" or "Which departments are hiring the most?" — what does someone come here to find out?

2. **What views do you need?** Based on what you saw in the code, propose specific options:
   - D3 charts — suggest specific chart types based on the data shape (e.g., "bar chart of listings by department" or "line chart of monthly counts over time", not just "charts")
   - DataTables table — suggest which columns to show by default, which to hide, which should have dropdown filters vs. text search
   - Summary KPIs at the top (total count, date range, key comparison numbers)

3. **Any reference sites?** Existing data sites in the portfolio (USAJobs tracker, FedScope dashboard) or other sites that are close to what you want?

## Step 3: Plan the layout

Based on the code and the answers, present a plan covering:
- What output data file(s) the site will consume (and whether the pipeline needs a new export step)
- File structure — which files, what's shared vs. page-specific
- Header: title, one-line description, links to GitHub/data source/methodology
- KPI bar: what summary numbers go at the top
- D3 charts: what charts, what data drives each one, how they connect to the DataTables filters
- DataTables config: which columns, which column filters (dropdown vs. text), default sort, CSV export button
- How filter state syncs to URL query params (both DataTables filters and any chart filters)
- Footer: data source attribution, GitHub link, "Built by Abigail Haddad" link
- Data caveats that should be displayed near relevant charts/tables

## Step 4: Build the site

### File structure:
```
site/
├── index.html              # Main page
├── css/
│   └── brand.css           # Shared brand CSS variables and base styles
├── js/
│   ├── filters.js          # Shareable URL filter state management
│   └── formatting.js       # Number formatting utilities
└── data/
    └── (output files from the pipeline)
```

Don't put everything in one giant HTML file. Extract shared styles and utilities.

### DataTables setup:
- Use DataTables' built-in column search for filtering — add search inputs in the footer or header of filterable columns
- For columns with a small set of unique values, use `<select>` dropdowns populated from the data itself
- For columns with many values, use text input search
- Enable CSV export via the Buttons extension
- Style with the brand palette — override DataTables' default styles to match warm white/cream/tan borders
- Sync DataTables filter state to URL query params on every filter change
- On page load, read query params and apply them to DataTables filters

### D3 setup:
- Set font-family to Source Sans 3 on all text elements
- Axis lines and gridlines in #E8DDD0, not default black
- Primary data color: #2D6A4F (Forest Green), secondary: #D4A03C (Amber)
- Tooltips: #2A211A background, #F5EDE0 text, 0.375rem border-radius, no delay
- Responsive: use viewBox and preserveAspectRatio, redraw on window resize
- If D3 charts should filter when DataTables filters change (or vice versa), wire them together

### Visual identity (from the brand skill):
- Use the CSS variables block from the skill as the foundation in `brand.css`
- Warm White (#FFF8F0) backgrounds, never pure white or pure black
- Forest Green (#2D6A4F) for interactive elements
- DM Sans for headings, Source Sans 3 for body and chart text, JetBrains Mono for code
- Cards with 1px #E8DDD0 borders, 0.5rem radius
- DataTables alternating rows: #FFF8F0 and #F5EDE0

### Data presentation rules (from the skill):
- **Numbers:** Round aggressively. 42,847 not 42,847.00. 3.2M not 3,200,000. Percentages zero decimals unless distinction matters.
- **Axes:** Abbreviate (10K, 20K). Don't label every gridline. Skip axis titles when the unit is obvious from context.
- **Tables:** Right-align numbers, left-align text. Sort by most important metric descending by default.
- **Charts:** No chartjunk, no 3D, no gradient fills. Annotate outliers directly.
- **Empty states:** "No data matches these filters" — clear message, not an empty chart with bare axes.
- **Loading:** "Loading..." text, not a spinner.
- **Caveats:** Near the data, not on a separate page.

### Header pattern:
```html
<header>
    <h1>Site Title</h1>
    <p class="site-description">What this data shows and the date range.</p>
    <p class="site-links">
        <a href="...">GitHub</a> · <a href="...">Data source</a>
    </p>
</header>
```

### Footer pattern:
```html
<footer>
    <p>Data source: <a href="...">Source</a> · Code: <a href="...">GitHub</a> · Built by <a href="https://abigailhaddad.netlify.app">Abigail Haddad</a></p>
</footer>
```

## Step 5: Review

After generating, check:
- Does the site load data from the pipeline's actual output files?
- Do the metrics match how the code calculates them?
- Are DataTables column filters working and synced to URL params?
- Can someone share a filtered view by copying the URL?
- Does the CSV export work?
- Are D3 charts using Source Sans 3, not browser defaults?
- Are axis lines #E8DDD0, not black?
- Is shared code actually shared, not copy-pasted across files?
- Does it look like it belongs in the same family as the other data sites?
- Are data caveats displayed near the relevant data?
- Does the footer link back to the personal site?
