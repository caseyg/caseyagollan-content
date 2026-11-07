---
date: 2026-11-06T20:00:00-05:00
title: 2026-11-06 Changelog
summary: Replaced IndieKit with native IndieAuth and Micropub publishing on the
  site. Refreshed the library with 32 more books, readable shelves, better view
  switching, and less texture memory. Added saved cards for Bluesky and Mastodon
  likes/reposts, feeds, and media uploads on the existing files domain. Lots of
  plumbing and cleanup.
category: changelog
draft: false
syndication:
  - https://bsky.app/profile/did:plc:s3fw2giksymfvruno3tvem4k/post/3mzoozs6d4tqh
  - https://social.coop/@caseyg/117572962830652076
---

## Publishing

* Replaced IndieKit with native IndieAuth and Micropub endpoints in the site's existing Cloudflare Worker. Markdown still lives in the content repo, media still lives in R2. No separate publishing app or MongoDB dependency. [#77](https://github.com/caseyg/caseyagollan.com/pull/77)
* Passkey sign-in at `/account`, client authorization with consent and PKCE, scoped tokens, and revocation. Reauthorized both old and new Quill clients against the new endpoints. Stopped the old Railway app after checking the migration; kept its configuration and database for rollback.
* Create, edit, delete, restore, and save drafts through Micropub. Stale edits get rejected instead of overwriting newer changes. Drafts stay out of public pages and feeds, though their Markdown is still visible in the public Git repo.
* Expanded Quill support beyond notes and articles: bookmarks, likes, reposts, replies, RSVPs, photos/video, events, presentations, reviews, itineraries, and food/drink posts. Structured properties render on the site. Markdown stays Markdown; rich HTML is sanitized. [#79](https://github.com/caseyg/caseyagollan.com/pull/79)
* Media uploads go through `/micropub/media` and return URLs on `files.caseyagollan.com`. Consolidated new uploads into the existing R2 bucket, keeping old media URLs working. Image, video, and audio uploads up to 25 MiB; photo alt text survives the round trip. The screenshots in this post were uploaded through the new endpoint. [#78](https://github.com/caseyg/caseyagollan.com/pull/78)
* Added RSS, Atom, and JSON feeds, plus a validated content-sync workflow: publishing to Git triggers checks and a site rebuild.
* Built a durable outbox for outgoing Webmentions and requested Mastodon/Bluesky syndication. It waits for the intended post revision to be public before sending. Outgoing delivery is still disabled pending live send checks.

## Library

* Refreshed from today's LibraryThing export: 510 books, up from 478. Added author and catalog-entry data alongside the new covers. [#73](https://github.com/caseyg/caseyagollan.com/pull/73)
* Made the shelves easier to browse. Better spine text fitting with author surnames, sorting by displayed spine color, year headings for acquisition/publication dates, and acquisition-date fallback to the date added to LibraryThing. [#74](https://github.com/caseyg/caseyagollan.com/pull/74)
* Graph/shelf view and sort order now live in the URL, so a particular arrangement can be bookmarked or shared. Shelf deep links wait for layout initialization before framing the books.
* Shelves fit the screen width and start at the top. Constrained camera panning, kept books draggable, and made selected books pull forward to show their covers. Books now line up along their bottom edges. [#81](https://github.com/caseyg/caseyagollan.com/pull/81)
* Book detail URLs work in the deployed Worker, with catalog details available even when the external lookup fails. Decoded display text instead of showing HTML entities.
* Reduced texture memory: bounded spine textures, plain materials for solid-color backs, and separate mobile budgets for covers and generated textures. Cleaned up animation frames, timeouts, and listeners when leaving the page. [#72](https://github.com/caseyg/caseyagollan.com/pull/72)

![Library shelves with readable book spines, aligned bottom edges, and acquisition-year headings.](https://files.caseyagollan.com/publishing/2026/11/a3113583-eb02-43ad-991e-4f4d8517ce4d.png)

*The [recently acquired shelves](https://caseyagollan.com/library?view=shelves), with books grouped by year.*

## Notes & Posts

* Likes and reposts of Bluesky/Mastodon posts now show saved cards with the author, text, timestamp, and images. Snapshots are captured when publishing; avatars and images are copied into R2. No live embed widget or social API request needed to read the page. If capture fails, the original link still works. [#80](https://github.com/caseyg/caseyagollan.com/pull/80)
* Fixed bookmark titles linking to their external sources, on lists and individual pages. Added a 🔗 and the source URL underneath; untitled bookmarks fall back to the URL. [#67](https://github.com/caseyg/caseyagollan.com/pull/67)
* New post permalinks can load before the next rebuild: the Worker fetches missing posts from GitHub at the same dated URL. Existing built posts, archives, and feeds still update on rebuild. [#68](https://github.com/caseyg/caseyagollan.com/pull/68)
* Excluded drafts from indexes and static pages. Preserved local dates and permalinks through the shared parser. [#70](https://github.com/caseyg/caseyagollan.com/pull/70)

![A saved Bluesky post showing the author, linked text, BumpTop collage, and original timestamp inside a static card.](https://files.caseyagollan.com/publishing/2026/11/3ffa62ce-85cc-46b8-961b-02fb860a13cb.png)

*A [saved Bluesky like](https://caseyagollan.com/2026/11/06/c1d5be8d), with its text and image kept on the site.*

## Builds & Cleanup

* Stopped parsing the same 34 Markdown files 2,448 times during prerendering. Each is parsed once per build; development reads stay fresh. Narrower D3 imports reduced client modules transformed from 902 to 666. Small local build improvements, roughly 0.14 and 0.19 seconds respectively in separate warm-build comparisons. [#69](https://github.com/caseyg/caseyagollan.com/pull/69)
* Removed old Eleventy/generated site copies, the nested starter, duplicate content, backups, and browser screenshots. The content submodule stays canonical; old files remain in Git history.
* Fixed Svelte/TypeScript diagnostics and updated repo guidance for the current Workers setup. Docs, tests, and planning-only changes no longer trigger Cloudflare builds. [#71](https://github.com/caseyg/caseyagollan.com/pull/71)
* Swapped the favicon for the square Sisu photo. [#76](https://github.com/caseyg/caseyagollan.com/pull/76)
