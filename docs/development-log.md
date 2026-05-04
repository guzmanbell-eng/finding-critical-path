# Finding Critical Path Site Development Log

This document records meaningful development work on the Finding Critical Path website.

Its purpose is to create a clear historical record of how the site evolves over time so that future designers, developers, or collaborators can understand:
- what changed
- why it changed
- what decisions were made
- what files or systems were affected
- what follow-up work may still be needed

This log should be updated after any **meaningful** site change.

A meaningful change includes updates to:
- layout
- design direction
- navigation
- content model
- archive behavior
- search behavior
- image handling
- site structure
- documentation
- maintainability
- future expansion considerations

Minor visual tweaks do not need a heavy log entry unless they affect user experience in an important way.

---

### 2026-05-04 - Mobile Horizontal Overflow Fixed After Week 18 Deployment

**Summary**
Removed the narrow-mobile horizontal overflow that appeared on the homepage and Week 18 article page after the Week 18 deployment, while preserving the existing static workflow, article content, publication ordering, navigation, and desktop layout intent.

**Reason for Change**
Live mobile review at roughly 390px wide showed a horizontal scrollbar and right-edge clipping on the homepage and Week 18 article page. Because Week 18 reused the shared homepage, edition, and footer layout patterns, the issue needed to be fixed in shared CSS rather than by changing Week 18 content or markup.

**Likely Cause**
The primary cause was the site's full-bleed decorative band pattern using `100vw` pseudo-elements inside centered containers. On narrow viewports, and also by a few pixels on desktop where the scrollbar gutter is included in `100vw`, those pseudo-elements could create a scrollable horizontal area. Some shared grid and flex children also lacked explicit shrink guards, which made long editorial titles, excerpts, references, images, or utility links more vulnerable to overflow as new edition content varied in length.

**What Changed**
- Added horizontal overflow containment to `.site-shell` using `overflow-x: clip` so decorative full-bleed surfaces cannot create page-level horizontal scrolling
- Added `min-width: 0` to key shared grid/flex children and media containers in the homepage, article, archive, and header layouts
- Added conservative wrapping protection for article body text, featured excerpts, closing utility links, and share controls
- Slightly reduced small-screen display-type ceilings for homepage/edition titles so longer titles wrap more comfortably on phone widths
- Constrained the homepage lead and footer pseudo-elements to the local container width inside the small-screen breakpoint to avoid mobile edge spill from decorative background bands

**Files or Areas Affected**
- `assets/css/site.css`
- `docs/development-log.md`

**Design or Structural Decisions**
This was kept as a CSS-only layout repair. No article copy, archive chronology, homepage ordering, navigation structure, image assets, scripts, dependencies, build logic, or deployment assumptions were changed. `docs/site-overview.md` was intentionally left unchanged because the documented site behavior and future guidance did not change; this was an implementation-quality fix within the existing mobile guardrails.

**Mobile / Performance / Accessibility Notes**
- Verified with local static serving and Chrome device emulation that `scrollWidth` equals `clientWidth` at 360px, 390px, and 430px for the homepage, Week 18, archive, and Week 17 pages
- Verified the same four pages at 1280px width to confirm the fix did not introduce desktop horizontal overflow
- Measured key 390px elements, including homepage intro, featured title, featured image, featured excerpt, Week 18 title, article body, hero image, and closing utility area, and confirmed their bounding boxes fit inside the viewport
- No new runtime cost, dependency, or script behavior was introduced
- The changes support mobile readability by allowing long titles and link text to wrap rather than forcing page overflow

**Risks / Watchouts**
- Because the site is static and edition content varies by hand, future weekly deployments should continue checking narrow mobile widths after adding longer titles, long reference titles, or unusually wide imagery
- Real-device mobile review remains valuable for the homepage header reveal and logo area, especially because browser chrome, font rendering, and scrollbar behavior can differ from headless validation

**Follow-Up Opportunities**
- Add narrow mobile overflow checks to the manual weekly publication checklist so future edition releases catch layout pressure from long titles, source links, or new image proportions before deployment
- Include at least one real-device mobile review after deployment when homepage framing, hero imagery, or title length changes materially


### 2026-05-04 - Week 18 Published As Latest Edition

**Summary**  
Published Week 18 as the new latest edition, promoted it on the homepage, added it to the top of the archive, and connected adjacent navigation between Weeks 17 and 18 while preserving the site's manual static-content workflow.

**Reason for Change**  
Week 18 source markdown and image assets were already prepared, but the site does not auto-discover new editions. The live article route, homepage, archive, and adjacent article navigation needed to be updated manually so the newest published edition appears consistently across public surfaces.

**What Changed**  
- Created the live Week 18 edition page at `archive/2026/week-18/index.html`
- Carried the Week 18 title, normalized public date range, hero image, opening, body, closing, references, and process note directly from `content/2026/week-18.md`
- Promoted Week 18 into the homepage featured latest-edition area using the markdown's `Hook`, `Hook Text`, and `Tech Framing` wording verbatim
- Shifted the homepage `Past Editions` strip so it now shows Weeks 17, 16, and 15 in reverse chronological order behind the new latest edition
- Added Week 18 to the top of the main archive in reverse chronological position
- Updated adjacent edition navigation so Week 17 now links forward to Week 18 and Week 18 links back to Week 17

**Files or Areas Affected**  
- `archive/2026/week-18/index.html`
- `archive/2026/week-17/index.html`
- `index.html`
- `archive/index.html`
- `docs/development-log.md`

**Design or Structural Decisions**  
This remained a manual static-content integration within the site's existing edition template, homepage feature treatment, archive list pattern, and closing utility navigation. No new dependency, build step, automated discovery layer, or architecture change was introduced, and `docs/site-overview.md` did not need updating because site behavior and guidance stayed the same.

**Mobile / Performance / Accessibility Notes**  
- No new dependencies or additional scripts were introduced beyond the existing edition-page share behavior
- Week 18 reuses the site's established responsive article layout, homepage feature block, and archive row pattern to preserve mobile behavior
- The Week 18 hero and archive/homepage image alt text were taken directly from the markdown metadata for consistent accessibility treatment
- The existing image path pattern and shared stylesheet were reused, preserving current static deployment and performance assumptions

**Risks / Watchouts**  
- The markdown-to-HTML workflow is still manual, so homepage, archive, article route, and adjacent navigation must continue to be checked together for each future edition
- Reading time, preview placement, article markup, and public date formatting are still maintained by hand, which leaves room for drift if future updates miss one of the public surfaces
- Because the site does not auto-discover edition metadata, future publication passes should continue verifying chronology, asset filenames, alt text, and links against the markdown source of truth

**Follow-Up Opportunities**  
- Review the homepage, archive, and Week 18 article route in-browser on mobile and desktop to confirm the new edition image and opening copy sit cleanly within the existing responsive layout
- If the manual workflow continues, consider turning the repeated weekly publication checks into a concise checklist so future integrations are less likely to miss one of the public surfaces


### 2026-04-30 - Week 17 Published As Latest Edition

**Summary**  
Published Week 17 as the new latest edition, promoted it on the homepage, added it to the top of the archive, and connected adjacent navigation between Weeks 16 and 17 without changing the site's manual static workflow.

**Reason for Change**  
Week 17 source markdown and image assets were already prepared, but the site does not auto-discover new editions. The publication state needed a focused manual update so the newest published edition appears consistently across the article route, homepage, archive, and edition-to-edition navigation.

**What Changed**  
- Created the live Week 17 edition page at `archive/2026/week-17/index.html`
- Carried the Week 17 title, date range, hero image, opening, body, closing, references, and process note directly from `content/2026/week-17.md`
- Promoted Week 17 into the homepage featured latest-edition area using the markdown's `Hook`, `Hook Text`, and `Tech Framing` wording verbatim
- Shifted the homepage `Past Editions` strip so it now shows Weeks 16, 15, and 14 in reverse chronological order behind the new latest edition
- Added Week 17 to the top of the main archive in reverse chronological position
- Updated adjacent edition navigation so Week 16 now links forward to Week 17 and Week 17 links back to Week 16

**Files or Areas Affected**  
- `archive/2026/week-17/index.html`
- `archive/2026/week-16/index.html`
- `index.html`
- `archive/index.html`
- `docs/development-log.md`

**Design or Structural Decisions**  
This remained a manual static-content integration within the site's existing edition template, homepage feature treatment, archive list pattern, and closing utility navigation. No new dependency, build step, automation layer, or architecture change was introduced, and `docs/site-overview.md` did not need updating because site behavior and guidance stayed the same.

**Mobile / Performance / Accessibility Notes**  
- No new dependencies or additional scripts were introduced beyond the existing shared edition-page share behavior
- Week 17 reuses the site's established responsive article layout, homepage feature block, and archive row pattern to preserve mobile behavior
- The Week 17 hero and archive/homepage image alt text were taken directly from the markdown metadata for consistent accessibility treatment
- The existing image path pattern and shared stylesheet were reused, preserving current static deployment and performance assumptions

**Risks / Watchouts**  
- The markdown-to-HTML workflow is still manual, so homepage, archive, article route, and adjacent navigation must continue to be checked together for each future edition
- Reading time, preview placement, and article markup are still maintained by hand, which leaves room for drift if future updates miss one of the public surfaces
- Because the site does not auto-discover edition metadata, future publication passes should continue verifying chronology and asset filenames against the markdown source of truth

**Follow-Up Opportunities**  
- Review the homepage, archive, and Week 17 article route in-browser on mobile and desktop to confirm the new edition image and long opening copy sit cleanly within the existing responsive layout
- If the manual workflow continues, consider documenting a short repeatable publication checklist so future weekly integrations are less likely to miss one of the public surfaces


### 2026-04-24 - Week 4 Launch Graphic Alt Text Corrected

**Summary**  
Updated the Week 4 launch article image alt text so it accurately describes the current Finding Critical Path logo graphic instead of a generic editorial illustration.

**Reason for Change**  
The Week 4 page uses the publication logo as its launch graphic, so the previous alt text overstated the visual content and no longer matched the image. The correction keeps the existing image and layout unchanged while improving accessibility accuracy.

**Files or Areas Affected**  
- `content/2026/week-04.md`
- `archive/2026/week-04/index.html`
- `archive/index.html`
- `docs/development-log.md`

### 2026-04-23 - Cloudflare Web Analytics Snippet Installed

**Summary**  
Added the Cloudflare Web Analytics snippet to every public HTML page so lightweight analytics can load site-wide without changing the site's structure or behavior.

**Reason for Change**  
The site needed a minimal analytics layer for public-page traffic measurement without introducing another analytics tool or changing deployment, routing, or content behavior.

**Files or Areas Affected**  
- `index.html`
- `about/index.html`
- `archive/index.html`
- `archive/2026/index.html`
- `archive/2026/week-04/index.html`
- `archive/2026/week-05/index.html`
- `archive/2026/week-06/index.html`
- `archive/2026/week-07/index.html`
- `archive/2026/week-08/index.html`
- `archive/2026/week-09/index.html`
- `archive/2026/week-10/index.html`
- `archive/2026/week-11/index.html`
- `archive/2026/week-12/index.html`
- `archive/2026/week-13/index.html`
- `archive/2026/week-14/index.html`
- `archive/2026/week-15/index.html`
- `archive/2026/week-16/index.html`
- `methodology/index.html`
- `docs/development-log.md`

### 2026-04-23 - Week 4 Hero Graphic Height Brought In Line

**Summary**  
Reduced the displayed size of the Week 4 launch graphic on both the article page and the main archive so the square image sits at a calmer height that better matches later edition presentation.

**Reason for Change**  
The Week 4 launch graphic was rendering noticeably taller than the newer edition hero treatment, both on the article page and in the archive list. A small page-specific sizing adjustment keeps the image square while bringing its visual height closer to the Week 16 presentation.

**Files or Areas Affected**  
- `archive/2026/week-04/index.html`
- `archive/index.html`
- `assets/css/site.css`
- `docs/development-log.md`

### 2026-04-23 - About Page Launch Article Link Added

**Summary**  
Added a quiet inline link to the published launch article in the About page's `Why it exists` section.

**Reason for Change**  
The About page needed a small editorial bridge back to the publication's launch piece so readers can find the original framing without adding a new module or changing the page's restrained tone.

**Files or Areas Affected**  
- `about/index.html`
- `docs/development-log.md`

### 2026-04-23 - Weeks 4 Through 11 Backfilled Into Published Archive

**Summary**  
Published archive editions for weeks 4 through 11, replaced the old placeholder redirects in that range, and reconnected the full published edition chain from the launch piece through Week 16 without disturbing the true latest-edition homepage state.

**Reason for Change**  
The markdown and graphics for weeks 4 through 11 were already prepared, but most of those routes were still unpublished placeholders. The site needed a clean archive backfill that respected publication chronology, preserved the existing static edition pattern, and kept the homepage anchored to the true latest edition rather than the most recently integrated files.

**What Changed**  
- Added a live Week 4 archive page at `archive/2026/week-04/index.html` and treated it as the special launch/intro archive piece within the normal published chain
- Replaced the redirect placeholder routes for weeks 5 through 11 with full published edition pages
- Carried the week 4 through 11 markdown title, date, hero image, article body, and `Dive deeper` material into the live archive pages where those sections exist
- Preserved each markdown file's structured opening and closing wording where those structures exist, while keeping the body presentation continuous and editorial
- Updated `archive/index.html` so the public archive now lists the full published sequence in reverse chronological order from Week 16 through Week 4
- Updated adjacent edition navigation so the published chain now runs continuously from Week 4 to Week 16, including adding Week 11 as the `Previous edition` link on Week 12
- Left the homepage unchanged because Week 16 remains the true latest published edition by chronology and the homepage `Past Editions` strip already reflected the correct three prior published editions
- Corrected Week 5 markdown metadata so `content/2026/week-05.md` now points to the actual existing asset filename `w05cover.jpg`

**Files or Areas Affected**  
- `content/2026/week-05.md`
- `archive/2026/week-04/index.html`
- `archive/2026/week-05/index.html`
- `archive/2026/week-06/index.html`
- `archive/2026/week-07/index.html`
- `archive/2026/week-08/index.html`
- `archive/2026/week-09/index.html`
- `archive/2026/week-10/index.html`
- `archive/2026/week-11/index.html`
- `archive/2026/week-12/index.html`
- `archive/index.html`
- `docs/development-log.md`

**Design or Structural Decisions**  
This backfill stayed inside the site's established static publication workflow. The main archive remained the public archive surface, the homepage latest-edition treatment was left untouched, and no new layout pattern or generation step was introduced. Week 4 was intentionally integrated as a special introductory archive piece, so it was published in chronology and navigation without forcing it into a newer standard-edition shape it does not fully use.

**Mobile / Performance / Accessibility Notes**  
- No new dependencies or scripts were introduced
- The backfilled editions reuse the current responsive edition-page template and archive row pattern
- The hero image alt text for each backfilled edition was carried from markdown metadata
- The archive remains a single-page chronological browse surface, which should still be checked in-browser now that the published list is materially longer

**Risks / Watchouts**  
- This workflow is still manual, so future backfills or corrections should continue checking for drift between markdown metadata, asset filenames, archive rows, and published page navigation
- Week 4 is intentionally different from the later weekly brief structure, so its live page should be reviewed in-browser to confirm the special intro piece still feels clean inside the standard edition shell

### 2026-04-22 - Homepage Logo Load-State Stabilized On Mobile

**Summary**  
Stabilized the homepage intro logo on mobile so it no longer narrows during first paint before the branding layout settles.

**Reason for Change**  
The earlier mobile sizing guard corrected the final layout, but the homepage logo still depended on load-time image sizing and row-based measurements. On mobile, that allowed a brief squeeze before the image dimensions and intro layout fully resolved, creating visible layout shift in the branding area.

**What Changed**  
- Wrapped the homepage intro logo in a dedicated `.home-logo-wrap` element that becomes a reserved square box on mobile with `aspect-ratio: 1 / 1`
- Gave the mobile logo wrapper an explicit `3.3rem` width and matching `min-width` so the logo column stays stable from first paint
- Updated `.home-logo` to use `display: block`, `width: 100%`, and `height: auto`
- Added intrinsic `width` and `height` attributes (`1056` by `1056`) to the homepage logo markup so the browser can reserve image dimensions during load

**Files or Areas Affected**  
- `index.html`
- `assets/css/site.css`
- `docs/site-overview.md`
- `docs/development-log.md`

**Design or Structural Decisions**  
Kept the fix narrow and homepage-focused. The intro still uses the same two-column editorial composition, but the logo now lives in a reserved wrapper rather than letting the image itself determine the column width during load.

**Mobile / Performance / Accessibility Notes**  
- Reduces mobile CLS risk by reserving the logo box before image decode completes
- Keeps desktop layout and homepage typography intact
- Introduces no new dependencies or script behavior
- Still worth confirming on a real mobile device, since this issue was specifically paint-order sensitive

### 2026-04-21 - Mobile Homepage Logo Compression Fixed

**Summary**  
Adjusted the homepage intro logo sizing on small screens so the Finding Critical Path mark now keeps a stable proportional width instead of compressing when space gets tight.

**Reason for Change**  
On mobile, the homepage logo could visually narrow inside the intro framing as the adjacent text column compressed. The logo needed to hold its intended presence while letting the text side absorb the responsive pressure.

**What Changed**  
- Updated the mobile `.home-logo` rule so the logo now fills the fixed mobile logo column with `width: 100%` and `height: auto`
- Added a matching mobile `min-width` so the logo keeps a stable width inside the homepage intro layout
- Applied the same sizing rule to the scrolled-homepage state so the logo remains proportional after the header reveal behavior engages

**Files or Areas Affected**  
- `assets/css/site.css`
- `docs/development-log.md`

**Design or Structural Decisions**  
This was kept as a narrow CSS-only fix within the existing homepage composition. The mobile intro still uses the same two-column layout, but the text column now absorbs responsive compression instead of the logo.

**Mobile / Performance / Accessibility Notes**  
- Mobile-only CSS adjustment with no desktop layout change
- No scripts, dependencies, or markup changes were introduced
- The logo image continues to render proportionally using intrinsic aspect ratio

### 2026-04-21 - Week 16 Integrated As Live Latest Edition

**Summary**  
Published Week 16 as a live edition page and promoted it into the site's current latest-edition flow.

**Reason for Change**  
The Week 16 markdown and edition graphic were already prepared. The site needed the edition published through the established static article pattern, then surfaced in the homepage, archive, and adjacent edition navigation without changing the site's structure or deployment assumptions.

**What Changed**  
- Added a published Week 16 edition page at `archive/2026/week-16/index.html`
- Carried the Week 16 title, date, hero image, continuous article body, and `Dive deeper` entries from `content/2026/week-16.md` into the live edition page
- Preserved the markdown wording directly for the Week 16 `Hook`, `Hook Text`, `Tech Framing`, `Structural Close`, and `Forward Looking Question`
- Promoted Week 16 into the homepage featured latest-edition slot using the markdown's `Hook`, `Hook Text`, and `Tech Framing` verbatim
- Shifted the homepage `Past Editions` strip so it now shows the prior published sequence behind Week 16 in reverse chronological order
- Added Week 16 to the main archive in reverse chronological position ahead of Week 15
- Updated adjacent edition navigation so Week 15 now links forward to Week 16 and Week 16 links back to Week 15
- Confirmed the existing Week 16 asset at `assets/2026/week-16/w16cover.png` already matched the markdown metadata and required no rename or path correction
- Completed a post-integration drift check across the markdown source, live edition page, homepage, archive, asset path, alt text, and adjacent navigation; no additional website corrections were required

**Files or Areas Affected**  
- `assets/2026/week-16/w16cover.png`
- `archive/2026/week-16/index.html`
- `archive/2026/week-15/index.html`
- `archive/index.html`
- `index.html`
- `docs/development-log.md`

**Design or Structural Decisions**  
This remained a manual static-content integration within the site's existing edition template, homepage feature treatment, archive row pattern, and closing utility band. No new image handling, layout pattern, or publication structure was introduced.

**Mobile / Performance / Accessibility Notes**  
- No new dependencies or scripts were introduced
- Week 16 reuses the site's existing responsive edition-page pattern
- The hero image alt text was taken from the markdown metadata
- Homepage and archive updates stayed within the current lightweight static markup flow

### 2026-04-19 - Site Overview Synced To Final Launch State

**Summary**  
Updated the site overview so it now describes the implemented initial public launch state more accurately and lays out the near-term roadmap in a staged, practical way.

**Reason for Change**  
The site had reached its intended initial public state, but `docs/site-overview.md` still reflected some earlier assumptions and future-oriented language. The overview needed to function as a clean handoff document for the actual launch posture rather than a partially aspirational spec.

**What Changed**  
- Updated the site structure guidance to clarify that the public information architecture is centered on Home, Archive, and About
- Documented that compatibility routes may still exist for older year, sample, or unpublished paths, but should resolve quietly into intentional public destinations
- Updated the homepage guidance to describe the current featured latest edition plus `Past Editions` pattern as the implemented launch behavior
- Refined the archive guidance to reflect the current full-archive display, restrained stacked editorial row layout, structural ending into the footer, and staged future scaling path
- Clarified that archive search is not part of the initial launch state and should be added later only when it can be introduced cleanly
- Expanded the future roadmap section to distinguish immediate post-launch polish from later archive scaling and broader capability expansion

**Files or Areas Affected**  
- `docs/site-overview.md`
- `docs/development-log.md`

**Design or Structural Decisions**  
The overview now treats the current site as a finished initial launch rather than an in-progress prototype. Future work is framed in staged layers so later contributors can preserve the publication-first launch state without prematurely adding complexity.

**Mobile / Performance / Accessibility Notes**  
- Documentation-only change with no runtime impact
- The updated roadmap now explicitly calls out a real-device mobile review of the homepage header reveal behavior as immediate post-launch polish

### 2026-04-19 - Public Edition Date Formatting Normalized

**Summary**  
Normalized visible public edition date ranges so homepage, archive, and published edition pages now use one consistent editorial date style.

**Reason for Change**  
Small inconsistencies in visible date formatting were making the site feel slightly unfinished. The public-facing edition dates needed to read the same way everywhere they appear.

**What Changed**  
- Standardized surfaced public date ranges to use an en dash style such as `March 15–21, 2026`
- Updated the homepage featured and past-edition dates to match that standard
- Updated the main archive dates to match the same standard
- Updated the published edition page date lines, along with matching page-description date strings, so the current public edition pages stay consistent

**Files or Areas Affected**  
- `index.html`
- `archive/index.html`
- `archive/2026/week-12/index.html`
- `archive/2026/week-13/index.html`
- `archive/2026/week-14/index.html`
- `archive/2026/week-15/index.html`
- `docs/development-log.md`

**Design or Structural Decisions**  
This was kept as a narrow consistency pass rather than a broader content edit. The standard now matches the editorial date-range style documented for the publication and applies it uniformly across surfaced public pages.

**Mobile / Performance / Accessibility Notes**  
- Copy-only HTML updates with no layout or behavior changes
- No scripts or dependencies were added
- The standardized dates remain clear and legible across desktop and mobile

### 2026-04-19 - Year Archive Route Folded Into Main Archive

**Summary**  
Replaced the standalone 2026 archive page with a redirect/fallback route so the public archive experience stays centered on the main archive page.

**Reason for Change**  
The `archive/2026/index.html` route was still publicly accessible in an older archive treatment, which made the site feel like it had two competing archive systems. That weakened the intended Home / Archive / About framing and needed to be cleaned up before launch.

**What Changed**  
- Replaced `archive/2026/index.html` with a redirect page instead of a standalone archive listing
- Pointed the route to the main archive so readers land on the current public archive experience
- Removed the older year-specific archive presentation from public browsing while preserving the route as a compatibility fallback

**Files or Areas Affected**  
- `archive/2026/index.html`
- `docs/development-log.md`

**Design or Structural Decisions**  
This was handled as a minimal route-level cleanup rather than a broader archive refactor. Redirecting the year archive into the main archive preserves the current structure while making the public archive system feel singular, intentional, and publication-first.

**Mobile / Performance / Accessibility Notes**  
- Lightweight HTML-only redirect/fallback page
- No new scripts or dependencies were added
- The route still resolves cleanly if visited directly on desktop or mobile

### 2026-04-19 - Week 10 Sample Route Removed From Public Edition Flow

**Summary**  
Replaced the live Week 10 sample-style article page with a redirect/fallback route so unpublished sample content is no longer publicly exposed.

**Reason for Change**  
The Week 10 route was still behaving like a normal published edition even though it contained sample/test-style article content and implementation language. That weakened launch trust and needed to be resolved before public publishing.

**What Changed**  
- Replaced `archive/2026/week-10/index.html` with a redirect page instead of a live article page
- Pointed the route to the main archive so visitors land on an intentional public browse page
- Removed public exposure of the sample article body, sample `Dive deeper` copy, and sample-only utility treatment from the Week 10 route

**Files or Areas Affected**  
- `archive/2026/week-10/index.html`
- `docs/development-log.md`

**Design or Structural Decisions**  
This was handled as a minimal route-level cleanup rather than a broader restructuring pass. Redirecting Week 10 into the main archive preserves the existing archive structure while making sure unpublished sample material does not read like a real public edition.

**Mobile / Performance / Accessibility Notes**  
- Lightweight HTML-only redirect/fallback page
- No new scripts or dependencies were added
- The route still resolves cleanly if visited directly on desktop or mobile

### 2026-04-18 - Archive Growth Path Clarified In Site Overview

**Summary**  
Updated the site overview documentation so the archive loading strategy now reflects a staged progression tied to actual archive size rather than a fixed early `Load more` rule.

**Reason for Change**  
The archive backlog is still small enough to browse comfortably in one view, so the documentation needed to clarify that full-archive display remains the right default for now. It also needed to document the intended future progression so later contributors do not introduce progressive loading or year filters before they are genuinely useful.

**What Changed**  
- Replaced the archive loading guidance in `docs/site-overview.md` with language that allows the full archive to remain visible while the backlog is still small
- Documented that `Load more` should be introduced only when archive volume clearly benefits from progressive reveal
- Added an archive-specific future roadmap subsection describing the intended progression from full archive display, to limited initial display with `Load more`, to year selection once multiple publication years exist

**Files or Areas Affected**  
- `docs/site-overview.md`
- `docs/development-log.md`

**Design or Structural Decisions**  
The archive should stay simple while it is short. Progressive loading and year-based browsing are future tools, not default requirements, and should be introduced only when archive scale makes them meaningfully useful.

**Mobile / Performance / Accessibility Notes**  
- Documentation-only change with no runtime impact
- The guidance supports a simpler browsing experience in the near term while leaving room for a more scalable archive later

### 2026-04-18 - Archive Ending Simplified

**Summary**  
Removed the archive closing line and tightened the end spacing so the final archive row now resolves more cleanly into the footer.

**Reason for Change**  
In practice, the added editorial sign-off felt unnecessary. The archive needed a cleaner structural ending with noticeably less space after the final row, but still enough room to avoid feeling cramped.

**What Changed**  
- Removed the `More next week.` closing line from the archive page
- Reduced the archive page’s bottom padding so the footer sits closer to the last archive entry
- Kept the rest of the archive layout and footer treatment unchanged

**Files or Areas Affected**  
- `archive/index.html`
- `assets/css/site.css`
- `docs/development-log.md`

**Design or Structural Decisions**  
The archive now ends structurally rather than editorially. Tightening the archive-specific bottom spacing preserves a calm finish while avoiding the hanging gap that had developed between the last entry and the footer.

**Mobile / Performance / Accessibility Notes**  
- The tighter end spacing is applied on both desktop and mobile
- No interaction changes
- No scripts or dependencies were added

### 2026-04-18 - Archive Closing Note Added

**Summary**  
Added a short editorial closing line at the end of the archive page so the page lands more intentionally before the footer.

**Reason for Change**  
After the final archive entry, the page was ending too abruptly and felt slightly unfinished. A small publication-voice closing note helps the archive resolve more cleanly without adding promotional UI.

**What Changed**  
- Added the line `More next week.` below the final archive entry
- Styled it as a quiet editorial note rather than a heading, button, or CTA
- Used a restrained top rule and tightened end spacing so the transition into the footer feels more deliberate

**Files or Areas Affected**  
- `archive/index.html`
- `assets/css/site.css`
- `docs/development-log.md`

**Design or Structural Decisions**  
The closing note reuses the publication’s existing editorial voice and sits as a minimal sign-off after the archive list. The treatment stays understated so it finishes the page without competing with the archive entries themselves.

**Mobile / Performance / Accessibility Notes**  
- No interaction changes
- The closing note remains readable and unobtrusive on mobile
- No scripts or dependencies were added

### 2026-04-18 - Archive Grid Reworked Into Editorial Rows

**Summary**  
Replaced the archive page’s multi-column tile grid with a stacked editorial row layout that feels more consistent with the homepage’s split composition.

**Reason for Change**  
The earlier archive cleanup improved polish, but the three-across grid still felt too generic and gallery-like. The archive needed a more publication-shaped browse pattern that better matched the homepage’s editorial rhythm.

**What Changed**  
- Replaced the main archive grid with one published edition per row
- Switched each archive entry to a text-left, image-right split layout on larger screens
- Moved reading-time treatment into a quiet metadata line alongside the full date range
- Preserved concise preview text and the existing `Read edition` action
- Kept the archive header restrained while making the edition rows feel more deliberate and publication-like

**Files or Areas Affected**  
- `archive/index.html`
- `assets/css/site.css`
- `docs/site-overview.md`
- `docs/development-log.md`

**Design or Structural Decisions**  
The archive rows intentionally echo the homepage’s text-first editorial split without copying the homepage hero outright. This keeps the archive clearly secondary to the homepage while giving each published edition more presence and reducing the generic card-grid feel.

**Mobile / Performance / Accessibility Notes**  
- Archive entries now collapse into a natural stacked layout on smaller screens
- No scripts or dependencies were added
- Existing archive links and published-edition ordering were preserved
- The reading-time treatment remains visible but quieter than the earlier image-badge version

### 2026-04-18 - Archive Landing Page Refined Into Editorial Edition Grid

**Summary**  
Reworked the main archive page from a year-oriented list into a calmer image-led edition grid that feels much closer to the homepage’s editorial tone and visual quality.

**Reason for Change**  
The previous archive page felt procedural and text-heavy, with too much emphasis on year structure and not enough emphasis on the published editions themselves as meaningful editorial objects.

**What Changed**  
- Replaced the old archive intro copy with a calmer publication-focused header area
- Removed the year-archive framing and direct year-archive CTA from the main archive page
- Rebuilt the published-editions presentation as a restrained responsive tile grid
- Gave each published edition stronger graphic presence through a visible cover image
- Added quiet reading-time labels on the edition images
- Switched archive preview copy to direct opening lines from the published edition wording rather than generic listing summaries
- Kept the archive ordered in reverse chronology using only currently published editions

**Files or Areas Affected**  
- `archive/index.html`
- `assets/css/site.css`
- `docs/site-overview.md`
- `docs/development-log.md`

**Design or Structural Decisions**  
The new archive layout borrows the homepage’s light framing language through a restrained intro band and editorial divider, but keeps the archive distinct by presenting all published editions as equally browsable entries rather than featuring one dominant lead story. The edition tiles intentionally avoid heavy boxed-card styling so the page stays polished and publication-first rather than template-like.

**Mobile / Performance / Accessibility Notes**  
- The archive grid now shifts intentionally from 3 columns to 2 columns to 1 column across the existing breakpoints
- Cover images remain visible and readable on mobile, including the quiet reading-time label treatment
- No scripts or dependencies were added
- Existing archive links and publication ordering were preserved

### 2026-04-18 - Homepage Featured Edition Handoff Tightened

**Summary**  
Refined the spacing between the homepage featured-edition excerpt and the `Keep reading` link so the transition feels more editorial and connected.

**Reason for Change**  
The previous spacing left the `Keep reading` link feeling too detached from the end of the featured-edition preview, which weakened the handoff into the full article.

**What Changed**  
- Reduced the bottom margin on the featured-edition excerpt container
- Removed the trailing bottom margin from the excerpt’s final paragraph so the link sits closer to the closing line of preview text
- Kept the existing homepage structure, wording, and `Keep reading` link styling unchanged

**Files or Areas Affected**  
- `assets/css/site.css`
- `docs/development-log.md`

**Design or Structural Decisions**  
The spacing was reduced moderately rather than aggressively so the homepage keeps its calm, airy rhythm while making the `Keep reading` link feel like a natural continuation of the preview instead of a detached action block.

**Mobile / Performance / Accessibility Notes**  
- Responsive behavior remains unchanged
- No structural or interaction changes
- Title and image links remain as-is
- No performance impact

### 2026-04-18 - Footer Surface Aligned With Header

**Summary**  
Updated the site-wide footer background treatment so it uses the same cool framed surface as the header, creating a more cohesive page shell without making the footer heavier.

**Reason for Change**  
The footer needed to feel more integrated with the publication framing already established by the header. Matching the surfaces strengthens visual cohesion while preserving the site’s restrained editorial tone.

**What Changed**  
- Introduced a shared `--frame-surface` token for the existing header background value
- Updated the header to read from that shared token instead of repeating the raw value
- Applied the same surface value to the footer with a full-bleed background treatment that keeps the footer content width and spacing unchanged
- Preserved the existing footer typography, separator treatment, and overall minimal presentation

**Files or Areas Affected**  
- `assets/css/site.css`
- `docs/site-overview.md`
- `docs/development-log.md`

**Design or Structural Decisions**  
The footer now reuses the exact header surface value rather than a near-match. A pseudo-element provides the full-width footer background so the layout can keep its current constrained content width without requiring HTML structure changes.

**Mobile / Performance / Accessibility Notes**  
- No interaction changes
- No additional scripts or dependencies
- Footer remains visually quiet and wraps naturally on smaller screens
- The change is purely presentational and keeps contrast and readability intact

### 2026-04-18 - Footer Copyright Encoding Normalized

**Summary**  
Normalized the repeated footer copyright marker across the site so it renders consistently as a proper copyright symbol on every page.

**Reason for Change**  
Several pages were displaying a mojibake sequence (`Â©`) before the copyright notice, which weakened polish and indicated inconsistent character handling in the repeated footer markup.

**What Changed**  
- Replaced the footer copyright marker with the HTML entity `&copy;` across all site pages that use the shared footer wording
- Verified the HTML documents already include a `<meta charset="utf-8">` declaration in the head
- Kept the existing footer wording, separator, and LinkedIn link unchanged

**Files or Areas Affected**  
- `index.html`
- `about/index.html`
- `archive/index.html`
- `archive/2026/index.html`
- `archive/2026/week-05/index.html`
- `archive/2026/week-06/index.html`
- `archive/2026/week-07/index.html`
- `archive/2026/week-08/index.html`
- `archive/2026/week-09/index.html`
- `archive/2026/week-10/index.html`
- `archive/2026/week-11/index.html`
- `archive/2026/week-12/index.html`
- `archive/2026/week-13/index.html`
- `archive/2026/week-14/index.html`
- `archive/2026/week-15/index.html`
- `methodology/index.html`
- `docs/development-log.md`

**Design or Structural Decisions**  
Using the HTML entity avoids relying on the file’s literal copyright character encoding while preserving the existing editorial footer copy exactly as rendered in the browser.

**Mobile / Performance / Accessibility Notes**  
- No layout or interaction changes
- No performance impact
- Footer text now renders consistently without introducing special character ambiguity

### 2026-04-14 - Homepage Past Editions Section Added

**Summary**  
Replaced the simple homepage archive callout with a restrained `Past Editions` section that shows recent publication continuity beneath the featured edition.

**Reason for Change**  
The archive handoff had become too slight after simplification. A small recent-editions section provides a better editorial sense of continuity while still keeping the featured latest edition clearly dominant.

**What Changed**  
- Replaced the homepage archive callout with a `Past Editions` section
- Added recent prior editions using only graphic, title, and full date
- Kept the follow-on archive path as a quiet inline sentence: `Explore more past editions in the archive.`
- Added minimal homepage-scoped CSS for the lighter past-editions layout

**Files or Areas Affected**  
- `index.html`
- `assets/css/site.css`
- `docs/site-overview.md`
- `docs/development-log.md`

**Design or Structural Decisions**  
The section uses a restrained grid and lighter typography so it reads as supporting publication context rather than as a second hero. The divider was kept to preserve a calm sectional break below the featured edition. Only currently published prior editions were included, which means the section presently shows two items rather than three until another past issue is publicly available.

**Mobile / Performance / Accessibility Notes**  
- The layout collapses into a simpler stacked list on smaller screens
- The section uses existing image and text patterns without adding scripts or interaction complexity

### 2026-04-14 - Homepage Archive Path Simplified

**Summary**  
Simplified the homepage archive path from a labeled mini-section into a single quiet sentence with an inline archive link.

**Reason for Change**  
The previous archive treatment carried too much structure for a secondary navigation path and pulled unnecessary attention away from the featured edition.

**What Changed**  
- Removed the `Archive` section label from the homepage archive path
- Removed the separate `Open the archive` CTA treatment
- Replaced the block with the sentence `Explore past editions in the archive.`
- Kept the archive link inline so the handoff feels lighter and more editorial

**Files or Areas Affected**  
- `index.html`
- `assets/css/site.css`
- `docs/site-overview.md`
- `docs/development-log.md`

**Design or Structural Decisions**  
The divider above the archive path was kept because it still helps separate the featured edition from the quieter secondary navigation without making the archive feel like a competing module.

**Mobile / Performance / Accessibility Notes**  
- No behavior changes
- The simplified archive path remains clearly accessible and visually lighter on both desktop and mobile

### 2026-04-14 - Footer Copy Reordered

**Summary**  
Refined the site-wide footer copy order and separator so the footer reads more cleanly and more like restrained publication metadata.

**Reason for Change**  
The previous footer punctuation felt busier than needed. Reordering the reserved-rights text and using a spaced vertical bar creates a cleaner reading rhythm while keeping the LinkedIn follow path quiet.

**What Changed**  
- Reordered the footer line so the reserved-rights statement leads
- Replaced the previous separator treatment with a spaced vertical bar
- Kept the existing `Follow on LinkedIn` destination and overall footer styling

**Files or Areas Affected**  
- `index.html`
- `about/index.html`
- `archive/index.html`
- `archive/2026/index.html`
- `archive/2026/week-05/index.html`
- `archive/2026/week-06/index.html`
- `archive/2026/week-07/index.html`
- `archive/2026/week-08/index.html`
- `archive/2026/week-09/index.html`
- `archive/2026/week-10/index.html`
- `archive/2026/week-11/index.html`
- `archive/2026/week-12/index.html`
- `archive/2026/week-13/index.html`
- `archive/2026/week-14/index.html`
- `archive/2026/week-15/index.html`
- `methodology/index.html`
- `docs/development-log.md`

**Design or Structural Decisions**  
The footer remains a single-line editorial note. The new text order reads more like publication metadata, and the vertical bar separates the follow link cleanly without adding visual weight.

**Mobile / Performance / Accessibility Notes**  
- No layout or behavior changes
- The footer remains lightweight and wraps naturally on smaller screens

**Follow-Up Note**  
Literal spaces around the separator did not render visibly in the browser because HTML collapses whitespace. The footer now uses a dedicated separator element with CSS margin so the spacing is actually visible and consistent.

### 2026-04-14 - Footer LinkedIn Follow Path Added

**Summary**  
Added a restrained publication-level LinkedIn follow link to the site-wide footer so readers can find the LinkedIn-hosted newsletter without adding navigation clutter.

**Reason for Change**  
The site needed a quiet global follow path for the publication itself, distinct from the author's personal links and without adding promotional weight to the main page layouts.

**What Changed**  
- Updated the footer text across all static pages to append `Â· Follow on LinkedIn`
- Pointed the new footer link to the LinkedIn-hosted Finding Critical Path newsletter home
- Added a minimal footer link rule so the inline link keeps the same calm footer treatment

**Files or Areas Affected**  
- `index.html`
- `about/index.html`
- `archive/index.html`
- `archive/2026/index.html`
- `archive/2026/week-05/index.html`
- `archive/2026/week-06/index.html`
- `archive/2026/week-07/index.html`
- `archive/2026/week-08/index.html`
- `archive/2026/week-09/index.html`
- `archive/2026/week-10/index.html`
- `archive/2026/week-11/index.html`
- `archive/2026/week-12/index.html`
- `archive/2026/week-13/index.html`
- `archive/2026/week-14/index.html`
- `archive/2026/week-15/index.html`
- `methodology/index.html`
- `assets/css/site.css`
- `docs/development-log.md`

**Design or Structural Decisions**  
The footer keeps its existing single-line editorial treatment. The LinkedIn path is presented as a quiet inline extension of the copyright note rather than as a social module or button.

**Mobile / Performance / Accessibility Notes**  
- The update preserves the existing footer layout and wraps naturally on smaller screens
- No scripts or dependencies were added
- The link remains clearly interactive while staying visually restrained

### 2026-04-14 - Homepage Secondary Action Removed

**Summary**  
Removed the `Read on LinkedIn` secondary action from the homepage featured-edition block so the page returns to a single, cleaner on-site reading path.

**Reason for Change**  
The homepage needed a more restrained action area, with less visual and navigational competition around the featured edition.

**What Changed**  
- Removed the `Read on LinkedIn` homepage action link
- Simplified the featured-edition action styling so it only supports the primary `Keep reading` text link
- Updated the site overview guidance to reflect the lighter single-link homepage treatment

**Files or Areas Affected**  
- `index.html`
- `assets/css/site.css`
- `docs/site-overview.md`
- `docs/development-log.md`

**Design or Structural Decisions**  
The homepage now keeps a single editorial read path for the featured edition, which better matches the site's minimal, publication-first presentation.

**Mobile / Performance / Accessibility Notes**  
- Slightly simpler markup and CSS
- No layout or behavior regressions expected

### 2026-04-14 - Homepage Featured Action Simplified

**Summary**  
Replaced the homepage featured-edition boxed button with a lighter two-line text action group and added a quieter secondary path to the LinkedIn-hosted publication.

**Reason for Change**  
The homepage needed to keep the featured edition action area calm, editorial, and publication-first while still offering readers a direct route to the LinkedIn-hosted version of the newsletter.

**What Changed**  
- Replaced the boxed `Keep Reading` CTA on the homepage with a grouped two-line text treatment
- Kept `Keep reading` as the primary on-site action to the featured edition
- Added `Read on LinkedIn` as a quieter secondary action beneath it
- Added minimal homepage-scoped CSS to preserve a restrained visual hierarchy without affecting button styles elsewhere

**Files or Areas Affected**  
- `index.html`
- `assets/css/site.css`
- `docs/site-overview.md`
- `docs/development-log.md`

**Design or Structural Decisions**  
The action area now behaves more like editorial navigation than promotion: the primary link keeps the accent color and stronger weight, while the LinkedIn path sits below in a quieter muted treatment. This preserves a clean homepage and gives the LinkedIn-hosted publication a clear but secondary presence.

**Mobile / Performance / Accessibility Notes**  
- The action links stay grouped in a simple vertical stack that remains readable on mobile
- No scripts or dependencies were added
- The change is HTML/CSS-only with no meaningful performance cost

## Entry Template

Copy and complete the template below for each meaningful update.

### [YYYY-MM-DD] - [Short Change Title]

**Summary**  
A short plain-language summary of what was changed.

**Reason for Change**  
Why this change was made. Focus on user value, site quality, maintainability, publication goals, or future flexibility.

**What Changed**  
- Item 1
- Item 2
- Item 3

**Files or Areas Affected**  
- `path/to/file`
- `path/to/file`
- Brief note if the change affected a page, component, template, styling system, content structure, or documentation

**Design or Structural Decisions**  
Describe any meaningful decisions that shaped the implementation. Note any tradeoffs that were considered.

**Mobile / Performance / Accessibility Notes**  
Record anything relevant to:
- mobile behavior
- load speed
- image handling
- readability
- accessibility
- responsive layout

**Risks / Watchouts**  
Call out anything a future teammate should be careful about.

**Follow-Up Opportunities**  
List any sensible next steps that were identified but not yet implemented.

---

## Log Entries

### 2026-04-14 - Site-wide Footer Copyright Update

**Summary**  
Replaced the existing footer label with the requested copyright line across the site's repeated footer markup.

**Reason for Change**  
The publication needed a minimal rights-reservation line that fits the existing restrained editorial footer without adding clutter.

**What Changed**  
- Updated the footer text in each static page that renders the site's standard footer
- Preserved the existing footer markup, spacing, typography hooks, and layout
- Avoided structural refactors because the current site uses repeated static footer markup rather than a shared component

**Files or Areas Affected**  
- `index.html`
- `archive/index.html`
- `archive/2026/index.html`
- `archive/2026/week-05/index.html`
- `archive/2026/week-06/index.html`
- `archive/2026/week-07/index.html`
- `archive/2026/week-08/index.html`
- `archive/2026/week-09/index.html`
- `archive/2026/week-10/index.html`
- `archive/2026/week-11/index.html`
- `archive/2026/week-12/index.html`
- `archive/2026/week-13/index.html`
- `archive/2026/week-14/index.html`
- `archive/2026/week-15/index.html`
- `about/index.html`
- `methodology/index.html`

**Design or Structural Decisions**  
This was implemented as a text-only change. Although the footer is not currently controlled by a shared global component, consolidating footer rendering would be a broader structural change and was not necessary for this request.

**Mobile / Performance / Accessibility Notes**  
No behavior or asset changes were introduced. The update preserves the existing semantic footer structure and CSS styling.

**Risks / Watchouts**  
Because footer markup is duplicated across static pages, future footer copy changes will need to be applied in more than one file unless the site is later templated.

**Follow-Up Opportunities**  
- If the site later adopts a shared include or generator step, consolidate the repeated footer markup at that time

### 2026-04-12 - Development Log Initialized

**Summary**  
Created the initial development log for the Finding Critical Path website project.

**Reason for Change**  
The project needs a durable written record of meaningful site changes so future teammates can understand how the site evolved and continue development without relying on Codex.

**What Changed**  
- Created `docs/development-log.md`
- Defined the purpose of the log
- Added a reusable entry template for future updates
- Established expectations for what kinds of changes should be documented

**Files or Areas Affected**  
- `docs/development-log.md`

**Design or Structural Decisions**  
The log was designed to be detailed enough for a future web designer or developer to understand both implementation history and decision-making context. It is intended to complement `docs/site-overview.md`, which explains the site as it currently exists.

**Mobile / Performance / Accessibility Notes**  
No direct user-facing site changes were made in this update.

**Risks / Watchouts**  
The log only adds value if it is kept current. Future contributors should update it after meaningful work rather than trying to reconstruct history later.

**Follow-Up Opportunities**  
- Add future entries as meaningful site changes are made
- Keep the level of detail consistent enough to support future handoff

### 2026-04-12 - Initial Site Structure Review

**Summary**  
Reviewed the current site implementation, content organization, routing, and styling foundation against the project guidance in `AGENTS.md`, `docs/site-overview.md`, and this development log. No structural changes were made to the site itself in this pass.

**Reason for Change**  
Before moving into design refinement or content-model improvements, the project needed a clear assessment of what is already working, what currently conflicts with the publication direction, and what structural tradeoffs should be considered without casually changing the existing foundation.

**What Changed**  
- Reviewed the current static site structure across the homepage, archive pages, about page, methodology page, issue pages, shared CSS, and markdown content files
- Assessed the current implementation against the publication goals: publication-first identity, credible editorial presentation, strong mobile behavior, restrained scope, and future expansion potential
- Identified strengths in the existing base infrastructure, including simple routing, lightweight delivery, shared styling, and a content/archive folder structure that is understandable and maintainable
- Identified inconsistencies with the documented direction, especially public placeholder content, the presence of a separate public Methodology page, incomplete issue metadata, missing edition graphics, and archive/edition patterns that do not yet match the desired publication experience
- Documented a broad-strokes recommendation for the next phase without changing architecture, deployment assumptions, or routing structure

**Files or Areas Affected**  
- `index.html`
- `archive/index.html`
- `archive/2026/index.html`
- `archive/2026/week-10/index.html`
- `archive/2026/week-05/index.html` through `archive/2026/week-13/index.html`
- `about/index.html`
- `methodology/index.html`
- `assets/css/site.css`
- `content/2026/*.md`
- `docs/development-log.md`

**Design or Structural Decisions**  
The current implementation already preserves an important project constraint: it is simple, static, and easy to deploy. That is a meaningful strength and should not be casually replaced.

The main architectural concern is not that the foundation is wrong, but that the content and page layer is currently duplicated across many hand-authored HTML files. That duplication is still manageable at the current size, but it will become harder to maintain as more editions, richer archive behavior, search, tags, or alternate editorial formats are added. This should be treated as a future decision point rather than an immediate rewrite trigger.

The review also surfaced a scope mismatch with the documented public structure. The guidance calls for public launch navigation of Home, Archive, and About only. The current public Methodology page and nav item create unnecessary top-level complexity and weaken the intended restrained launch shape, even though the methodology content itself is aligned and valuable.

Several current display choices also make the site feel more provisional than editorial:
- issue numbering is still prominent in archive listings
- multiple public pages contain placeholders
- the homepage frames the publication well but does not yet center the latest edition with a strong visual editorial preview
- edition pages do not yet use the intended split header with hero image, byline, share actions, or previous/next edition navigation
- the reference treatment does not yet match the intended â€œDive deeperâ€ editorial pattern

**Mobile / Performance / Accessibility Notes**  
The current static approach is favorable for performance and hosting simplicity.

The shared stylesheet already includes responsive layout shifts for major page sections and appears to treat smaller screens intentionally rather than as an afterthought. That said, the current archive presentation is still list-based rather than the intended tile-based browsing experience, and issue pages do not yet provide the stronger mobile-first editorial framing described in the project guidance.

Accessibility is partly supported through semantic sections and nav landmarks, but there are current gaps or likely follow-up needs:
- the logo image uses an empty `alt` value while functioning as part of the brand link
- placeholder content on public pages weakens clarity and trust
- edition graphics and corresponding alt text are not yet implemented even though the content model anticipates them

**Risks / Watchouts**  
- Public placeholder editions and placeholder metadata make the site feel unfinished, which directly conflicts with the projectâ€™s credibility goals
- Repeating header/nav/footer markup across many pages increases the chance of future inconsistency as the site evolves
- The current markdown content files are not obviously connected to the published HTML output, creating a risk of content drift between source material and live pages
- Public year/archive pages currently emphasize week labels and directory organization more than editorial identity, which could make the publication feel procedural rather than publication-first
- A future move toward search, tags, richer archive browsing, or alternate content types will be harder if content data continues to live in parallel hand-maintained HTML and markdown forms

**Follow-Up Opportunities**  
- Refine the existing homepage so the latest edition becomes the clear editorial focal point with image, date range, excerpt, and a subtle archive path
- Rework the public archive experience within the existing structure toward the documented tile layout, initial six-item view, and in-page filtering
- Consolidate methodology content into the About page structure described in the project guidance, then remove the extra public Methodology nav item when ready
- Bring edition pages into alignment with the documented format: split header, byline linked to About, hero image, Dive deeper section, share controls, and previous/next navigation
- Decide whether to keep the current static hand-authored pattern for the near term or introduce a lightweight content-generation step later to reduce duplication without disturbing deployment assumptions
- Tighten visible metadata so title and full date range lead the editorial identity, with week identifiers treated as secondary or internal where useful

### 2026-04-12 - Publication Alignment Pass 1

**Summary**  
Implemented the highest-value version 1 publication-alignment updates that improve public credibility without changing the projectâ€™s static structure or deployment assumptions.

**Reason for Change**  
The site needed a more credible public face before deeper archive and edition-page work. This pass focused on removing visible signs of incompleteness, simplifying the launch navigation, and making the homepage and About page feel more like a real publication.

**What Changed**  
- Simplified global navigation to `Home / Archive / About` across the homepage, archive pages, About page, methodology route, and published edition pages
- Refined the homepage into a latest-edition landing page with the publication tagline, tighter value framing, a proper latest-edition preview, and a quieter archive path
- Added a lightweight static SVG cover asset for the latest published edition so the homepage can present a polished hero image without changing infrastructure or adding dependencies
- Consolidated methodology content into the About page and rewrote About into three clear sections: Why it exists, Methodology, and Author bio
- Added a LinkedIn profile link in the author bio while keeping the author secondary to the publication
- Removed public placeholder issue listings from the archive and year archive so only published editions appear in public browsing paths
- Replaced unpublished issue placeholder pages with lightweight archive redirects so those routes no longer expose unfinished public content

**Files or Areas Affected**  
- `index.html`
- `archive/index.html`
- `archive/2026/index.html`
- `archive/2026/week-10/index.html`
- `archive/2026/week-05/index.html`
- `archive/2026/week-06/index.html`
- `archive/2026/week-07/index.html`
- `archive/2026/week-08/index.html`
- `archive/2026/week-09/index.html`
- `archive/2026/week-11/index.html`
- `archive/2026/week-12/index.html`
- `archive/2026/week-13/index.html`
- `about/index.html`
- `methodology/index.html`
- `assets/css/site.css`
- `assets/2026/week-10/W10Cover.svg`
- `docs/development-log.md`

**Design or Structural Decisions**  
This pass intentionally avoided major structural changes. The site remains a static HTML/CSS implementation with the same folder layout and routing model.

The methodology route was preserved for compatibility, but it now redirects readers into the About page so the public information architecture stays aligned with the documented launch scope.

Unpublished week folders were left in place to preserve the existing content structure, but their public-facing pages now redirect back into the year archive instead of displaying placeholder copy.

**Mobile / Performance / Accessibility Notes**  
- The new homepage cover image is an SVG to keep the asset lightweight and sharp on both desktop and mobile
- The updated homepage and About page continue using the shared responsive CSS system rather than introducing heavier layout logic
- Public-facing copy is now more direct and less cluttered, which improves scanning on smaller screens
- Redirect/fallback pages were kept lightweight so direct visits to older reserved routes do not create dead ends

**Risks / Watchouts**  
- The public archive now shows only the single published edition, which is more credible than placeholders but also makes the archive feel sparse until more finished editions are added
- The current content source still exists in both markdown and hand-authored HTML, so future content updates should continue watching for drift between source files and published pages
- The added LinkedIn link should be updated if a preferred public author URL or publication-specific LinkedIn destination should be used instead

**Follow-Up Opportunities**  
- Rework the archive into the intended tile-based browsing experience with image thumbnails, six-up initial presentation, and load-more behavior
- Bring the published edition template into closer alignment with the target editorial format, especially byline treatment, hero placement, Dive deeper styling, and previous/next navigation
- Decide whether unpublished week folders should remain as reserved routes or be handled differently once the publication schedule becomes clearer
- Consider a lightweight generation workflow later if maintaining parallel markdown and HTML starts to create avoidable friction

### 2026-04-12 - About Page Copy Update

**Summary**  
Updated the public About page to use the approved publication copy from `docs/about-page-copy.md` and tightened the author contact treatment.

**Reason for Change**  
The About page needed to reflect the approved editorial framing and author language while staying publication-first, credible, and aligned with the documented About-page structure.

**What Changed**  
- Replaced the existing About-page section copy with the approved text from `docs/about-page-copy.md`
- Preserved the required section order: Why it exists, Methodology, and Author bio
- Added polished LinkedIn and email links in the Author bio section
- Kept the Methodology content folded into About and left the separate methodology route as a redirect/fallback rather than a standalone public information page

**Files or Areas Affected**  
- `about/index.html`
- `assets/css/site.css`
- `docs/development-log.md`

**Design or Structural Decisions**  
This update intentionally stayed at the content-and-presentation layer. The page structure, routing model, and static deployment assumptions were preserved.

The contact treatment was kept minimal and text-first so the page remains restrained and publication-oriented rather than shifting toward a personal profile layout.

**Mobile / Performance / Accessibility Notes**  
- The About page continues to use the existing lightweight layout and shared responsive CSS
- Contact links were added as simple text links, which keeps the page fast and easy to scan on mobile
- No heavy media, dependencies, or interactive features were introduced

**Risks / Watchouts**  
- The updated author copy is stronger and more specific, so future revisions should keep the publication-first balance intact rather than allowing the page to drift into a personality-first presentation
- The separate methodology route still exists as a redirect for compatibility; if routing assumptions change later, that redirect behavior should be revisited deliberately

**Follow-Up Opportunities**  
- Add a small edition-page byline link to the About bio section when the edition template is updated
- Refine the published edition page toward the target editorial format, especially hero placement, byline treatment, and final Dive deeper styling
- Rework the archive into the intended tile-based browsing experience once more published editions are ready

### 2026-04-12 - Week 14 Integrated

**Summary**  
Integrated the completed Week 14 markdown into the site as a published edition and moved it into the active homepage and archive flow.

**Reason for Change**  
Week 14 needed to be available in the live site content flow using the existing static structure, with its edition page, graphic asset, and archive ordering all aligned.

**What Changed**  
- Added a published Week 14 edition page at `archive/2026/week-14/index.html`
- Linked the edition page to the existing Week 14 cover image in `assets/2026/week-14/w14cover.png`
- Promoted Week 14 to the homepage as the latest edition
- Added Week 14 to the archive listings ahead of Week 10 so published editions appear in the correct order
- Added small supporting styles for edition hero images and reference titles

**Files or Areas Affected**  
- `archive/2026/week-14/index.html`
- `index.html`
- `archive/index.html`
- `archive/2026/index.html`
- `assets/css/site.css`
- `docs/development-log.md`

**Design or Structural Decisions**  
This update preserved the current folder layout, static HTML workflow, and deployment assumptions. Week 14 was integrated by following the same archive path conventions already used in the project.

Because the current edition template is still transitional, Week 14 was added within the existing page pattern rather than triggering a broader edition-template redesign.

**Mobile / Performance / Accessibility Notes**  
- The edition uses the existing graphic asset directly instead of introducing a heavier image workflow
- The Week 14 cover image is rendered within the article flow using lightweight shared CSS
- Alt text from the markdown file was carried into the edition page for the hero image

**Risks / Watchouts**  
- The project still relies on manually keeping markdown content and published HTML in sync, so future edition updates should continue watching for drift
- Date formatting now includes `March 29-April 4, 2026`; if the site later standardizes punctuation styling more strictly, earlier and later editions may need a consistency pass

**Follow-Up Opportunities**  
- Add next/previous edition navigation across published issues once more editions are live
- Bring published editions into the target split-header format with byline treatment and stronger Dive deeper styling
- Rework the archive into the intended tile-based layout once the number of published editions justifies it

### 2026-04-12 - Homepage Lead-Edition Redesign

**Summary**  
Redesigned the homepage so the latest edition becomes the main visual and editorial focus rather than appearing as a secondary panel beside a dominant publication intro.

**Reason for Change**  
The homepage needed to feel more like a publication landing page centered on the newest edition, with the publication framing supporting the lead story rather than competing with it.

**What Changed**  
- Reworked the homepage layout so the publication title, tagline, and framing appear as a compact introduction rather than the dominant hero
- Promoted the latest edition into a wide featured-edition layout with the cover image, title, date, excerpt, and primary reading path carrying most of the page's visual weight
- Reduced the archive prompt to a quieter supporting line below the featured edition
- Added focused homepage styles to support the new editorial hierarchy across desktop and mobile

**Files or Areas Affected**  
- `index.html`
- `assets/css/site.css`
- `docs/development-log.md`

**Design or Structural Decisions**  
This pass preserved the siteâ€™s static structure and routing model. The redesign stays within the existing homepage file and shared stylesheet rather than introducing new templates or dependencies.

The main hierarchy decision was to treat the latest edition as a lead story. The publication identity now frames the page briefly at the top, while the edition package occupies the central visual space and carries the primary call to action.

**Mobile / Performance / Accessibility Notes**  
- The homepage still uses the existing static image asset and shared CSS, keeping load behavior lightweight
- The featured edition appears first and remains dominant on mobile through a simple single-column collapse
- No new scripts, libraries, or heavy media behaviors were introduced

**Risks / Watchouts**  
- The homepage now depends more heavily on the latest edition image quality, so future covers will have a larger impact on perceived polish
- If later homepage features are added, they should be kept restrained so the lead-edition hierarchy does not erode back into a busier landing page

**Follow-Up Opportunities**  
- Bring other published edition pages up to the same visual standard as the latest featured edition
- Rework the archive into the intended tile layout so the visual language between the homepage lead story and archive browsing feels more cohesive
- Add a byline link into edition pages once the edition template is refined further

### 2026-04-12 - Homepage Framing Compression

**Summary**  
Added a homepage-only framing behavior that gives the publication identity more presence on initial load, then quietly compresses that framing after scrolling so the featured edition becomes even more content-forward.

**Reason for Change**  
The homepage needed a stronger first-impression publication feel without letting the framing continue to compete with the latest edition once a reader begins engaging with the page.

**What Changed**  
- Added a homepage-only body class and a small inline scroll listener to toggle a compact scrolled state
- Increased the initial prominence of the homepage framing through spacing and typography adjustments
- Added a compressed scrolled state that reduces the framing block's scale and spacing while keeping the featured edition prominent
- Kept the behavior limited to the homepage so Archive, About, and edition pages retain their existing header behavior

**Files or Areas Affected**  
- `index.html`
- `assets/css/site.css`
- `docs/development-log.md`

**Design or Structural Decisions**  
The implementation uses CSS for the visual behavior and a very small amount of homepage-only JavaScript to switch states based on scroll position. This keeps the effect lightweight and avoids introducing a heavier animation or dependency layer.

The transition was designed to affect the homepage framing block rather than site-wide navigation so the publication identity feels more intentional on arrival while the latest edition remains the page's central editorial object.

**Mobile / Performance / Accessibility Notes**  
- The behavior is homepage-only and uses a single passive scroll listener with a simple class toggle
- The visual change is restrained and spacing-based rather than animation-heavy
- Mobile gets the same behavior with smaller scale shifts so the page remains calm and readable on narrow screens

**Risks / Watchouts**  
- The perceived quality of the effect depends on the transition feeling subtle; future homepage additions should avoid stacking more motion onto this area
- If the homepage content structure changes substantially later, the scroll threshold may need minor tuning

**Follow-Up Opportunities**  
- Tune the scrolled-state threshold after browser review if the compression feels too early or too late
- Refine the edition template so the homepage featured story and edition-page opening share a stronger visual relationship
- Continue the archive redesign when more published editions are live

### 2026-04-12 - Homepage Excerpt Expansion

**Summary**  
Adjusted the homepage featured-edition layout so more of the latest article is directly visible and the excerpt reads across the full page width instead of being confined to a half-page text column.

**Reason for Change**  
The homepage needed to preview more of the newest edition immediately and let the editorial text feel more like a lead-story read rather than a short teaser beside the image.

**What Changed**  
- Reworked the homepage featured-edition block so the image leads and the text sits below at full content width
- Expanded the visible Week 14 excerpt to roughly 150 words using the published article text
- Updated homepage styling so the featured edition copy is no longer constrained to a narrow side column

**Files or Areas Affected**  
- `index.html`
- `assets/css/site.css`
- `docs/development-log.md`

**Design or Structural Decisions**  
This change stays within the existing static homepage structure and keeps the featured edition as the homepage focal point. The image still establishes the cover-like presentation, but the text now gets more editorial breathing room underneath.

**Mobile / Performance / Accessibility Notes**  
- The change uses existing markup and shared CSS only
- The homepage remains lightweight and mobile-friendly because the layout simply reduces column constraints rather than adding interactive behavior
- More of the article is visible without requiring an extra click, which improves scan value on both desktop and mobile

**Risks / Watchouts**  
- Showing more text on the homepage increases vertical length slightly, so future homepage additions should stay restrained
- If future excerpts are much longer or shorter, the homepage may need a small consistency pass to keep the lead-story block balanced

**Follow-Up Opportunities**  
- Standardize how much excerpt text appears for future published editions
- Align the archive summaries and homepage excerpt style once more editions are live

### 2026-04-12 - Homepage Hero Split Restored

**Summary**  
Adjusted the homepage featured-edition layout so the top of the lead story returns to a balanced half-text / half-image split while keeping the longer excerpt below at full width.

**Reason for Change**  
The expanded article preview was useful, but the homepage still needed the cover image and edition metadata to share the top of the page in a more editorial, cover-like composition.

**What Changed**  
- Restored the featured edition's top section to a two-column split with the Latest edition label, title, and date on one side and the hero image on the other
- Kept the longer article preview text below that split so readers still see more of the latest piece immediately
- Updated homepage styles so the split collapses cleanly back to a single column on smaller screens

**Files or Areas Affected**  
- `index.html`
- `assets/css/site.css`
- `docs/development-log.md`

**Design or Structural Decisions**  
This adjustment keeps the homepage publication-first and editorial by separating the lead-story header from the article preview body. The top of the page now behaves more like a featured cover spread, while the excerpt remains a readable follow-on block.

**Mobile / Performance / Accessibility Notes**  
- The split layout uses CSS only and preserves the existing lightweight homepage behavior
- On smaller screens the layout stacks naturally so the image and metadata remain readable without forcing a cramped side-by-side arrangement

**Risks / Watchouts**  
- Future edition images may vary in crop quality, so the half-page treatment will continue to depend on strong source art
- If future homepage excerpts grow longer, spacing may need another small pass to keep the lead-story block feeling balanced

**Follow-Up Opportunities**  
- Standardize homepage lead-story crops and text lengths for future editions
- Continue refining the featured-edition visual language so it aligns even more closely with the final edition-page template

### 2026-04-12 - Homepage Logo Framing Added

**Summary**  
Added a larger homepage logo to the framing section and tied it into the existing homepage-only compression behavior.

**Reason for Change**  
The homepage framing needed a stronger visual identity on arrival, while still compressing gracefully so the featured edition remains the primary focus once readers begin scrolling.

**What Changed**  
- Added a larger logo to the homepage framing block above the tagline and title
- Updated homepage-only CSS so the logo scales down along with the rest of the framing in the scrolled state
- Kept the change limited to the homepage so Archive, About, and edition pages retain their normal presentation

**Files or Areas Affected**  
- `index.html`
- `assets/css/site.css`
- `docs/development-log.md`

**Design or Structural Decisions**  
The logo was added only to the homepage intro rather than the global header so it contributes to the landing-page framing without changing site-wide navigation behavior.

**Mobile / Performance / Accessibility Notes**  
- The homepage uses the existing local logo asset with CSS-only size transitions
- The logo scales down on mobile as well, preserving the same calm compression behavior without adding layout complexity

**Risks / Watchouts**  
- The homepage framing now has a bit more visual identity, so future additions should continue to keep that section restrained enough not to compete with the lead edition

**Follow-Up Opportunities**  
- Review the balance between logo size, title size, and featured-edition prominence after browser testing

### 2026-04-12 - Homepage Logo Alignment Refined

**Summary**  
Adjusted the homepage framing so the large intro logo sits to the left of the framing text and scales to match the full vertical span of the text block.

**Reason for Change**  
The homepage framing needed the logo to feel more integrated with the editorial identity rather than stacked above the text, while preserving the homepage-only compression behavior.

**What Changed**  
- Moved the homepage intro logo to the left of the framing text using a two-column intro layout
- Sized the logo to fill the full vertical space of the intro text block instead of appearing as a separate icon above it
- Preserved the scroll-compression behavior so the logo still reduces with the rest of the framing

**Files or Areas Affected**  
- `index.html`
- `assets/css/site.css`
- `docs/development-log.md`

**Design or Structural Decisions**  
This refinement keeps the homepage framing more editorial by making the logo and framing copy read as a single composition rather than as stacked elements.

**Mobile / Performance / Accessibility Notes**  
- The adjustment uses CSS layout changes only and keeps the same lightweight homepage behavior
- Mobile retains the left-logo layout at a reduced scale so the framing remains compact and readable

**Risks / Watchouts**  
- Because the logo now fills the framing height more aggressively, its perceived size will depend on the final balance of title and framing copy length

**Follow-Up Opportunities**  
- Review whether the left-logo proportion feels right relative to the title after browser testing

### 2026-04-12 - Homepage Header Deferred

**Summary**  
Adjusted the homepage-only header behavior so the standard compact header is absent on initial load and appears only after the reader scrolls.

**Reason for Change**  
The homepage was showing duplicate publication branding on arrival because the normal header and the homepage framing were both visible at once. The arrival state needed to belong to the homepage framing alone.

**What Changed**  
- Hid the standard header in the homepage's initial state so it no longer competes with the homepage framing on first view
- Revealed the compact sticky header only after the existing homepage scroll threshold is crossed
- Kept the behavior homepage-only so Archive, About, and edition pages continue showing the standard header immediately

**Files or Areas Affected**  
- `assets/css/site.css`
- `docs/development-log.md`

**Design or Structural Decisions**  
This change reuses the existing homepage scroll-state hook rather than introducing a second behavior system. The compact header remains the persistent orientation layer after scroll, but it is removed from the landing view so the homepage framing can own the first impression.

**Mobile / Performance / Accessibility Notes**  
- The behavior remains lightweight because it is driven by existing homepage scroll-state classes and CSS transitions
- The hidden header is also non-interactive on initial load, preventing accidental focus or tap targets before it appears
- Other pages retain their standard immediate header behavior

**Risks / Watchouts**  
- The reveal timing is tied to the same homepage scroll threshold as the framing compression, so future tuning may need to consider both effects together

**Follow-Up Opportunities**  
- Review whether the header reveal feels timed correctly relative to the framing compression on desktop and mobile

### 2026-04-12 - Homepage Top Offset Reduced

**Summary**  
Reduced the homepage-only top offset above the framing so the landing state starts higher on the page and feels less like space reserved for the hidden compact header.

**Reason for Change**  
The homepage still had too much empty space above the framing on initial load. The issue was primarily the homepage lead section's own top padding, which remained too generous even after the compact header was hidden on arrival.

**What Changed**  
- Reduced the homepage lead section's initial top padding significantly on desktop and mobile
- Also reduced the homepage scrolled-state top padding so the compact header can appear without creating an awkward spacing jump
- Kept the adjustment limited to the homepage so other pages retain their normal header/layout behavior

**Files or Areas Affected**  
- `assets/css/site.css`
- `docs/development-log.md`

**Design or Structural Decisions**  
This was treated as a homepage pre-scroll spacing issue rather than a site-wide header problem. The fix stays entirely in homepage-specific CSS and works with the existing hidden-header / revealed-header behavior.

**Mobile / Performance / Accessibility Notes**  
- No new scripts or dependencies were introduced
- Desktop and mobile both received tuned spacing values so the framing starts higher without feeling cramped

**Risks / Watchouts**  
- If the homepage framing content changes length again, the top padding may need another small calibration pass

**Follow-Up Opportunities**  
- Review the landing-state top spacing in-browser to confirm the initial and scrolled states still feel calm and intentional

### 2026-04-12 - Homepage Transition Divider Added

**Summary**  
Added a subtle divider treatment between the homepage framing and the featured edition to clarify where the lead story begins without introducing a harsh section break.

**Reason for Change**  
The homepage needed a quieter, more intentional transition between the publication framing and the featured latest edition. A restrained structural cue helps the lead story feel deliberately introduced rather than simply following the framing block.

**What Changed**  
- Added a thin homepage-only horizontal divider between the framing block and the featured edition
- Reduced the spacing below the framing block and tuned the spacing around the divider so the transition feels connected rather than separated
- Adjusted the divider spacing slightly in the scrolled state and on mobile so the transition remains calm across viewports

**Files or Areas Affected**  
- `index.html`
- `assets/css/site.css`
- `docs/development-log.md`

**Design or Structural Decisions**  
The divider uses a very light horizontal rule with softened ends so it reads as an editorial structural cue rather than a decorative line. It is intentionally quiet and homepage-specific.

**Mobile / Performance / Accessibility Notes**  
- The divider is CSS-only and marked as decorative with `aria-hidden`
- Mobile spacing was tuned separately so the divider supports the composition without feeling cramped

**Risks / Watchouts**  
- If the homepage framing or featured edition spacing changes again later, the divider margins may need a small follow-up adjustment to keep the transition balanced

**Follow-Up Opportunities**  
- Review whether the divider feels more helpful than visible after browser testing on both desktop and mobile

### 2026-04-12 - Homepage Framing Tone Test

**Summary**  
Added a very subtle tonal background treatment behind the homepage framing area to test whether it better unifies the landing state and the later compact-header transition.

**Reason for Change**  
The homepage framing was structurally clear, but it still benefited from a quiet tonal cue that could gather the intro area together without competing with the featured edition or turning the top of the page into a hero band.

**What Changed**  
- Added a faint homepage-only tonal wash behind the framing area using a lightweight pseudo-element
- Kept the tonal treatment shallow and softly faded so it remains a structural cue rather than a visible design feature
- Tuned the tonal area so it compresses slightly along with the homepage framing in the scrolled state

**Files or Areas Affected**  
- `assets/css/site.css`
- `docs/development-log.md`

**Design or Structural Decisions**  
The tonal treatment was kept intentionally close to the existing page neutrals. It is not a color block or hero background; it is a barely perceptible surface shift that helps the framing feel more anchored to the arrival state.

**Mobile / Performance / Accessibility Notes**  
- The effect is CSS-only and uses no additional assets or scripts
- The tonal treatment remains behind content and does not affect interaction behavior
- Mobile gets a slightly shallower version so the top of the page stays calm and uncluttered

**Risks / Watchouts**  
- Because the effect is intentionally subtle, its value may depend on the display and lighting conditions where it is reviewed
- If future homepage changes add more visual structure at the top, this tonal wash may become unnecessary or should be reduced further

**Follow-Up Opportunities**  
- Compare the homepage with and without the tonal treatment in-browser to decide whether the unifying effect is worth keeping

### 2026-04-12 - Homepage Tone Zone Unified

**Summary**  
Extended the homepage tonal treatment so the full area above the divider, including the compact header when it appears, now reads as one unified framing layer.

**Reason for Change**  
The initial tonal treatment helped the homepage framing, but the top of the page still benefited from feeling more clearly like a single publication zone rather than a framing block floating above the featured edition. Extending the tone upward and into the revealed header creates a more unified arrival experience.

**What Changed**  
- Extended the homepage-only tonal treatment across the full top zone above the divider
- Tuned the compact homepage header background and border so it visually belongs to that same tonal layer when revealed after scroll
- Kept the divider as the transition point into the featured edition below

**Files or Areas Affected**  
- `assets/css/site.css`
- `docs/development-log.md`

**Design or Structural Decisions**  
The tonal treatment remains intentionally subtle and neutral. It is now applied as a single quiet surface across the homepage top zone rather than as a shorter wash behind only the framing copy.

**Mobile / Performance / Accessibility Notes**  
- The change remains CSS-only and homepage-only
- No assets, dependencies, or new scripting were introduced
- Mobile receives the same unified tonal zone without adding visual heaviness

**Risks / Watchouts**  
- If the tone is pushed further later, the homepage top could start to feel like a banner rather than a structural editorial layer

**Follow-Up Opportunities**  
- Review whether the top-zone unity now feels stronger without making the homepage less airy or less publication-like

### 2026-04-12 - Homepage Tone Zone Trimmed

**Summary**  
Trimmed the homepage tonal treatment so it stays in the upper framing/header zone and no longer extends into the featured article section.

**Reason for Change**  
The unified gray tone was helpful for the top framing layer, but it reached too far down the page and began affecting the article area, which should remain on the normal page background.

**What Changed**  
- Limited the height of the homepage-only tonal background so it ends above the featured edition content block
- Tuned both desktop and mobile values, including the scrolled state, so the gray remains attached to the framing zone only

**Files or Areas Affected**  
- `assets/css/site.css`
- `docs/development-log.md`

**Design or Structural Decisions**  
This refinement keeps the tonal treatment as a framing device rather than letting it become part of the article presentation.

**Mobile / Performance / Accessibility Notes**  
- CSS-only adjustment with no change to performance or behavior

**Risks / Watchouts**  
- If the framing block grows taller later, the trimmed tonal height may need recalibration

**Follow-Up Opportunities**  
- Review the divider boundary in-browser to confirm the tonal zone now stops in the right place on both desktop and mobile

### 2026-04-12 - Homepage Tone Zone Full-Bleed

**Summary**  
Adjusted the homepage tonal treatment so it extends fully across the viewport like the header background while still remaining confined to the upper framing zone.

**Reason for Change**  
The trimmed tonal zone was stopping in the right vertical place, but it was still behaving like an in-content block rather than a full-width framing layer. The homepage top needed the same full-bleed behavior as the header.

**What Changed**  
- Made the homepage tonal background full-bleed across the viewport instead of constrained to the centered content width
- Kept the tonal zone limited vertically so it still stops above the featured article section

**Files or Areas Affected**  
- `assets/css/site.css`
- `docs/development-log.md`

**Design or Structural Decisions**  
This keeps the tonal zone acting like a structural page layer instead of a content card background, which better matches the header behavior and strengthens the unified top-zone effect.

**Mobile / Performance / Accessibility Notes**  
- CSS-only refinement with no behavior or performance impact

**Risks / Watchouts**  
- If the homepage width system changes later, the full-bleed positioning should be rechecked to ensure it still aligns correctly

**Follow-Up Opportunities**  
- Review whether the full-bleed tone and the header now feel like the same layer at first glance

### 2026-04-12 - Homepage Header Space Removed From Landing State

**Summary**  
Moved the homepage-only compact header out of normal document flow so the tonal framing zone can begin flush with the top of the page.

**Reason for Change**  
The hidden homepage header was still reserving vertical space before it appeared, which left an uncovered strip above the homepage framing and made the tonal zone feel detached from the top edge.

**What Changed**  
- Switched the homepage-only header from in-flow sticky behavior to a fixed overlay layer
- Kept the existing reveal behavior after scroll so the compact header still returns as the persistent navigation/orientation layer
- Let the homepage tonal framing begin at the true top of the page instead of below reserved header space

**Files or Areas Affected**  
- `assets/css/site.css`
- `docs/development-log.md`

**Design or Structural Decisions**  
This keeps the homepage landing state owned by the publication framing while preserving the standard compact header behavior once the reader begins scrolling.

**Mobile / Performance / Accessibility Notes**  
- CSS-only refinement with no dependency or routing impact

**Risks / Watchouts**  
- The fixed homepage header should be checked in-browser to confirm the reveal still feels smooth and does not overlap awkwardly with the framing content

**Follow-Up Opportunities**  
- Review whether the tonal zone now reaches the page edge in the intended way on both desktop and mobile

### 2026-04-12 - Homepage Tone Extended To Divider

**Summary**  
Extended the homepage tonal layer downward so it reaches the divider line at the bottom of the framing zone.

**Reason for Change**  
After the full-bleed/top-edge fixes, the gray framing layer was still ending slightly too early and stopping short of the divider, which weakened the sense of the entire upper zone reading as one unified publication layer.

**What Changed**  
- Increased the homepage-only tonal overlay height in the initial state so it carries all the way to the divider
- Tuned the scrolled-state and mobile overlay heights to preserve the same relationship at smaller sizes and after the compact header appears

**Files or Areas Affected**  
- `assets/css/site.css`
- `docs/development-log.md`

**Design or Structural Decisions**  
This keeps the divider as the clean transition into the featured edition while making the full area above it feel intentionally unified.

**Mobile / Performance / Accessibility Notes**  
- CSS-only adjustment with no effect on performance or interaction behavior

**Risks / Watchouts**  
- If the homepage framing content height changes again, the overlay height may need another small recalibration

**Follow-Up Opportunities**  
- Review in-browser whether the gray now reaches the divider precisely without appearing to tint the article section

### 2026-04-12 - Homepage Tone Divider Gap Closed

**Summary**  
Adjusted the homepage tonal overlay again to close the last visible gap above the divider line.

**Reason for Change**  
The prior height increase improved the boundary, but a thin strip of the normal page background was still visible between the tonal framing layer and the divider.

**What Changed**  
- Increased the homepage-only tonal overlay height slightly in desktop and mobile states
- Tuned the scrolled-state values as well so the gray still meets the divider after the compact header appears

**Files or Areas Affected**  
- `assets/css/site.css`
- `docs/development-log.md`

**Design or Structural Decisions**  
This keeps the top framing zone reading as one continuous layer all the way to the divider without changing the featured article section below.

**Mobile / Performance / Accessibility Notes**  
- CSS-only refinement with no effect on load speed or behavior

**Risks / Watchouts**  
- If the framing layout changes materially later, the overlay may need another small height adjustment

**Follow-Up Opportunities**  
- Confirm the divider now sits directly on the tonal zone on both desktop and mobile

### 2026-04-12 - Homepage Tone Slightly Overshot To Meet Divider

**Summary**  
Extended the homepage tonal overlay a little further so it slightly overshoots into the divider boundary and removes the last visible strip of page background.

**Reason for Change**  
Even after the previous adjustment, a narrow pale strip was still visible above the divider in-browser, so the tonal layer needed a small buffer rather than an exact edge match.

**What Changed**  
- Increased the homepage-only tonal overlay heights again on desktop and mobile
- Tuned the scrolled-state values so the same edge behavior holds after the compact header appears

**Files or Areas Affected**  
- `assets/css/site.css`
- `docs/development-log.md`

**Design or Structural Decisions**  
Allowing a slight overshoot is more reliable than trying to make the tonal layer stop exactly at the divider, especially as rendering varies slightly across viewports.

**Mobile / Performance / Accessibility Notes**  
- CSS-only refinement with no change to interaction behavior or load performance

**Risks / Watchouts**  
- If pushed too far, the gray could begin to tint the edition area below the divider, so the boundary should be checked visually

**Follow-Up Opportunities**  
- Recheck the divider edge on desktop and mobile to confirm the tone now meets it cleanly without affecting the article section

### 2026-04-12 - Header Surface Unified Across Site

**Summary**  
Standardized the compact header surface so the header looks consistent across the homepage, archive, About, and edition pages.

**Reason for Change**  
The site was already using the same header markup everywhere, but the homepageâ€™s revealed compact header and the standard header on other pages were using slightly different surface tones and border treatments, which made the navigation feel less cohesive than it should.

**What Changed**  
- Updated the default site header surface to match the compact header treatment used on the homepage after scroll
- Kept the homepage-only hidden-on-arrival behavior intact so the landing framing still owns the first impression

**Files or Areas Affected**  
- `assets/css/site.css`
- `docs/development-log.md`

**Design or Structural Decisions**  
This preserves the homepageâ€™s special arrival experience while making the persistent navigation layer feel like the same publication system everywhere else on the site.

**Mobile / Performance / Accessibility Notes**  
- CSS-only update with no dependency, routing, or interaction changes

**Risks / Watchouts**  
- The slightly cooler header surface should be checked on archive and edition pages to make sure it still feels calm and not too heavy

**Follow-Up Opportunities**  
- Review whether the header now feels like one consistent publication layer across page types

### 2026-04-12 - About Page Composition Rebalanced

**Summary**  
Refined the About page layout so the content sits in a more centered, balanced composition while keeping the text itself left-aligned and editorial.

**Reason for Change**  
The About page content was reading as too narrow and left-weighted, which left excess empty space on the right and made the page feel less intentional than the rest of the publication.

**What Changed**  
- Added an About-page-specific inner shell to center the intro and body content more deliberately within the page
- Widened the About content measure modestly on desktop while keeping a readable editorial line length
- Increased spacing between sections and tuned the intro spacing so the page rhythm feels calmer and more intentional
- Preserved left-aligned text and the existing static structure

**Files or Areas Affected**  
- `about/index.html`
- `assets/css/site.css`
- `docs/development-log.md`

**Design or Structural Decisions**  
This keeps the About page publication-first and restrained while giving it a stronger page composition that better matches the siteâ€™s overall level of polish.

**Mobile / Performance / Accessibility Notes**  
- Lightweight HTML/CSS-only refinement
- Mobile behavior keeps the layout at full width with tightened spacing for readability

**Risks / Watchouts**  
- The wider desktop measure should be checked to confirm it still feels comfortably readable for long paragraphs

**Follow-Up Opportunities**  
- Review whether the About page now feels more centered and intentional without becoming too wide or formal

### 2026-04-12 - About Page Reading Measure Tightened

**Summary**  
Refined the About page reading width so the centered composition remains intact while the body text feels slightly more editorial and controlled.

**Reason for Change**  
The broader About-page layout direction was working well, but the body text measure had become just a little too wide for the intended reading feel.

**What Changed**  
- Narrowed the About intro measure slightly
- Reduced the maximum width of the About section stack while preserving the centered page composition and left-aligned text

**Files or Areas Affected**  
- `assets/css/site.css`
- `docs/development-log.md`

**Design or Structural Decisions**  
This keeps the stronger centered composition from the prior pass while pulling the reading width back toward a more polished editorial measure.

**Mobile / Performance / Accessibility Notes**  
- CSS-only refinement with no change to infrastructure or behavior
- Mobile layout remains full-width within the existing responsive page padding

**Risks / Watchouts**  
- The narrower measure should be checked to make sure the page still feels balanced rather than reverting toward the earlier left-heavy impression

**Follow-Up Opportunities**  
- Review whether the current About-page width now feels like the right middle ground between spacious composition and comfortable reading

### 2026-04-12 - Edition Reading Flow Restored

**Summary**  
Corrected the published edition pages so they return to a calmer longform reading experience, with `Dive deeper` at the end of the article and no visible section headings interrupting the body.

**Reason for Change**  
The side-positioned source box and visible in-body section labels were making the editions feel more segmented and utility-oriented than a polished publication piece should.

**What Changed**  
- Moved `Dive deeper` from a side column into the end of each published article as a normal closing section
- Simplified the edition layout to a centered single-column reading flow
- Removed visible body section headings from the published edition text and folded the flow back into continuous prose
- Preserved in-text reference numbers and the closing source list format

**Files or Areas Affected**  
- `archive/2026/week-10/index.html`
- `archive/2026/week-14/index.html`
- `assets/css/site.css`
- `docs/development-log.md`

**Design or Structural Decisions**  
This keeps the edition pages aligned with the publication goal of calm, uninterrupted longform reading while preserving the current static site structure.

**Mobile / Performance / Accessibility Notes**  
- HTML/CSS-only refinement with no dependency or routing impact
- A single-column article flow improves continuity on both desktop and mobile

**Risks / Watchouts**  
- Future editions should follow the same pattern so the site does not drift back into visibly segmented article layouts

**Follow-Up Opportunities**  
- Review whether the `Dive deeper` spacing and pager placement feel right before moving into broader edition-page refinement

### 2026-04-12 - Edition Header And Reader Refined

**Summary**  
Refined the published edition pages so they now open with a homepage-related editorial split header, then transition into a calmer full-article reading experience with closing source, share, and navigation sections.

**Reason for Change**  
The edition pages needed to feel like a natural continuation of the homepageâ€™s publication language rather than a separate template, while still prioritizing reading once the article begins.

**What Changed**  
- Rebuilt the edition opening around a split header with edition label, large title, date, byline, and hero image
- Added a subtle transition rule between the editorial header and the article body
- Kept the article body in a centered reading column beneath the larger opening frame
- Restyled `Dive deeper` as a calmer end section rather than a boxed utility panel
- Added edition-page share controls for copy link, LinkedIn, and email
- Kept bottom navigation simple with archive and previous/next links
- Corrected visible encoding artifacts in the week 10 page and cover asset

**Files or Areas Affected**  
- `archive/2026/week-10/index.html`
- `archive/2026/week-14/index.html`
- `assets/css/site.css`
- `assets/2026/week-10/W10Cover.svg`
- `docs/development-log.md`

**Design or Structural Decisions**  
This pass intentionally borrows the homepageâ€™s split editorial rhythm for the edition opening, but hands off quickly into a quieter reading column so the page does not feel like a duplicate homepage hero.

**Mobile / Performance / Accessibility Notes**  
- Lightweight static HTML/CSS with a very small inline share script
- Mobile should stack the edition header naturally once responsive rules are applied
- Share controls rely on the current page URL in the browser, which preserves deployment flexibility

**Risks / Watchouts**  
- The new issue header classes should be reviewed on smaller screens to ensure the image, title, and byline hierarchy remain balanced

**Follow-Up Opportunities**  
- Review whether the edition opening now feels closely enough related to the homepage before refining body typography or pager styling further

### 2026-04-12 - Dive Deeper Typography Rebalanced

**Summary**  
Adjusted the `Dive deeper` typography so it now uses a more editorial hybrid treatment instead of reading too uniformly like interface copy.

**Reason for Change**  
The full section had shifted too far toward sans-serif utility styling, which made the references feel more like a UI component than a curated editorial source section.

**What Changed**  
- Kept the `Dive deeper` section label in sans-serif
- Set source titles to a deliberate sans-serif treatment for scanability
- Shifted the explanatory source summaries back to serif body typography with calmer line height and normal tracking
- Kept source/action links in sans-serif and gave them a little space below the summary copy

**Files or Areas Affected**  
- `assets/css/site.css`
- `docs/development-log.md`

**Design or Structural Decisions**  
This creates a clearer division of roles inside the section: labels and titles scan like editorial metadata, while the summary text reads more like a short continuation of the publication voice.

**Mobile / Performance / Accessibility Notes**  
- CSS-only refinement with no structural or behavior changes

**Risks / Watchouts**  
- The title styling should be checked to ensure it still feels restrained and not too loud against the calmer serif summaries

**Follow-Up Opportunities**  
- Review whether the `Dive deeper` section now feels enough like an editorial reference list before refining share/pager typography

### 2026-04-12 - Dive Deeper Link Treatment Simplified

**Summary**  
Simplified the `Dive deeper` links so each source title is now the hyperlink and the separate `Source` line has been removed.

**Reason for Change**  
The extra `Source` label added clutter and made the section feel more mechanical than a curated editorial reading list should.

**What Changed**  
- Converted each published `Dive deeper` source title into the hyperlink
- Removed the separate `Source` line under each item
- Added hover/focus styling to the linked source titles so clickability remains clear without making the section feel like a UI list

**Files or Areas Affected**  
- `archive/2026/week-14/index.html`
- `assets/css/site.css`
- `docs/development-log.md`

**Design or Structural Decisions**  
This keeps the section cleaner and more editorial while preserving scanability and clear interaction affordances.

**Mobile / Performance / Accessibility Notes**  
- Lightweight HTML/CSS-only refinement
- Hover/focus states remain explicit for linked titles on desktop and keyboard navigation

**Risks / Watchouts**  
- The linked title treatment should be checked to make sure it feels clearly interactive without becoming too visually assertive

**Follow-Up Opportunities**  
- Review whether the simplified title-link pattern should become the standard for future edition source lists

### 2026-04-13 - Edition Ending Utility Consolidated

**Summary**  
Consolidated the published edition endings into one quieter utility band so the pages now hand off more cleanly from `Dive deeper` into the site footer.

**Reason for Change**  
The separate share row, archive/previous-next row, and global footer were creating a stacked â€œtriple footerâ€ effect that made the article ending feel more segmented than editorial.

**What Changed**  
- Removed the standalone `Share` band from published edition pages
- Merged archive access, previous/next edition navigation, and share actions into one consolidated article-end utility band directly below `Dive deeper`
- Simplified the closing treatment so the links can read clearly without extra subhead labels
- Updated the shared edition CSS so the closing utility band stays understated on desktop and wraps cleanly on mobile
- Added the closing-pattern guidance to `docs/site-overview.md`

**Files or Areas Affected**  
- `archive/2026/week-10/index.html`
- `archive/2026/week-14/index.html`
- `assets/css/site.css`
- `docs/site-overview.md`
- `docs/development-log.md`

**Design or Structural Decisions**  
The implementation keeps `Dive deeper` as its own editorial section, then uses a single restrained band for article-end actions instead of separate labeled utility rows. The actions remain lightweight and text-forward so the reading experience still closes like a publication rather than a feature-heavy article template.

**Mobile / Performance / Accessibility Notes**  
- The change is HTML/CSS-only and keeps the existing small inline share script
- The consolidated band wraps into a simple vertical stack on smaller screens instead of becoming a cramped multi-row control area
- The closing links remain inside a semantic `nav` with a clear `aria-label`

**Risks / Watchouts**  
- If more article-end actions are added later, the single closing band could become too busy and recreate the same segmented feeling in a different form
- Future published editions should follow this same pattern so the ending treatment stays consistent across the archive

**Follow-Up Opportunities**  
- Review spacing between `Dive deeper`, the closing band, and the global footer in-browser to confirm the handoff feels calm on both desktop and mobile
- If future editions gain both previous and next links at once more often, consider whether the ordering inside the shared band should be tuned further for scanability

### 2026-04-13 - About Page Copy And Sources Refreshed

**Summary**  
Updated the About page to match the revised copy source, refined the Methodology language, and added a restrained â€œSources regularly reviewedâ€ subsection inside the Methodology area.

**Reason for Change**  
The About page needed to reflect the current publication direction more accurately while staying calm, credible, and publication-first. The new source acknowledgment also needed to build trust without turning the page into a directory or profile-heavy overview.

**What Changed**  
- Synced the public About page copy to the latest text in `docs/about-page-copy.md`
- Expanded the Methodology section with the revised language about how the scan draws from reporting, regulatory updates, policy developments, and adjacent industry coverage
- Added a light-touch â€œSources regularly reviewedâ€ subsection within Methodology rather than introducing a new top-level section
- Styled the source acknowledgment as a restrained inline list so it reads like editorial support material instead of a directory block
- Preserved the existing three-part About page structure: Why it exists, Methodology, and Author bio

**Files or Areas Affected**  
- `about/index.html`
- `assets/css/site.css`
- `docs/site-overview.md`
- `docs/development-log.md`

**Design or Structural Decisions**  
The implementation keeps the page refinement primarily in the copy structure rather than relying on heavier design treatment. The sources acknowledgment sits inside Methodology behind a small sentence-case subhead and uses compact, low-contrast list styling so it extends the trust signal without competing with the main editorial sections.

**Mobile / Performance / Accessibility Notes**  
- The update remains static HTML/CSS only with no new dependencies or behavior
- The source list wraps naturally on smaller screens so it stays readable without becoming a long vertical directory
- The subsection remains semantically part of the Methodology section, which keeps the page hierarchy clearer for readers and assistive technologies

**Risks / Watchouts**  
- If the source list grows too long over time, it could start to feel more like an index than a restrained acknowledgment
- Future copy changes should continue using `docs/about-page-copy.md` as the source of truth so the public page and content guidance do not drift apart

**Follow-Up Opportunities**  
- Review the new Methodology flow in-browser to confirm the subsection break feels supportive rather than interruptive
- If more source categories are added later, consider pruning or grouping them so the acknowledgment stays curated

### 2026-04-13 - About Page Source List Reformatted

**Summary**  
Reformatted the `Sources regularly reviewed` treatment on the About page from a wrapped inline run into a quieter editorial source list.

**Reason for Change**  
The comma-separated wrapped presentation felt awkward and accidental once it broke across lines. The sources needed to become easier to scan while remaining restrained, publication-first, and clearly subordinate to the Methodology section.

**What Changed**  
- Replaced the inline comma-separated source run with a true list using one source per line
- Styled the list as plain text links only, without chips, borders, boxes, or badge-like treatment
- Set the source list to two columns on desktop for easier scanning while keeping a single-column layout on mobile
- Preserved the existing subsection hierarchy so `Sources regularly reviewed` remains a subordinate part of Methodology

**Files or Areas Affected**  
- `about/index.html`
- `assets/css/site.css`
- `docs/development-log.md`

**Design or Structural Decisions**  
The list stays intentionally simple: no bullets, no card framing, and no metadata styling that would make the sources feel like UI. A two-column text list improves scanability on wider screens without turning the subsection into a directory block.

**Mobile / Performance / Accessibility Notes**  
- The update remains static HTML/CSS only
- Desktop uses a two-column text list; smaller screens collapse naturally to a single column without requiring alternate markup
- The sources are now a semantic list, which improves structure and makes the subsection more legible for assistive technologies

**Risks / Watchouts**  
- If the source names become materially longer later, the two-column layout should be rechecked to make sure it still feels calm and balanced
- If many more sources are added, the subsection could begin to feel more exhaustive than curated

**Follow-Up Opportunities**  
- Review the column balance in-browser to confirm the desktop list feels intentional rather than newspaper-like
- If the source set expands, consider grouping or pruning entries to preserve the restrained editorial tone

### 2026-04-14 - Week 15 Integrated

**Summary**  
Integrated the completed Week 15 markdown and image assets into the live publication flow so the new edition is now the current public-facing latest issue.

**Reason for Change**  
Week 15 needed to be published through the site's existing static edition pattern, then surfaced consistently across the homepage, archive views, and edition-to-edition navigation.

**What Changed**  
- Added a published Week 15 edition page at `archive/2026/week-15/index.html`
- Carried the Week 15 title, date range, hero image, body copy, and `Dive deeper` sources from the markdown into the established edition template
- Promoted Week 15 to the homepage latest-edition feature with its cover image, updated excerpt, and correct links
- Added Week 15 to the main archive and 2026 archive ahead of prior published editions
- Updated Week 14 so it links forward to Week 15 in the article-end utility navigation

**Files or Areas Affected**  
- `archive/2026/week-15/index.html`
- `archive/2026/week-14/index.html`
- `index.html`
- `archive/index.html`
- `archive/2026/index.html`
- `docs/development-log.md`

**Design or Structural Decisions**  
This integration follows the site's current hand-authored static workflow rather than introducing any new content pipeline. Week 15 reuses the existing article, homepage feature, archive listing, and closing-navigation patterns so the new edition feels like a normal continuation of the publication rather than a special-case layout.

**Mobile / Performance / Accessibility Notes**  
- The edition uses the provided Week 15 image asset directly within the established responsive article template
- Homepage and archive updates remain static HTML with no new behavior or dependencies
- Hero image alt text was carried from the markdown metadata into the published edition page

**Risks / Watchouts**  
- The site still depends on manual synchronization between markdown source files and published HTML, so future edition updates should continue checking for drift
- Week 15 now becomes the latest edition everywhere, so any future change to the preferred homepage excerpt or archive summary should be updated in multiple places unless the workflow becomes more automated later

**Follow-Up Opportunities**  
- Review the Week 15 article page in-browser to confirm image balance, reading flow, and closing navigation on both desktop and mobile
- If more published editions are added soon, consider whether the archive summaries should receive a small consistency pass for voice and length

### 2026-04-14 - Homepage Latest Preview Synced To Article Opening

**Summary**  
Updated the homepage latest-edition preview so it now uses the Week 15 article's existing structured opening instead of a hand-written summary-style excerpt.

**Reason for Change**  
The homepage preview had drifted away from the markdown source and was effectively presenting generated-style summary copy rather than the article's intended opening. The latest-edition preview needed to preserve the editorial wording already written for the edition.

**What Changed**  
- Replaced the current homepage preview text with the exact Week 15 `Hook`, `Hook Text`, and `Tech Framing` wording from `content/2026/week-15.md`
- Kept the existing homepage layout and featured-edition structure unchanged
- Preserved the markdown wording directly rather than paraphrasing or compressing it into a new summary

**Files or Areas Affected**  
- `index.html`
- `docs/development-log.md`

**Design or Structural Decisions**  
This fix stays intentionally narrow. The homepage still uses the existing static markup pattern, but the current featured-edition copy is now aligned with the markdown source of truth. No broader content-model or generation changes were introduced in this pass.

**Mobile / Performance / Accessibility Notes**  
- HTML-only content update with no change to behavior or dependencies
- The homepage preview remains in the existing featured-edition text block, so responsive behavior is unchanged

**Risks / Watchouts**  
- The homepage preview is still manually mirrored from markdown, so future edition promotions should continue checking for exact copy alignment unless a more automated sourcing step is introduced later

**Follow-Up Opportunities**  
- Review the featured-edition text block in-browser to confirm the longer direct source copy still feels balanced on both desktop and mobile

### 2026-04-14 - Preview Sourcing Rules Documented

**Summary**  
Updated the project guidance so homepage and archive preview text sourcing is now explicitly defined as part of the editorial system.

**Reason for Change**  
The latest-edition homepage preview had drifted because preview sourcing was implied rather than documented. Future editions need a clear rule that preserves editorial control and prevents structured opening copy from being replaced with paraphrased or generated summaries.

**What Changed**  
- Updated `AGENTS.md` to define homepage latest-edition preview sourcing from `Hook`, `Hook Text`, and `Tech Framing` when those structured sections are present
- Added guidance in `AGENTS.md` that archive preview text should also come from the structured article opening rather than new summary writing when that structure exists
- Updated `docs/site-overview.md` to document the same canonical preview-sourcing rule for future contributors and handoff
- Made explicit that preview text should preserve the markdown wording directly rather than being paraphrased or auto-summarized

**Files or Areas Affected**  
- `agents.md`
- `docs/site-overview.md`
- `docs/development-log.md`

**Design or Structural Decisions**  
This documentation change treats preview sourcing as part of the publication's content model without requiring a broader architectural change. The rule stays compatible with the current static hand-authored workflow while making the editorial source of truth clear.

**Mobile / Performance / Accessibility Notes**  
- Documentation-only change with no direct runtime impact
- The guidance helps maintain more consistent preview behavior across homepage and archive contexts, including on mobile

**Risks / Watchouts**  
- The rule is explicit, but the current workflow is still manual, so future contributors must still remember to mirror the structured opening into the relevant HTML until a more automated content flow exists

**Follow-Up Opportunities**  
- If the site later adds a generation step, use this documented rule as the basis for automating preview extraction from markdown

### 2026-04-14 - Edition Opening Structure Clarified

**Summary**  
Restored the missing `Tech Framing` line to the published Week 15 edition and updated the guidance so the full structured opening remains part of the article body when present in markdown.

**Reason for Change**  
The markdown for Week 15 included `Hook`, `Hook Text`, and `Tech Framing`, but the published edition page had dropped the `Tech Framing` line. The project guidance also needed to state clearly that this structured opening belongs in the edition itself, not only in preview contexts.

**What Changed**  
- Added the Week 15 `Tech Framing` line back into the published article body
- Updated `AGENTS.md` to require preserving `Hook`, `Hook Text`, and `Tech Framing` in the edition body when those structured opening fields exist
- Updated `docs/site-overview.md` to document the same article-opening rule for future contributors

**Files or Areas Affected**  
- `archive/2026/week-15/index.html`
- `agents.md`
- `docs/site-overview.md`
- `docs/development-log.md`

**Design or Structural Decisions**  
This keeps the structured opening consistent across the article itself and its preview contexts without changing the site's architecture. The edition body remains a calm continuous read, but it now preserves the full editorial opening as written in markdown.

**Mobile / Performance / Accessibility Notes**  
- HTML-only content correction plus documentation updates
- No new behavior or layout patterns were introduced

**Risks / Watchouts**  
- The workflow is still manual, so future edition integrations should continue checking that the full opening sequence appears in both the article page and any preview contexts where the guidance calls for it

**Follow-Up Opportunities**  
- Review the opening rhythm on the Week 15 article page to confirm the added `Tech Framing` paragraph feels natural between the opening setup and the evidence sequence

### 2026-04-14 - Pull Quote Treatment Removed From Editions

**Summary**  
Removed the pull-quote styling from the published editions so the article body now reads as a continuous longform piece throughout.

**Reason for Change**  
The emphasized quote treatment was making the editions feel more segmented than the intended publication-first reading experience. The articles should stay visually consistent and uninterrupted unless a special treatment is deliberately introduced later.

**What Changed**  
- Converted the quote-styled paragraphs in the published edition pages back into normal body paragraphs
- Removed the unused shared `.pull-quote` styling from the site CSS
- Updated the project guidance to state that standard editions should not break out individual lines as pull quotes or quote modules unless explicitly requested

**Files or Areas Affected**  
- `archive/2026/week-14/index.html`
- `archive/2026/week-15/index.html`
- `assets/css/site.css`
- `agents.md`
- `docs/site-overview.md`
- `docs/development-log.md`

**Design or Structural Decisions**  
This keeps the reading experience more editorial and continuous by letting important lines carry emphasis through the writing itself rather than through a separate visual treatment.

**Mobile / Performance / Accessibility Notes**  
- HTML/CSS-only refinement with no behavior changes
- Removing the pull-quote block helps maintain a more even reading rhythm on smaller screens as well as desktop

**Risks / Watchouts**  
- Future edition integrations should check that no old quote-class markup gets copied forward from earlier pages

**Follow-Up Opportunities**  
- Review the mid-article and closing rhythm on the published editions to confirm the longform flow now feels more even

### 2026-04-14 - About Bio Link Row Expanded

**Summary**  
Added the Finding Critical Path LinkedIn newsletter to the About page Author bio link row so the publication's LinkedIn home is clearly distinct from the author's personal profile.

**Reason for Change**  
The About page already linked to Josh Bell's personal LinkedIn profile and email, but it did not yet provide a direct path to the LinkedIn-hosted version of the publication.

**What Changed**  
- Added a `Newsletter` link to the existing Author bio link row on the About page
- Kept the existing restrained inline treatment and left the surrounding copy and layout unchanged

**Files or Areas Affected**  
- `about/index.html`
- `docs/development-log.md`

**Design or Structural Decisions**  
The new link stays in the existing inline row to preserve the publication-first, minimal About page presentation rather than introducing additional explanatory copy or a separate publication-links treatment.

**Mobile / Performance / Accessibility Notes**  
- Reused the current link-row structure and spacing, so the row remains lightweight and wraps cleanly on smaller screens
- No performance impact expected

### 2026-04-14 - About Page Independence Line Added

**Summary**  
Synced the About page with the latest approved `Why it exists` copy by adding the new closing sentence that clarifies the publication's independence and authorship.

**Reason for Change**  
`docs/about-page-copy.md` was updated with an additional final sentence in the first section, and the public About page needed to match the source-of-truth copy.

**What Changed**  
- Added `Finding Critical Path is an independent publication written by Josh Bell.` to the end of the `Why it exists` section on the public About page

**Files or Areas Affected**  
- `about/index.html`
- `docs/development-log.md`

**Design or Structural Decisions**  
This remains a copy-only update and preserves the existing About page structure and styling.

**Mobile / Performance / Accessibility Notes**  
- No layout or behavior changes
- No performance impact expected

### 2026-04-14 - Structural Close Preservation Clarified

**Summary**  
Restored the full Week 15 `Structural Close` wording from markdown and updated the project guidance so structured closing sections are preserved directly in published editions.

**Reason for Change**  
The published Week 15 edition was still carrying a shortened version of the `Structural Close` instead of the full markdown text. The guidance needed to make the closing sequence explicit so future editions do not trim or rewrite it.

**What Changed**  
- Replaced the shortened Week 15 closing paragraph with the full `Structural Close` wording from `content/2026/week-15.md`
- Updated `AGENTS.md` to require preserving `Structural Close` and `Forward Looking Question` directly from markdown when those structured closing fields are present
- Updated `docs/site-overview.md` to document the same rule for future contributors

**Files or Areas Affected**  
- `archive/2026/week-15/index.html`
- `agents.md`
- `docs/site-overview.md`
- `docs/development-log.md`

**Design or Structural Decisions**  
This keeps the edition close aligned with the markdown source of truth and treats the closing sequence as part of the canonical editorial structure, not as optional or compressible supporting copy.

**Mobile / Performance / Accessibility Notes**  
- HTML-only content correction plus documentation updates
- No behavior or layout changes were introduced

**Risks / Watchouts**  
- The current workflow remains manual, so future edition integrations should continue checking the close against the markdown source as carefully as the opening

**Follow-Up Opportunities**  
- Review the Week 15 ending in-browser to confirm the restored full close and the forward-looking question still read with the intended rhythm before `Dive deeper`

### 2026-04-14 - Week 13 Integrated

**Summary**  
Published Week 13 as a live edition page and wired it into the existing static publication flow.

**Reason for Change**  
The project already had the Week 13 markdown and graphic in place. The site needed the edition published through the standard article pattern, then surfaced on the homepage, archive views, and adjacent edition navigation without broader structural changes.

**What Changed**  
- Replaced the old Week 13 redirect page with a full published edition at `archive/2026/week-13/index.html`
- Carried the Week 13 title, date, hero image, opening, body, closing, and `Dive deeper` entries from `content/2026/week-13.md` into the live edition page
- Promoted Week 13 into the homepage featured latest-edition slot using the markdown's `Hook`, `Hook Text`, and `Tech Framing` verbatim
- Added Week 13 to the main archive and the 2026 archive in chronological position among the currently published editions
- Updated adjacent previous/next links so Week 10 leads to Week 13 and Week 14 points back to Week 13
- Renamed the Week 13 image asset to match the markdown filename casing so the deployed path stays aligned with the source metadata

**Files or Areas Affected**  
- `assets/2026/week-13/w13cover.png`
- `archive/2026/week-13/index.html`
- `archive/2026/week-10/index.html`
- `archive/2026/week-14/index.html`
- `archive/index.html`
- `archive/2026/index.html`
- `index.html`
- `docs/development-log.md`

**Design or Structural Decisions**  
This remained a manual static-content integration using the site's existing edition template, homepage feature block, archive list pattern, and closing utility navigation. The implementation preserves the markdown wording directly instead of rewriting any structured opening, closing, or source material.

**Mobile / Performance / Accessibility Notes**  
- No new dependencies or scripts were introduced
- Week 13 reuses the site's existing responsive article layout and homepage feature treatment
- The hero image alt text was taken directly from the markdown metadata

**Risks / Watchouts**  
- Homepage latest-edition promotion now points to Week 13 while later-dated published editions still exist in the archive, so that editorial ordering should be checked intentionally
- The workflow is still manual, so future edition integrations should continue checking asset filenames and preview copy against the markdown source

**Follow-Up Opportunities**  
- Review the homepage and archive flows in-browser to confirm the Week 13 promotion is the intended editorial ordering
- If future editions continue to be integrated out of sequence, consider documenting the desired rule for homepage promotion versus archive chronology more explicitly

### 2026-04-14 - Edition Ordering Corrected

**Summary**  
Corrected the homepage, archive listings, and adjacent edition navigation so published 2026 editions once again follow true edition chronology rather than recent integration order.

**Reason for Change**  
Week 13 had been promoted as the homepage feature because it was added most recently, which broke the publication's chronology rules. The site needed a cleanup pass so homepage and archive behavior reflect edition dates from the content source of truth.

**What Changed**  
- Restored Week 15 as the homepage featured latest edition
- Reordered the homepage `Past Editions` section to show the most recent prior published editions only, in reverse chronological order
- Reordered the main archive and 2026 archive listings to `week-15`, `week-14`, `week-10`, `week-13`
- Corrected adjacent edition navigation so Week 13 leads into Week 10, Week 10 into Week 14, and Week 14 into Week 15

**Files or Areas Affected**  
- `index.html`
- `archive/index.html`
- `archive/2026/index.html`
- `archive/2026/week-13/index.html`
- `docs/development-log.md`

**Design or Structural Decisions**  
This was kept as a narrow cleanup pass within the existing static workflow. No article copy, layout pattern, or broader site architecture was changed.

**Mobile / Performance / Accessibility Notes**  
- No new dependencies or behavior changes
- Existing responsive homepage and archive patterns were preserved while restoring content order


### 2026-04-14 - Week 10 Removed From Published Flow

**Summary**  
Removed the legacy Week 10 sample page from the public published-edition flow until a real markdown-backed Week 10 edition is ready.

**Reason for Change**  
`content/2026/week-10.md` has not been populated yet, so the live Week 10 HTML was behaving like a published edition even though it was still older standalone sample content outside the current markdown-driven workflow.

**What Changed**  
- Removed Week 10 from the homepage `Past Editions` section
- Removed Week 10 from the main archive and 2026 archive published-edition listings
- Reconnected adjacent edition navigation so the published chain now runs Week 13 -> Week 14 -> Week 15
- Left the legacy Week 10 page file in place, but stopped treating it as part of the active published sequence

**Files or Areas Affected**  
- `index.html`
- `archive/index.html`
- `archive/2026/index.html`
- `archive/2026/week-13/index.html`
- `archive/2026/week-14/index.html`
- `docs/development-log.md`

**Design or Structural Decisions**  
This was handled as a publication-state cleanup only. The underlying static files were not refactored or redesigned; the site now simply excludes Week 10 from public chronology until the markdown source is populated and published through the same structure as the other editions.

**Mobile / Performance / Accessibility Notes**  
- No new dependencies or behavior changes
- Existing homepage, archive, and edition templates were preserved

### 2026-04-14 - Week 12 Integrated As Archived Edition

**Summary**  
Published Week 12 as an older archived edition and inserted it into the existing 2026 publication sequence without changing homepage latest-edition behavior.

**Reason for Change**  
Week 12 was ready to publish from markdown, but it is older than the current latest edition. The site needed a backfill integration that respected true edition chronology rather than recent integration timing.

**What Changed**  
- Replaced the reserved Week 12 redirect with a live edition page at `archive/2026/week-12/index.html`
- Carried Week 12 title, date, hero image, body copy, and `Dive deeper` entries from `content/2026/week-12.md` into the published article page
- Added Week 12 to the main archive and 2026 archive in chronological position after Week 13
- Updated adjacent edition navigation so the published chain now includes Week 12 before Week 13
- Aligned the Week 12 image asset filename with the markdown metadata so the published path matches the source of truth

**Files or Areas Affected**  
- `assets/2026/week-12/w12cover.png`
- `archive/2026/week-12/index.html`
- `archive/2026/week-13/index.html`
- `archive/index.html`
- `archive/2026/index.html`
- `docs/development-log.md`

**Design or Structural Decisions**  
This was implemented as an archive backfill within the existing static workflow. Homepage latest-edition treatment was intentionally left unchanged because Week 12 is older than the currently featured published issue.

**Mobile / Performance / Accessibility Notes**  
- No new dependencies or scripts were added
- Week 12 reuses the current responsive edition-page template and archive listing pattern
- The hero image alt text was taken directly from the markdown metadata

### 2026-04-14 - Homepage Past Editions Synced After Week 12 Backfill

**Summary**  
Added Week 12 into the homepage `Past Editions` strip so the homepage now reflects the full current published sequence behind the latest edition.

**Reason for Change**  
Week 12 had been added to the archive flow correctly, but the homepage secondary edition strip had not yet been expanded to include it as the third prior published edition.

**What Changed**  
- Added Week 12 as the third homepage `Past Editions` tile after Week 14 and Week 13
- Kept the homepage featured latest edition unchanged as Week 15

**Files or Areas Affected**  
- `index.html`
- `docs/development-log.md`
