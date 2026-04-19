# AGENTS.md

## Project Purpose

This project is the web home for **Finding Critical Path**.

The site exists to:
- provide a durable archive for published editions
- present the publication as a credible nuclear industry resource
- create an independent home for this work outside any single employer or platform
- support future expansion without losing clarity or quality

This site is **not** a personal website, resume site, generic blog, corporate marketing page, or general news aggregator.

Finding Critical Path should feel like a **real publication** focused on making sense of the signals shaping the nuclear industry.

## Core Publication Identity

**Title:** Finding Critical Path  
**Tagline:** From emerging signals to direction.

The publication should clearly communicate early that it helps readers make sense of the nuclear industry, then let the content carry that identity without repetitive explanation.

This is better framed as a **publication of weekly editions** than as a “newsletter,” even if distribution currently happens through LinkedIn’s newsletter feature.

## Audience

The primary audience is **nuclear professionals**.

The site should feel like a valuable industry resource for readers who want insight, interpretation, and direction from current nuclear industry developments.

The tone should assume an informed audience. Do not make the site feel beginner-oriented, overly simplified, or general-interest in tone.

## Design Direction

The site should feel:

- sophisticated
- clean
- polished
- credible
- expert

The reading experience should feel:

- editorial
- refined
- professional but approachable
- thoughtful
- calm for longform reading

The site should **not** feel like:

- a personal blog
- a resume site
- a company marketing page
- a generic article template
- a flashy startup landing page
- a beginner explainer site
- a rough homegrown side project
- a cluttered feature-heavy website

Avoid:
- obvious template feel
- unnecessary clutter
- features for their own sake
- visual gimmicks
- empty pages
- unfinished public sections
- anything that weakens trust or polish

## Visual Principles

Use a **cool light** overall visual foundation.

The site should rely mostly on:
- clean neutrals
- strong contrast
- restrained accent color use
- disciplined spacing
- editorial typography

Typography direction:
- use **sans-serif** for navigation, metadata, interface, archive support text, and general site framing
- use **serif** for longform edition body text
- keep typography editorial and refined, not trendy or overly technical

Spacing should be balanced, leaning slightly more spacious than tight.

Motion and interactivity should be subtle:
- clear hover/focus states
- gentle transitions only
- no distracting animation

## Content and Page Structure

### Launch Structure

Version 1 should support:
- Home
- Archive
- About

Do not add public pages, links, or navigation items for anything that is not ready to be public.

Do not create “coming soon” pages or empty public sections.

### Home

The homepage should act as a light-framed landing experience centered on the **latest edition**.

It should include:
- site title and logo
- tagline near the top
- one sentence of reader-focused framing/value
- preview of the latest edition
- clear path to continue reading
- subtle path to the archive

The homepage should **not** dump the full latest edition inline by default.

The latest edition preview should include:
- hero image
- title
- date range
- excerpt
- keep reading link

When structured opening content is present in an edition markdown file, the homepage latest-edition preview should use the markdown's:
- Hook
- Hook Text
- Tech Framing

Use that wording directly.
Do not paraphrase, compress, or auto-summarize the preview text when those structured sections are available.

Treat the tagline as part of the page framing, not as repeated article metadata.

### Archive

The archive should use a **responsive tile layout**.

Default behavior:
- desktop: 3 across
- medium screens: 2 across
- mobile: 1 across

The initial archive view should show **6 editions**, with a **Load more** interaction after that.

Archive tiles should include:
- thumbnail image derived from the main edition graphic
- title
- full date range
- short summary
- estimated reading time shown quietly on the image, ideally in the lower-right corner

When structured opening content is present in an edition markdown file, archive preview text should also be sourced from the article opening rather than newly written or generated summary copy. Preserve original wording from the markdown and prefer the opening structure as the source of truth for archive-facing preview text.

Archive search should:
- live on the archive page
- filter results on the same page
- search edition summary and full edition text for version 1

Search does not need to appear in the global navigation.

## Edition Chronology and Ordering Rules

Edition order must always follow **publication chronology**, not the order in which files were added, edited, migrated, or integrated into the site.

Use the edition content files and their metadata as the source of truth for ordering, especially:
- week
- week_id
- date
- slug

Do not infer “latest” from:
- file creation date
- file modified date
- the most recently integrated edition
- the most recently touched HTML page
- the most recently added asset

### Homepage Ordering

The homepage featured edition must always be the **most recent published edition by chronology**.

If an older edition is added to the archive later, do **not** promote it to the homepage unless it is actually the newest published edition.

The homepage `Past Editions` section must:
- exclude the currently featured latest edition
- show only prior published editions
- remain in reverse chronological order

### Archive Ordering

Archive pages must list published editions in **reverse chronological order**.

When an older archived edition is added later, insert it into the correct chronological position rather than placing it at the top because it is new to the site.

### Edition Navigation Ordering

Previous / Next edition links must follow **edition chronology among published editions only**.

Do not base previous/next links on:
- page creation order
- integration order
- folder creation order
- manual guesswork from recently edited files

### Migration and Backfill Rule

When backfilling older editions into the archive, treat the task as an archival integration only.

Backfilled editions should:
- be published into the correct chronological position
- appear in archive listings in the correct order
- update previous/next links as needed
- not displace the current homepage featured edition unless they are truly the newest edition by chronology

### About

The About page should include:
1. Why it exists
2. Methodology
3. Author bio

The tone should be thoughtful, restrained, and warm.

The methodology should be light-touch to moderate:
- enough to build trust
- enough to explain the broad process
- not a technical deep dive
- not a central focus of the site

The author should remain secondary to the publication.
Use:
- a small byline on editions
- that byline links to the bio section on About
- bio includes LinkedIn link

Do not let the site drift into a personality-first presentation.

## Edition Structure

The recurring published unit is an **edition**.

Use:
- **title**
- **full date range**

Do not rely on issue numbers as the primary display identifier.

Example date style:
- March 23–29, 2026

### Edition Header

On desktop, use an editorial split layout:
- text/meta on the left
- hero image on the right

On mobile, stack naturally and preserve readability.

Edition header order:
1. Title
2. Date range
3. Byline
4. Hero image alongside on desktop

Do not force a subtitle/deck into the edition format.
Support one later if needed, but do not require it.

### Article Body

The article body should:
- begin below the header block
- use a medium reading width
- maintain generous side margins
- support calm longform reading
- avoid interruption-heavy layout patterns

When structured opening content is present in an edition markdown file, the edition body should preserve that opening in order:
- Hook
- Hook Text
- Tech Framing

Do not omit the `Tech Framing` line from the published edition when it exists in the markdown.

Keep the article body visually continuous.
Do not restyle individual lines as pull quotes, breakout quotes, or other emphasized quote blocks inside standard editions unless explicitly asked.

When structured closing content is present in an edition markdown file, preserve the markdown wording directly for the closing sequence as well, including:
- Structural Close
- Forward Looking Question

Do not condense, paraphrase, or rewrite those closing sections in the published edition.

Do not break the longform reading experience with overly visible utility features.

## References and Source Handling

Keep the current **Dive deeper** format.

Within the article body:
- use numbered reference markers like `[1]`
- make them clearly visible but small
- treat them as editorial credibility markers
- do not make them visually intrusive
- do not require jump-to-footnote behavior unless clearly useful later

At the end of the edition:
- include a Dive deeper section
- preserve numbered references
- include title, short explanatory summary, and source link
- keep the section calm, polished, and editorial in tone

Do not overload the article body with inline source links that disrupt reading flow.

## Navigation

Global navigation should remain simple.

Use:
- site title/logo
- Archive
- About

The site title/logo should link to Home.
Home shows the latest edition.

On edition pages:
- include subtle path back to Archive
- include Previous / Next navigation at the bottom
- avoid extra clutter like heavy related-content modules unless clearly valuable later

Share options belong on the edition page only.

Use:
- Copy link
- LinkedIn
- Email

Do not add share controls to archive tiles.

## Graphics and Images

Edition graphics are an important editorial asset.

They should:
- visually differentiate editions
- hint at the edition’s content/theme
- be prominently featured
- remain polished on both desktop and mobile

Use one primary edition image and derive thumbnail behavior from that image.
Do not require a separately designed thumbnail asset.

Optimize images for speed while preserving a professional visual standard.

Never sacrifice perceived quality so much that the site looks cheap or careless.

## Mobile, Performance, and Quality

### Mobile

Mobile is **equal priority** with desktop.

This is a non-negotiable requirement.

Assume many readers arrive from mobile via LinkedIn or related paths.

Every page and interaction should be designed to work well on mobile, not merely degrade acceptably.

### Performance

Performance is high priority.

Slow loading hurts engagement and credibility.

Prioritize:
- fast page loads
- optimized images
- responsive media handling
- avoiding unnecessary heavy UI features

Balance speed with professional visual quality.

### Accessibility and Readability

Follow current industry good practices for:
- readability
- contrast
- link visibility
- mobile legibility
- alt text and sensible semantic structure
- interaction clarity

Treat accessibility as a baseline quality expectation, not a later add-on.

## Change Management Rules

### Preserve the Existing Foundation

This project already has a base infrastructure.
Preserve it.

Do **not**:
- casually reorganize the project structure
- break existing GitHub/deployment assumptions
- replace the foundation with a different architecture without being asked
- make foundational structural decisions without careful consideration

Design-layer refinements are welcome when they are easy to maintain or reverse.

### Codex Freedom

You have **some freedom** in implementation and design details, but only within the editorial direction and guardrails in this document.

Do not invent a different site identity.

Do not introduce novelty that conflicts with the publication’s tone.

### Structural Decisions

If a possible improvement affects:
- architecture
- long-term flexibility
- deployment assumptions
- future expandability
- content model
- routing/navigation structure

then do **not** silently proceed.

Instead:
- explain the tradeoff in broad terms
- recommend a direction
- preserve the existing foundation unless the change is clearly justified

Do not ask for approval on every small design choice.
Use judgment.
Outline broad strokes, then execute.

### Dependencies

Prefer existing project tools and patterns.

Do not introduce new dependencies casually.

If suggesting a new dependency, explain briefly:
- what it does
- why it is needed
- why existing tools are insufficient
- any meaningful maintenance or flexibility tradeoff

## Consistency and Flexibility

Improve consistency where it strengthens the publication.

Do **not** force rigid standardization that makes future special pieces awkward.

The site must support:
- standard recurring editions
- occasional non-standard editions
- one-off insights
- retrospective pieces
- future expansion into adjacent formats

Keep the overall experience coherent while preserving flexibility.

## Future Expansion Guardrails

Version 1 should stay focused and uncluttered, but do not make choices that block likely future additions.

Potential future directions include:
- Signals section
- source-article search
- linking signals to relevant editions
- richer archive browsing
- site-wide search improvements
- topic/tag browsing
- featured reading paths
- subscription outside LinkedIn
- daily surfaced news driven from Google Sheets / automated workflows

Do not prematurely build these into the public site unless asked.

Do ensure current choices leave room for them.

## Definition of Success for Version 1

Version 1 is successful if:
- it feels like a real publication, not a side project
- it gives Finding Critical Path a durable independent home
- it looks polished and credible enough to share confidently
- it works well on mobile
- it loads quickly
- it avoids clutter and unfinished features
- it supports future expansion without needing a rebuild

## Documentation Requirements

Maintain project documentation automatically after any meaningful site change.

Meaningful changes include anything affecting:
- design direction
- behavior
- navigation
- content model
- structure
- maintainability
- future expansion considerations

Minor cosmetic tweaks do not require heavy documentation.

### Required Documentation Files

Maintain:
- `docs/site-overview.md`
- `docs/development-log.md`

### Documentation Expectations

`docs/site-overview.md` should remain a living handoff document that helps a future teammate understand:
- what the site is for
- who it serves
- how it is structured
- how the content model works
- what design guardrails should be preserved
- how the site should evolve without losing its core identity

`docs/development-log.md` should record meaningful changes over time, including:
- what changed
- why it changed
- files or areas affected
- decisions made
- important follow-up notes or risks

Write documentation clearly enough that a future web designer or developer could understand and continue the work without needing Codex.

## Working Style

For non-trivial work:
- understand the relevant files first
- form a broad-strokes plan
- execute without unnecessary back-and-forth on minor design decisions
- preserve quality, clarity, and flexibility
- document meaningful outcomes

For archive backfill tasks, always audit homepage feature status, archive order, and adjacent previous/next navigation before finishing.
Do not produce clutter.
Do not produce empty public features.
Do not produce fragile short-term solutions that compromise future growth.

Build with restraint, polish, and publication quality in mind.
