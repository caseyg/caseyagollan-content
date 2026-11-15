---
date: 2026-11-14T20:00:00-05:00
title: 2026-11-14 Changelog
summary: A post composer at /new and a rebuilt edit page, so I can write, edit
  and syndicate on the site itself, with drafts kept in a private repo. All
  posts are Markdown now. Imported the Bluesky and Mastodon archive backlog, with
  thread rollups, link cards and quoted posts. New sitewide nav and 404 page,
  site search, post type filters, a much faster library, and branch previews.
category: changelog
draft: false
---

## Publishing

<figure class="align-right narrow"><img src="https://files.caseyagollan.com/publishing/2026/11/5a1e5c58-780f-4d03-97c2-f220117e086a.webp" alt="The note composer on a phone: close, a Note menu, a drafts count, Save draft and Publish along the top, a borderless What’s on your mind? box, a row of field icons, and Mastodon and Bluesky chips."><figcaption>The composer opens straight into a note.</figcaption></figure>

* New post composer at `/new`, with every post type Quill offers: notes, articles, replies, bookmarks, likes, reposts, RSVPs, photos, video, events, reviews, itineraries, and food/drink. Publishing goes through the site's own Micropub endpoint, so posts are validated and stored exactly like posts from Quill. Photo and video uploads, browser location, and a bookmarklet that prefills the form. [#143](https://github.com/caseyg/caseyagollan.com/pull/143)
* Redesigned it around a single writing surface, like a social app's compose box. A menu switches post type and a Drafts menu lists drafts. Optional fields (photos, reply-to, location, tags, slug/date) open from toolbar icons. Syndication is a pair of chips with a character count for the strictest service. Star buttons for reviews, a segmented choice for RSVPs. Still works without JavaScript. [#146](https://github.com/caseyg/caseyagollan.com/pull/146)
* Drafts are saved to a separate private GitHub repo, so unpublished writing never shows up in the public content repo. They can be reopened, updated, discarded, or published. Fixed "Save draft" being ignored, drafts not loading when clicked, and `/new` 404ing from client-side links. Menus now share one popover that closes on an outside click or Escape. [#144](https://github.com/caseyg/caseyagollan.com/pull/144) [#152](https://github.com/caseyg/caseyagollan.com/pull/152)

<figure class="align-right narrow"><img src="https://files.caseyagollan.com/publishing/2026/11/3f2dc426-c04e-48af-a168-d34866dec8b2.webp" alt="The edit page for a note on a phone: Open on GitHub, Syndicate and Save buttons along the top, and a Properties panel listing date, status, pesos-source and syndication, with Add property below."><figcaption>Frontmatter as properties, with list values as removable pills.</figcaption></figure>

* On-site edit page for any post once I'm signed in. It saves only the changed properties and rejects stale edits. Markdown opens in a rich text editor with a toggle to the raw source. [#140](https://github.com/caseyg/caseyagollan.com/pull/140)
* Rebuilt the edit page to match the composer. Frontmatter shows as an Obsidian-style properties panel, with an Open on GitHub link. [#148](https://github.com/caseyg/caseyagollan.com/pull/148)
* The edit page streams in behind a skeleton and finds the post's file with one GitHub request instead of about 40. Edit links on index pages no longer disappear when a session expires, and the Syndicate link goes to the right place. [#149](https://github.com/caseyg/caseyagollan.com/pull/149)
* Redesigned the syndicate page to match the editor: one shared draft with destination chips, and a compact list of where the post already lives. Bluesky links saved as a DID and as a handle now count as the same post, so they no longer show twice. [#153](https://github.com/caseyg/caseyagollan.com/pull/153)
* Syndication editor on each post, writing links back to GitHub. Syndication drafts link to the Bluesky/Mastodon posts they mention, with live counts. [#90](https://github.com/caseyg/caseyagollan.com/pull/90) [#135](https://github.com/caseyg/caseyagollan.com/pull/135) [#136](https://github.com/caseyg/caseyagollan.com/pull/136)
* Sign-in fixes: native IndieAuth callbacks for Quill on iOS, streamlined passkey sign-in, correct token scope selection, and names for personal tokens. [#132](https://github.com/caseyg/caseyagollan.com/pull/132) [#133](https://github.com/caseyg/caseyagollan.com/pull/133) [#134](https://github.com/caseyg/caseyagollan.com/pull/134)
* Private Readwise review queue for batch-importing bookmarks, with editable summaries, tags, and import receipts. [#103](https://github.com/caseyg/caseyagollan.com/pull/103) [#111](https://github.com/caseyg/caseyagollan.com/pull/111) [#118](https://github.com/caseyg/caseyagollan.com/pull/118)

## Markdown everywhere

* Converted the 154 posts stored as HTML to Markdown. Each conversion was checked to render the same HTML; a full build matched on 1,883 of 1,889 pages. Saved copies of other people's posts stay as fetched. [content#16](https://github.com/caseyg/caseyagollan-content/pull/16)
* Bluesky and Mastodon imports are saved as Markdown whenever it renders the same post, and the edit page saves HTML posts back as Markdown. [#138](https://github.com/caseyg/caseyagollan.com/pull/138) [#148](https://github.com/caseyg/caseyagollan.com/pull/148)

## Notes & Posts

<figure class="align-right narrow"><img src="https://files.caseyagollan.com/publishing/2026/11/98942bc2-0f0d-490f-a9ef-7db31e00fed1.webp" alt="A Bluesky note on a phone: emoji-only nav in the corner, a Posts / 2026 / 11 / 14 trail, the note with a linked mention and shortened link, and a link card with a painting, the site name, title and description."><figcaption><a href="https://caseyagollan.com/2026/11/14/3n2cde25cgc2m/">An imported Bluesky note</a> with its mention linked and its link card saved.</figcaption></figure>

* Imported the public Bluesky and Mastodon archive backlog, about 1,100 posts, with deduplication, real activity timestamps, and privacy checks. Locked accounts and Bluesky public-access opt-outs are left out. [#99](https://github.com/caseyg/caseyagollan.com/pull/99) [#100](https://github.com/caseyg/caseyagollan.com/pull/100) [content#7](https://github.com/caseyg/caseyagollan-content/pull/7)
* Imported Bluesky posts render their links, profile-linked mentions, and link cards, instead of plain text with the URL repeated underneath. Re-rendered the existing imports. [#142](https://github.com/caseyg/caseyagollan.com/pull/142) [content#15](https://github.com/caseyg/caseyagollan-content/pull/15)
* Saved social cards now include photo galleries, link cards, quoted posts, and images copied to R2. [#84](https://github.com/caseyg/caseyagollan.com/pull/84) [#87](https://github.com/caseyg/caseyagollan.com/pull/87) [#104](https://github.com/caseyg/caseyagollan.com/pull/104)
* Likes and reposts of the same thing roll up into one entry on indexes, across networks and dates. Bluesky thread likes, reposts, and replies group into a shared thread card that links to its day archive. [#106](https://github.com/caseyg/caseyagollan.com/pull/106) [#129](https://github.com/caseyg/caseyagollan.com/pull/129) [#131](https://github.com/caseyg/caseyagollan.com/pull/131) [#139](https://github.com/caseyg/caseyagollan.com/pull/139)
* Replies use the shared post card, with the parent post and usernames condensed above. [#115](https://github.com/caseyg/caseyagollan.com/pull/115) [#119](https://github.com/caseyg/caseyagollan.com/pull/119) [#121](https://github.com/caseyg/caseyagollan.com/pull/121) [#122](https://github.com/caseyg/caseyagollan.com/pull/122)

<figure class="align-right narrow"><img src="https://files.caseyagollan.com/publishing/2026/11/b9cb999f-40fb-469f-9f6f-ef68c69cf9a4.webp" alt="On a phone, the Posts trail and a Filter button reading 2 selected, above pills for Notes 73, Articles 4, Bookmarks 11, Photos 37, Videos 3, Replies 65, Likes 866 and Reposts 159, with Notes and Photos filled and a Clear link."><figcaption><a href="https://caseyagollan.com/posts/filter?types=notes,photos">Notes and photos only</a>, with each type's count.</figcaption></figure>

* Post type filters on the feed, date, tag, and type pages. A Filter button opens a pill for each type, with its emoji and count; pick any combination to show only those. Filtered feeds have shareable URLs and page through matching posts only. [#151](https://github.com/caseyg/caseyagollan.com/pull/151)
* Pagination on the posts index. [#109](https://github.com/caseyg/caseyagollan.com/pull/109)

## Navigation & Search

<figure class="align-right narrow"><img src="https://files.caseyagollan.com/publishing/2026/11/baf5fb92-4acb-4d91-8f00-56666662e483.webp" alt="The 404 page on a phone: the emoji nav in the corner, a Casey Gollan · 404 trail, the heading Nothing at this address, a sentence naming the missing path /nope-xyz, and a blue button group for Home, Library and Posts."><figcaption>The nav, the trail, and the new 404 page.</figcaption></figure>

* Redesigned the sitewide navigation around one button-group style. The top right is always Home, Library, Posts, and Search, in that order, with the current section in darker blue. The top left is a trail of where you are, such as Posts · 2026 · 11 · 14, where each segment links up a level. On phones the nav shrinks to emoji. [#151](https://github.com/caseyg/caseyagollan.com/pull/151)
* New 404 page, replacing SvelteKit's unstyled default. [#151](https://github.com/caseyg/caseyagollan.com/pull/151)
* Site search with Pagefind, covering posts, books, saved social posts, and published [cag.wiki](https://cag.wiki) pages. Book covers and post images in results, catalog and author filters, and authors sorted by surname. Wiki pages with spaces in their names are indexed now too. [#85](https://github.com/caseyg/caseyagollan.com/pull/85) [#92](https://github.com/caseyg/caseyagollan.com/pull/92) [#101](https://github.com/caseyg/caseyagollan.com/pull/101) [#102](https://github.com/caseyg/caseyagollan.com/pull/102) [#150](https://github.com/caseyg/caseyagollan.com/pull/150)
* Design tokens and composable UI primitives, with Storybook stories for every site component. [#123](https://github.com/caseyg/caseyagollan.com/pull/123) [#124](https://github.com/caseyg/caseyagollan.com/pull/124)

## Library

<figure class="align-right"><img src="https://files.caseyagollan.com/publishing/2026/11/5b33ab0c-02f9-4def-9aec-a2aded0b0c81.webp" alt="The 2026 library shelf: colored book spines with their titles and author surnames, lined up along their bottom edges."><figcaption>The <a href="https://caseyagollan.com/library?view=shelves">recently acquired shelves</a>.</figcaption></figure>

* The library graph shows up about 3.5x sooner (2.0s instead of 7.0s in testing), and the longest main-thread stall dropped from 3.9s to 0.18s. The layout runs once, in a Web Worker, and spines and covers paint in over the next frames. [#147](https://github.com/caseyg/caseyagollan.com/pull/147)
* Book permalinks show the cover at full size straight away, then glide it onto the 3D book once the scene is ready. Sharper covers with truer color, the selected book stays selected when switching views, and shelf arrow keys follow the order the books are drawn in. [#147](https://github.com/caseyg/caseyagollan.com/pull/147)
* Books animate between shelf layouts with a spring. [#125](https://github.com/caseyg/caseyagollan.com/pull/125) [#128](https://github.com/caseyg/caseyagollan.com/pull/128)
* Better mobile browsing: fixed gestures and shelf selection, smoother book permalink loading, and tags as chips. [#116](https://github.com/caseyg/caseyagollan.com/pull/116) [#126](https://github.com/caseyg/caseyagollan.com/pull/126) [#127](https://github.com/caseyg/caseyagollan.com/pull/127)
* Book details render before the graph loads. Open Library descriptions and larger covers are cached in R2. [#105](https://github.com/caseyg/caseyagollan.com/pull/105) [#117](https://github.com/caseyg/caseyagollan.com/pull/117)

## Builds & Previews

* Every pushed branch gets its own Worker Preview URL, with sign-in, publishing, and imports turned off. [#141](https://github.com/caseyg/caseyagollan.com/pull/141)
* Cleared build diagnostics and fixed a navigation layout shift while search loads. [#82](https://github.com/caseyg/caseyagollan.com/pull/82) [#96](https://github.com/caseyg/caseyagollan.com/pull/96)
* Posts can include right-aligned screenshots, like the ones in this post. [#154](https://github.com/caseyg/caseyagollan.com/pull/154)
