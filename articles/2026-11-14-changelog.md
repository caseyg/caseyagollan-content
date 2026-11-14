---
date: 2026-11-14T20:00:00-05:00
title: 2026-11-14 Changelog
summary: A post composer at /new and a rebuilt edit page, so I can write and
  edit on the site itself, with drafts kept in a private repo. All posts are
  Markdown now. Imported the Bluesky and Mastodon archive backlog, with thread
  rollups, link cards and quoted posts. Added site search, post type filters,
  a faster library graph, a new nav and 404 page, and branch previews.
category: changelog
draft: true
---

<!-- Review before publishing: items marked [In progress] were still open on
2026-11-14. Remove the marker once each one merges, or cut the bullet. Then set
draft: false. -->

## Publishing

* New post composer at `/new`, with every post type Quill offers: notes, articles, replies, bookmarks, likes, reposts, RSVPs, photos, video, events, reviews, itineraries, and food/drink. Publishing goes through the site's own Micropub endpoint, so posts are validated and stored exactly like posts from Quill. Photo and video uploads, browser location, and a bookmarklet that prefills the form. [#143](https://github.com/caseyg/caseyagollan.com/pull/143)
* Drafts are saved to a separate private GitHub repo, so unpublished writing never shows up in the public content repo. Drafts can be reopened, updated, discarded, or published. Fixed "Save draft" being ignored when the buttons disabled on submit. [#144](https://github.com/caseyg/caseyagollan.com/pull/144)
* Redesigned the composer around a single writing surface, like a social app's compose box. It opens straight into a note; a menu switches post type and a Drafts menu lists drafts. Optional fields (photos, reply-to, location, tags, slug/date) open from toolbar icons. Syndication is a pair of chips with a character count for the strictest service. Star buttons for reviews, a segmented choice for RSVPs. Still works without JavaScript. [#146](https://github.com/caseyg/caseyagollan.com/pull/146)
* On-site edit page for any post once I'm signed in. Saves only the changed properties, and rejects stale edits. Markdown opens in a rich text editor with a toggle to the raw source. [#140](https://github.com/caseyg/caseyagollan.com/pull/140)
* Rebuilt the edit page to match the composer. Frontmatter shows as an Obsidian-style properties panel, with an Open on GitHub link. [#148](https://github.com/caseyg/caseyagollan.com/pull/148)
* **[In progress]** Edit page fixes: an Edit button on index pages, skeleton loading, and a Syndicate link.
* Syndication editor on each post, writing links back to GitHub. Syndication drafts link to the Bluesky/Mastodon posts they mention, with live counts. [#90](https://github.com/caseyg/caseyagollan.com/pull/90) [#135](https://github.com/caseyg/caseyagollan.com/pull/135) [#136](https://github.com/caseyg/caseyagollan.com/pull/136)
* Sign-in fixes: native IndieAuth callbacks for Quill on iOS, streamlined passkey sign-in, correct token scope selection, and names for personal tokens. [#132](https://github.com/caseyg/caseyagollan.com/pull/132) [#133](https://github.com/caseyg/caseyagollan.com/pull/133) [#134](https://github.com/caseyg/caseyagollan.com/pull/134)
* Private Readwise review queue for batch-importing bookmarks, with editable summaries, tags, and import receipts. [#103](https://github.com/caseyg/caseyagollan.com/pull/103) [#111](https://github.com/caseyg/caseyagollan.com/pull/111) [#118](https://github.com/caseyg/caseyagollan.com/pull/118)

## Markdown everywhere

* Converted the 154 posts stored as HTML to Markdown. Each conversion was checked to render the same HTML; a full build matched on 1,883 of 1,889 pages. Saved copies of other people's posts stay as fetched. [content#16](https://github.com/caseyg/caseyagollan-content/pull/16)
* Bluesky and Mastodon imports are saved as Markdown whenever it renders the same post, and the edit page saves HTML posts back as Markdown. [#138](https://github.com/caseyg/caseyagollan.com/pull/138) [#148](https://github.com/caseyg/caseyagollan.com/pull/148)

## Notes & Posts

* Imported the public Bluesky and Mastodon archive backlog, about 1,100 posts, with deduplication, real activity timestamps, and privacy checks. Locked accounts and Bluesky public-access opt-outs are left out. [#99](https://github.com/caseyg/caseyagollan.com/pull/99) [#100](https://github.com/caseyg/caseyagollan.com/pull/100) [content#7](https://github.com/caseyg/caseyagollan-content/pull/7)
* Saved social cards now include photo galleries, link cards, quoted posts, and images copied to R2. [#84](https://github.com/caseyg/caseyagollan.com/pull/84) [#87](https://github.com/caseyg/caseyagollan.com/pull/87) [#104](https://github.com/caseyg/caseyagollan.com/pull/104)
* Imported Bluesky posts render their links, profile-linked mentions, and link cards, instead of plain text with the URL repeated underneath. Re-rendered the existing imports. [#142](https://github.com/caseyg/caseyagollan.com/pull/142) [content#15](https://github.com/caseyg/caseyagollan-content/pull/15)
* Likes and reposts of the same thing roll up into one entry on indexes, across networks and dates. Bluesky thread likes, reposts, and replies group into a shared thread card that links to its day archive. [#106](https://github.com/caseyg/caseyagollan.com/pull/106) [#129](https://github.com/caseyg/caseyagollan.com/pull/129) [#131](https://github.com/caseyg/caseyagollan.com/pull/131) [#139](https://github.com/caseyg/caseyagollan.com/pull/139)
* Replies use the shared post card, with the parent post and usernames condensed above. [#115](https://github.com/caseyg/caseyagollan.com/pull/115) [#119](https://github.com/caseyg/caseyagollan.com/pull/119) [#121](https://github.com/caseyg/caseyagollan.com/pull/121) [#122](https://github.com/caseyg/caseyagollan.com/pull/122)
* Pagination on the posts index. [#109](https://github.com/caseyg/caseyagollan.com/pull/109)
* **[In progress]** Post type filter pills on the feed, date, tag, and type pages, behind a Filter button. Each type has its emoji; click to hide a type, double-click to show only that one. Filtered views have shareable URLs. [#145](https://github.com/caseyg/caseyagollan.com/pull/145)

## Search

* Site search with Pagefind, covering posts, books, saved social posts, and published [cag.wiki](https://cag.wiki) pages. Book covers and post images in results, catalog and author filters, and authors sorted by surname. [#85](https://github.com/caseyg/caseyagollan.com/pull/85) [#92](https://github.com/caseyg/caseyagollan.com/pull/92) [#101](https://github.com/caseyg/caseyagollan.com/pull/101) [#102](https://github.com/caseyg/caseyagollan.com/pull/102)

## Library

* **[In progress]** The library graph shows up about 3.5x sooner (2.0s instead of 7.0s in testing), and the longest main-thread stall dropped from 3.9s to 0.18s. The layout runs once, then spines and covers paint in over the next frames. Smoother loading animation, sharper covers, shelf arrows that follow the displayed order, selection kept when switching views, and smoother book permalink transitions. [#147](https://github.com/caseyg/caseyagollan.com/pull/147)
* Books animate between shelf layouts with a spring. [#125](https://github.com/caseyg/caseyagollan.com/pull/125) [#128](https://github.com/caseyg/caseyagollan.com/pull/128)
* Better mobile browsing: fixed gestures and shelf selection, smoother book permalink loading, and tags as chips. [#116](https://github.com/caseyg/caseyagollan.com/pull/116) [#126](https://github.com/caseyg/caseyagollan.com/pull/126) [#127](https://github.com/caseyg/caseyagollan.com/pull/127)
* Book details render before the graph loads. Open Library descriptions and larger covers are cached in R2. [#105](https://github.com/caseyg/caseyagollan.com/pull/105) [#117](https://github.com/caseyg/caseyagollan.com/pull/117)

## Design

* **[In progress]** Redesigned the sitewide navigation.
* **[In progress]** New 404 page.
* Design tokens and composable UI primitives, with Storybook stories for every site component, including the composer parts. [#123](https://github.com/caseyg/caseyagollan.com/pull/123) [#124](https://github.com/caseyg/caseyagollan.com/pull/124) [#148](https://github.com/caseyg/caseyagollan.com/pull/148)

## Builds & Previews

* Every pushed branch gets its own Worker Preview URL, with sign-in, publishing, and imports turned off. [#141](https://github.com/caseyg/caseyagollan.com/pull/141)
* Cleared build diagnostics and fixed a navigation layout shift while search loads. [#82](https://github.com/caseyg/caseyagollan.com/pull/82) [#96](https://github.com/caseyg/caseyagollan.com/pull/96)
