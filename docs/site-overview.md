# Finding Critical Path Site Overview

## 1. Project Overview

This site is the web home for **Finding Critical Path**.

It exists to provide a durable, independent home for the publication outside any single company or distribution platform. Its primary purpose is to archive editions of the publication in a way that feels credible, polished, and useful to nuclear professionals.

The site is intended to feel like a **real publication**, not a side project. It should present the work with enough sophistication and structure to invite exploration and build trust.

This is not intended to be:
- a personal website
- a resume site
- a company marketing site
- a generic blog
- a general news aggregator

It is a publication focused on making sense of the signals shaping the nuclear industry.

## 2. Purpose of the Site

The site has three primary jobs:

1. **Archive published editions**  
   It should serve as a durable, organized home for current and past editions.

2. **Act as a credibility layer**  
   It should reinforce the quality, seriousness, and usefulness of the work.

3. **Support future growth**  
   It should establish a foundation that can expand over time into broader publication and signal-tracking capabilities without losing clarity or polish.

## 3. Audience

The primary audience is **nuclear professionals**.

The site should feel like a valuable industry resource for readers who want help making sense of developments across the nuclear sector. It should assume an informed audience and avoid becoming beginner-oriented or overly generalized.

The goal is not to simplify the industry for casual readers. The goal is to provide meaningful signal, insight, and direction for people already engaged with nuclear topics.

## 4. Publication Identity

**Title:** Finding Critical Path  
**Tagline:** From emerging signals to direction.

The publication is best framed as a **publication of weekly editions**, not primarily as a newsletter, even though it is currently distributed through the LinkedIn newsletter platform.

The site should clearly communicate early that the work is focused on the nuclear industry, then allow the content itself to carry that identity without repetitive explanation.

### Working Positioning

Finding Critical Path exists to look broadly across nuclear industry developments, identify the stories and signals shaping the industry, surface meaningful connections, summarize what matters, and point readers back to original sources when they want to explore further.

The publication should feel like a serious nuclear industry resource built around recurring editions and long-term insight.

## 5. Design Direction

The site should feel:

- sophisticated
- clean
- polished
- credible
- expert

The editorial and reading experience should feel:

- refined
- thoughtful
- calm
- professional but approachable
- publication-first

The site should not feel:

- personal
- homegrown in a rough or simplistic way
- generic
- cluttered
- commercial
- flashy
- overly technical in presentation
- obviously templated

### Key Design Goals

The site should:
- invite exploration
- present the work with confidence
- let the writing and graphics carry the experience
- support longform reading without distraction
- remain restrained and uncluttered

### Warning Signs to Avoid

The site risks feeling like a side project if it has:
- an obvious template feel
- clutter
- features that do not add value
- broken links
- empty pages
- poor mobile compatibility

These are critical quality checks for future design and development work.

## 6. Visual Direction

### Color

The visual foundation should be **cool light**.

The overall palette should rely primarily on:
- cool light backgrounds
- neutrals
- strong contrast
- restrained accent use

The site does not need a strong color system beyond what is needed for clarity, emphasis, and alignment with the publication identity. The edition graphics should carry much of the visual differentiation across content.

### Logo

The site already has an existing logo and should use it.

The title and logo should always be present in the site header. The tagline should be visible when arriving on a page, but should not remain dominant as the reader scrolls.

### Typography

Typography should feel **editorial and refined**.

Recommended direction:
- **sans-serif** for navigation, metadata, interface elements, archive support text, and general framing
- **serif** for longform edition body text

This balance supports a publication-like reading experience while keeping the surrounding interface clean and controlled.

### Spacing and Motion

Spacing should be balanced, leaning slightly more spacious than tight.

Motion should be subtle:
- gentle hover states
- light transitions
- no distracting animation
- clear feedback around clickable elements

The header and footer should share the same restrained framing surface so pages feel intentionally bookended without adding visual heaviness.

## 7. Site Structure

Version 1 of the site should include:

- Home
- Archive
- About

No additional pages, public links, or visible sections should be added until they are ready to be public.

The public information architecture should remain centered on those three destinations.

Compatibility routes may still exist for older year, sample, or unpublished paths when needed to preserve the existing structure, but they should resolve quietly into intentional public destinations rather than behaving like parallel public pages.

Do not publish:
- empty pages
- placeholder sections
- “coming soon” pages
- navigation items for future features

### Navigation

The main navigation should remain simple:
- site title/logo
- Archive
- About

The site title/logo should link to Home.

## 8. Homepage Strategy

The homepage should serve as a light-framed entry point centered on the **latest edition**.

It should include:
- title and logo
- tagline
- one sentence of reader-focused value framing
- a preview of the latest edition
- a clear “keep reading” path
- a subtle path to the archive

The homepage should not simply dump the full latest edition inline.

The homepage currently pairs the featured latest edition with a restrained `Past Editions` section beneath it. That supporting section should remain clearly secondary, show only a small number of recent prior editions, and use only graphic, title, and full date before a quiet inline path to the archive.

The archive handoff on the homepage should read as publication continuity rather than as a separate CTA block. Prefer a short sentence with an inline archive link over a labeled archive module.

### Latest Edition Preview

The homepage preview of the latest edition should include:
- hero image
- title
- date range
- excerpt
- keep reading link

When an edition markdown file includes structured opening fields, the homepage latest-edition preview should use them directly in this order:
- `Hook`
- `Hook Text`
- `Tech Framing`

That copy should be preserved verbatim from the markdown source rather than paraphrased, summarized, or regenerated.

The tagline belongs to the page framing, not to the edition preview itself.

The homepage featured-edition action should remain lightweight and editorial, using a simple text link treatment rather than a promotional boxed button.

## 9. Archive Strategy

The archive is a key part of the site and should support browsing in a way that feels modern, clean, and editorial.

### Archive Layout

The archive should use a **restrained stacked editorial row layout**.

Responsive behavior:
- desktop: one edition per row in a split layout
- medium screens: one edition per row with a tighter split layout
- mobile: one edition per row, stacked naturally

The public archive landing page should move quickly from a calm, homepage-related header into the edition rows rather than explaining year structure or directory structure. It should feel like browsing a publication, not opening a records index.

The archive rows should feel like a lighter adaptation of the homepage featured-edition composition rather than a generic content grid.

The archive should currently end structurally into the footer rather than with a separate editorial closing note.

### Archive Entry Content

Each archive row should include:
- edition image
- title
- full date range
- short summary
- optional estimated reading time, shown quietly if it fits cleanly

When structured opening fields are available in the edition markdown, archive preview text should also come from that opening material rather than from new summary writing. Preserve the original wording from the markdown so homepage and archive previews stay editorially aligned with the published edition.

The edition graphic is important and should be given real visual presence in the archive.

Archive preview text should stay restrained. It should support scanning and editorial tone without turning the archive into a text-heavy listing page.

### Archive Loading

The archive currently shows the full set of published editions because the backlog is still small enough to browse comfortably in one view.

`Load more` should not be treated as an immediate default requirement. It should be introduced only once archive volume clearly benefits from progressive reveal rather than full-page scanning.

The long-term preferred behavior is to show a limited initial set of editions, then reveal more in batches through a **Load more** interaction until the full archive is displayed.

### Archive Search

Archive search is not part of the initial public launch state.

When search is introduced, it should live on the archive page and filter results in place.

The first useful search scope should cover:
- edition summary
- full edition text

The goal is to make the archive practically useful, not just visually browseable, but this should be added only when it can be done cleanly.

## 10. About Page Strategy

The About page should include three sections in this order:

1. **Why it exists**
2. **Methodology**
3. **Author bio**

The page should be thoughtful, restrained, and warm.

### Why It Exists

This section should explain the purpose of Finding Critical Path as a publication and why the work matters.

### Methodology

The methodology section should provide a transparent overview of how the publication is put together.

It should cover, at a high level:
- scanning broadly across nuclear industry developments
- identifying meaningful stories and signals
- selecting a smaller set for deeper interpretation
- surfacing connections across the week
- linking readers back to original sources for deeper exploration

This section should remain **light-touch to moderate**. It should build trust without becoming a technical process document.

It may also include a restrained source-acknowledgment subsection within the Methodology area when that helps reinforce credibility. That source treatment should feel curated and editorial, not exhaustive or directory-like.

### Author Bio

The author bio should come last and remain secondary to the publication.

The site should include:
- a small byline on edition pages
- the byline links to the bio section on the About page
- the bio includes a LinkedIn link

The site should remain publication-first, not personality-first.

## 11. Edition Content Model

The core recurring published unit is an **edition**.

Each edition should be identified primarily by:
- title
- full date range

Example:
**March 23–29, 2026**

Issue numbers are not the primary display format.

### Standard Edition Structure

A standard edition page should include:
- title
- date range
- byline
- hero image
- full article
- Dive deeper section
- one understated closing utility band that combines archive/navigation links with share actions

### Flexible Content Support

While most editions will follow a consistent weekly structure, the site should preserve flexibility for:
- one-off insights
- retrospective pieces
- special editions
- other future editorial formats

The site should remain coherent while allowing occasional non-standard pieces.

## 12. Edition Page Layout

The edition page should support a calm, longform reading experience.

### Header Layout

On desktop, the edition header should use a **split editorial layout**:
- text/meta on the left
- hero image on the right

On mobile, the layout should stack naturally.

The edition header should include, in order:
1. title
2. date range
3. byline
4. hero image

A subtitle/deck is not required for version 1 and should not be forced into the format.

### Article Body

The article body should:
- begin below the full header block
- use a medium reading width
- keep good margins on the sides
- feel calm and readable
- avoid interruption-heavy layouts

When structured opening fields are present in the edition markdown, the published article should preserve that opening sequence directly in the body:
- `Hook`
- `Hook Text`
- `Tech Framing`

That opening should appear in the edition itself, not just in homepage or archive previews.

Standard editions should keep a visually continuous longform body. Individual lines from the article should not be broken out as pull quotes or emphasized quote modules unless a future piece explicitly calls for that treatment.

When structured closing fields are present in the edition markdown, the published article should also preserve the markdown wording directly for the close, including the `Structural Close` and `Forward Looking Question`. Those sections should not be shortened, paraphrased, or rewritten in the published edition.

The reading experience should remain the focus.

## 13. References and Source Philosophy

Finding Critical Path is built around interpretation supported by transparent sourcing.

### In-Text References

The article body should include small numbered reference markers such as `[1]`.

These references should:
- provide credibility
- remain visually subtle
- avoid pulling the reader away from the longform experience

They do not need to function like academic footnotes or jump links unless that becomes useful later.

### Dive Deeper Section

Each edition should end with a **Dive deeper** section.

This section should preserve the current format:
- numbered references
- linked article titles
- short explanatory summaries
- source links

This approach supports transparency and deeper exploration while keeping the body of the article clean.

The article-ending utility area beneath `Dive deeper` should read as a single quiet handoff rather than multiple stacked interface bands. Archive access, previous/next edition links, and share actions should live together in one restrained closing section before the global site footer.

## 14. Graphics and Image Strategy

Edition graphics are one of the site’s main visual differentiators.

They should:
- distinguish editions from one another
- give readers an early clue about the edition’s theme
- be treated as meaningful editorial assets, not decoration

The archive and edition pages should both showcase the primary edition graphic.

The workflow should assume:
- one primary image per edition
- no separate manually designed thumbnail required
- thumbnail behavior derived from the main image

Images should be optimized for speed while still looking polished and professional.

## 15. Mobile, Performance, and Readability

### Mobile

Mobile is equal priority with desktop.

This is especially important because readers are likely to arrive from LinkedIn and similar pathways. Mobile usability is a core part of perceived publication quality.

### Performance

Performance is high priority.

Slow loading can significantly reduce engagement and trust. The site should prioritize:
- fast loading
- image optimization
- responsive media behavior
- avoiding unnecessary heavy features

### Accessibility and Readability

The site should follow current industry good practices for:
- readability
- contrast
- mobile legibility
- link visibility
- semantic structure
- image alt text
- general usability

Accessibility should be treated as a baseline quality standard.

## 16. Design Guardrails

The site should always protect:
- publication-first identity
- a clean, sophisticated, credible presentation
- uncluttered pages
- strong mobile experience
- fast loading
- longform reading quality
- flexibility for future expansion
- freedom from obvious template feel
- freedom from public-facing unfinished sections

The site should avoid:
- clutter
- decorative features without value
- fragile design decisions
- architecture choices that limit future growth
- changes that break GitHub or deployment assumptions
- casual structural changes without careful consideration

## 17. Development and Change Principles

The project already has a base infrastructure and that foundation should be preserved.

Future contributors should:
- avoid casually restructuring the project
- avoid making changes that could break GitHub/deployment connections
- be flexible in design-layer updates
- be cautious with structural decisions
- favor extensible patterns over short-term hacks

If a change has architectural implications, it should be considered carefully and documented clearly.

## 18. Future Roadmap Considerations

The version 1 site should remain focused, but it should leave room for future expansion.

### Immediate Post-Launch Polish

The first post-launch work should stay narrow and polish-oriented.

Priority items include:
- social preview metadata and Open Graph-style tags so shared links present cleanly
- favicon and app icon polish
- real-device mobile review of the homepage header reveal behavior

### Archive Growth Path

Archive browsing should evolve in stages based on actual archive volume rather than being introduced preemptively.

**Phase 1:** Show the full archive while the number of published editions is still small enough to browse comfortably in one view.

**Phase 2:** Introduce a limited initial archive display with a **Load more** interaction once the archive is large enough that progressive reveal improves browsing.

**Phase 3:** Add year selection once the publication spans multiple years and year-based browsing becomes genuinely useful.

**Phase 4:** Add **Archive Search** as a later archive usability enhancement once the publication library is large enough that browsing alone becomes less effective. This should help readers quickly find past editions, prioritize a solution that works well with a static site, and eventually support full-text search across edition content, title and excerpt search, and optional future filters such as year, theme, or topic. The goal is to improve discoverability and strengthen the archive as a polished publication resource, not just add a technical feature.

### Later Capability Expansion

Likely later directions include:
- **Signals** section
- search across individual source articles
- broader archive and site search improvements
- linking signals back to related editions
- topic/tag browsing
- featured reading paths
- better markdown-to-page automation
- improved sharing and distribution
- subscription outside LinkedIn
- daily surfaced news driven by Google Sheets / automated workflows

These should not appear publicly until they are ready, but current design and architecture choices should avoid blocking them.

## 19. Definition of Version 1 Success

Version 1 is successful if:
- it feels like a real publication, not a side project
- it gives Finding Critical Path a durable independent home
- it is polished enough to share confidently
- it works well on mobile
- it loads quickly
- it avoids clutter and empty features
- it supports future growth without needing a rebuild

## 20. Documentation Expectations

This site should be maintainable by future teammates without relying on Codex.

To support that, the project should maintain:
- a living site overview
- a development log of meaningful changes

Documentation should be detailed enough that a web designer or developer can:
- understand what the site is trying to achieve
- understand how it is structured
- understand key guardrails and design decisions
- continue improving the site without losing its core identity
