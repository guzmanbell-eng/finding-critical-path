# Google Search Setup Guide for Finding Critical Path

## Purpose

This document explains how to make the **Finding Critical Path** website easier for Google to discover, crawl, index, and understand. It is written as a handoff guide for an early-career web developer. The goal is not just to complete the tasks, but to understand what each task does and how to verify that it worked.

This guide assumes:
- the site is already live at `https://findingcriticalpath.com`
- the site is a static site
- the website codebase already exists and can be updated through the normal development workflow
- the objective is to improve the site’s visibility in Google Search over time

## Important context

Getting a site to show up in Google is not a single switch that gets flipped. It is a combination of:
- making sure Google can crawl the site
- making sure Google can find all the important pages
- making sure each page clearly communicates what it is about
- making sure the site sends clean, consistent technical signals
- giving Google tools to monitor indexing and detect problems

Even if all of this is done correctly, Google still decides when and how pages are indexed and ranked. The goal of this work is to make the site technically ready and easy for Google to process.

## What success looks like

When this work is complete:
- Google Search Console is connected to the domain
- a sitemap is available and submitted to Google
- a `robots.txt` file is present and correctly references the sitemap
- each important page has a canonical URL
- page titles and descriptions are clean and useful
- each edition page includes structured data that helps Google understand the content
- the site can be checked and monitored through Search Console going forward

## Scope of work

This guide covers:
1. Google Search Console setup
2. Sitemap generation and submission
3. `robots.txt` creation or verification
4. Canonical URL setup
5. Metadata review and cleanup
6. Structured data implementation
7. Internal linking review
8. Verification and monitoring

This guide does **not** cover:
- paid search or Google Ads
- internal archive search
- backlink strategy or off-site promotion
- full content strategy / keyword research beyond basic metadata guidance

---

# Phase 1: Preparation

## 1. Confirm the production domain and deployment behavior

### Why this matters
Before changing SEO settings, confirm the exact live domain and whether there are any alternate versions of the site. Mixed domain signals can confuse search engines.

### Checklist
- [ ] Confirm the primary production domain is `https://findingcriticalpath.com`
- [ ] Confirm whether `https://www.findingcriticalpath.com` redirects to the primary domain or vice versa
- [ ] Confirm there are no duplicate production environments accidentally open to indexing
- [ ] Confirm the site is publicly reachable without login or access restrictions

### Deliverable
A short note in the implementation log stating which domain is canonical and whether any alternate hostnames redirect correctly.

### Acceptance criteria
- Only one public domain is treated as primary
- Alternate versions redirect to the primary domain

---

# Phase 2: Google Search Console

## 2. Add the site to Google Search Console

### Why this matters
Google Search Console is the primary tool for:
- submitting the sitemap
- inspecting specific URLs
- checking indexing status
- seeing crawl and enhancement issues
- monitoring search performance over time

### Checklist
- [ ] Sign in to Google Search Console with the account that should manage the site
- [ ] Add the site as a **Domain property** if possible
- [ ] If Domain property verification is not feasible, use a **URL-prefix property** for `https://findingcriticalpath.com`
- [ ] Complete the verification method
- [ ] Confirm the property shows as verified

### Notes for the developer
Domain property verification is preferred because it covers all protocols and subdomains. If DNS access is not available, a URL-prefix property can still work, but it is narrower.

### Deliverable
Verified Search Console property.

### Acceptance criteria
- Search Console shows the property as verified
- The implementation owner can access the Search Console dashboard

---

# Phase 3: Sitemap

## 3. Make sure the site generates a sitemap

### Why this matters
A sitemap helps Google discover important URLs, especially on content-driven sites where new pages are added over time.

### Checklist
- [ ] Review the site build setup and confirm how sitemap generation is currently handled
- [ ] If the site does not already generate a sitemap, add sitemap generation to the build process
- [ ] Confirm the sitemap is produced in the final built site output
- [ ] Confirm the sitemap includes:
  - [ ] homepage
  - [ ] archive page(s)
  - [ ] all published edition pages
  - [ ] about page and other important public pages
- [ ] Confirm it excludes non-public or irrelevant pages

### Technical guidance
If the site uses Astro, use the official sitemap integration in the project so the sitemap is generated automatically during build.

### Deliverable
Accessible sitemap file on the live site.

### Typical expected URL
One of the following, depending on the site setup:
- `https://findingcriticalpath.com/sitemap-index.xml`
- `https://findingcriticalpath.com/sitemap.xml`

### Verification steps
- [ ] Open the sitemap URL in a browser
- [ ] Confirm it loads without error
- [ ] Confirm important pages appear in it

### Acceptance criteria
- Sitemap exists on the live site
- Sitemap includes all important public pages
- Sitemap does not include junk, duplicate, or staging pages

---

## 4. Submit the sitemap in Google Search Console

### Why this matters
Submitting the sitemap gives Google a clean entry point for discovering the site’s content.

### Checklist
- [ ] Open the verified Search Console property
- [ ] Go to the **Sitemaps** section
- [ ] Submit the live sitemap URL
- [ ] Confirm Google accepts the submission
- [ ] Record the sitemap location in the implementation notes

### Deliverable
Submitted sitemap in Search Console.

### Acceptance criteria
- Search Console shows the sitemap as submitted
- No immediate format or fetch errors appear

---

# Phase 4: robots.txt

## 5. Create or verify `robots.txt`

### Why this matters
The `robots.txt` file tells crawlers what they are allowed to access and gives them the sitemap location. It is a crawl guidance file, not a ranking tool.

### Checklist
- [ ] Check whether `https://findingcriticalpath.com/robots.txt` already exists
- [ ] If it does not exist, create it
- [ ] If it exists, review it for errors or unnecessary restrictions
- [ ] Make sure it allows crawling of the public site
- [ ] Add the sitemap URL to the file

### Recommended baseline content
Use this as the starting point unless there is a clear reason to change it:

```txt
User-agent: *
Allow: /

Sitemap: https://findingcriticalpath.com/sitemap-index.xml
```

If the actual sitemap path is `sitemap.xml`, update the file accordingly.

### Verification steps
- [ ] Open `https://findingcriticalpath.com/robots.txt`
- [ ] Confirm it loads
- [ ] Confirm it does not block the public pages
- [ ] Confirm the sitemap path listed is correct

### Acceptance criteria
- `robots.txt` exists on the live site
- Public pages are crawlable
- The sitemap reference is accurate

---

# Phase 5: Canonical URLs

## 6. Add canonical tags to all important pages

### Why this matters
Canonical tags help Google understand the preferred URL for a page. This reduces confusion when similar or duplicate URLs can exist.

### Checklist
- [ ] Review the site layout or shared head component
- [ ] Add a canonical URL tag to the shared page head logic if it is not already present
- [ ] Confirm that each page outputs a canonical URL using the live production domain
- [ ] Confirm canonical tags exist on:
  - [ ] homepage
  - [ ] archive page
  - [ ] edition pages
  - [ ] about page

### Example
```html
<link rel="canonical" href="https://findingcriticalpath.com/archive/2026/week-15/" />
```

### Notes for the developer
- Canonical URLs should use the final production domain
- They should be absolute URLs, not relative paths
- They should match the intended public URL exactly

### Verification steps
- [ ] View page source for representative pages
- [ ] Confirm the canonical link appears once
- [ ] Confirm the canonical URL is correct for each page

### Acceptance criteria
- Every important indexable page has a correct canonical tag
- No page points canonically to the wrong URL

---

# Phase 6: Metadata cleanup

## 7. Review and improve page titles and meta descriptions

### Why this matters
Titles and meta descriptions help Google understand the page and often influence how the result appears in search.

### Checklist
- [ ] Review the title tag pattern used site-wide
- [ ] Review the meta description pattern used site-wide
- [ ] Confirm the homepage has a strong title and description
- [ ] Confirm the archive page has a clear title and description
- [ ] Confirm each edition page has a unique title and description

### Guidance for titles
Titles should be:
- specific
- human-readable
- tied to the actual page topic
- consistent in branding

### Recommended title approach
- Homepage: `Finding Critical Path | Nuclear, Energy, and Technology Signals`
- Archive page: `Archive | Finding Critical Path`
- Edition page: `[Edition Title] | Finding Critical Path`

### Guidance for descriptions
Descriptions should summarize the page in plain language. Avoid keyword stuffing.

### Verification steps
- [ ] View source on representative pages
- [ ] Confirm one title tag per page
- [ ] Confirm one meta description per page
- [ ] Confirm edition pages do not reuse the exact same description

### Acceptance criteria
- All major pages have clean metadata
- Edition pages have unique, page-specific metadata

---

# Phase 7: Structured data

## 8. Add structured data for the site and edition pages

### Why this matters
Structured data gives search engines more explicit information about what a page represents.

### What to implement
There are two main structured data layers to add:

#### A. Site-level organization/publisher data
Use site-wide structured data to describe the publication or publisher.

#### B. Article-level structured data
Use page-level structured data on each edition page so Google can understand:
- the headline
- the author
- the publication date
- the description
- the image
- the canonical page URL

### Checklist
- [ ] Decide where the site-level structured data should live
- [ ] Add site-level JSON-LD to the shared layout if appropriate
- [ ] Add article JSON-LD generation to the edition page template
- [ ] Make sure each edition page provides the needed data fields
- [ ] Validate at least one representative page after deployment

### Example JSON-LD shape for an edition page
```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "BlogPosting",
  "headline": "Example Edition Title",
  "author": {
    "@type": "Person",
    "name": "Josh Bell"
  },
  "datePublished": "2026-04-21",
  "dateModified": "2026-04-21",
  "description": "A concise summary of the edition.",
  "mainEntityOfPage": {
    "@type": "WebPage",
    "@id": "https://findingcriticalpath.com/archive/2026/week-15/"
  }
}
</script>
```

### Notes for the developer
- Use real page data, not placeholders
- If an edition has a lead image, include it in the structured data
- Keep the structured data aligned with the visible page content

### Verification steps
- [ ] Validate representative pages using a structured data testing workflow
- [ ] Confirm there are no syntax errors
- [ ] Confirm the content matches the page

### Acceptance criteria
- Site-level structured data is present where intended
- Each edition page includes valid article/post structured data

---

# Phase 8: Internal linking and crawlability

## 9. Review internal links across the site

### Why this matters
Google finds content partly through internal links. A page that is linked clearly from other pages is easier to discover and understand.

### Checklist
- [ ] Confirm the homepage links to the archive
- [ ] Confirm the archive links to every published edition
- [ ] Confirm edition pages are reachable through normal links, not only JavaScript interactions
- [ ] Confirm there are no orphaned edition pages
- [ ] If practical, add previous/next edition links on article pages

### Verification steps
- [ ] Click through the site manually
- [ ] Confirm each important page is reachable through crawlable links

### Acceptance criteria
- All published editions are linked from the archive
- No important public page is isolated from internal navigation

---

# Phase 9: Final verification

## 10. Run a production verification pass

### Why this matters
SEO work is easy to partially complete. This final check confirms the live site actually reflects the intended setup.

### Checklist
- [ ] Confirm Search Console property is verified
- [ ] Confirm sitemap is live and submitted
- [ ] Confirm `robots.txt` is live
- [ ] Confirm canonical tags are present on representative pages
- [ ] Confirm metadata is present on representative pages
- [ ] Confirm structured data is present on representative edition pages
- [ ] Confirm the site is publicly crawlable

### Suggested spot-check pages
- [ ] Homepage
- [ ] Archive page
- [ ] Most recent edition page
- [ ] One older edition page
- [ ] About page

### Acceptance criteria
All listed checks pass on the live production site.

---

# Phase 10: Search Console follow-up and monitoring

## 11. Request indexing for key pages

### Why this matters
This is not required for every page, but it is a useful follow-up step for the most important URLs after setup is complete.

### Checklist
- [ ] Use URL Inspection in Search Console for the homepage
- [ ] Use URL Inspection for the archive page
- [ ] Use URL Inspection for the most recent edition page
- [ ] Request indexing if appropriate

### Acceptance criteria
The most important pages have been inspected in Search Console after deployment.

---

## 12. Establish an ongoing monitoring routine

### Why this matters
Google search setup is not one-and-done. The site should be monitored over time.

### Checklist
- [ ] Check Search Console after initial deployment
- [ ] Recheck after Google processes the sitemap
- [ ] Monitor for:
  - [ ] indexing issues
  - [ ] crawl errors
  - [ ] structured data errors
  - [ ] pages excluded from indexing
- [ ] Add Search Console review to the normal site maintenance process

### Recommended cadence
- First review: within a few days after deployment
- Second review: within 2 to 4 weeks
- Ongoing review: monthly or whenever site structure changes significantly

### Acceptance criteria
There is a named owner and a repeatable review cadence.

---

# Suggested implementation order

If the developer wants a clear order of operations, use this sequence:

1. Confirm production domain behavior
2. Set up Search Console
3. Generate or verify sitemap
4. Submit sitemap
5. Create or verify `robots.txt`
6. Add canonical tags
7. Review metadata
8. Add structured data
9. Review internal linking
10. Run live verification
11. Inspect and request indexing for key URLs
12. Begin ongoing monitoring

---

# Definition of done

This project is complete when all of the following are true:
- Search Console is verified
- the sitemap is live and submitted
- `robots.txt` is live and references the correct sitemap
- canonical tags are present on all major indexable pages
- metadata is in place and page-specific
- structured data is present on the publication and edition pages as intended
- internal linking is sufficient for crawlability
- the live site has been spot-checked
- a monitoring process has been defined

---

# Handoff notes for the project owner

Once this work is complete, the site should be in a much better position for Google discovery and indexing. That does not guarantee rankings, but it does create a technically sound foundation. As new editions are published, the most important ongoing habits will be:
- keeping the sitemap current
- keeping metadata clean
- making sure new pages are linked from the archive
- periodically checking Search Console for issues
