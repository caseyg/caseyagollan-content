---
date: 2025-11-29T19:33:16.917-05:00
title: 2025-11-29 Changelog
summary: Screenshot previews on citation nodes, smoother loading animations, migrated to Cloudflare Workers. Posts got a UI refresh with type icons, date-based permalinks, and restored webmentions. Library page 40% faster.
category: changelog
---

## Graph

* Added screenshot previews for citation nodes—hover to see a browser-window style preview of the source. Using Cloudflare Browser Rendering API, cached in R2.
* "Researching..." loading indicator now cycles through shapes (circle → star → triangle → diamond) with letter-by-letter shimmer.
* Loading nodes attach to their specific topic so you can navigate elsewhere while research continues.
* Fixed graph springing/resetting when screenshots loaded. Was using SvelteMap which triggered reactivity—switched to regular Map.
* Fixed big blue dot appearing when clicking nodes during ping animation. CSS selector wasn't excluding `.ping-ring`.
* Migrated from Cloudflare Pages to Workers for observability. Can actually see logs now.

## Notes & Posts

* Added type icons: 📝 note, 📄 article, 🔖 bookmark, 📸 photo, 🎥 video, 💬 reply.
* Button-like hover states on all metadata links.
* Auto-linking Mastodon (@user@instance) and Bluesky handles.
* Tags display inline with # prefix.
* Date-based permalinks: `/2025/11/29/post-title` with archive pages for year/month/day.
* Restored webmentions with avatar facepiles for likes/reposts, full display for replies.
* Added syndication icons: Mastodon 🐘, Bluesky 🦋, X 🐦.
* Webmention counts (⭐ 🔁 💬) on post lists.

## Library

* Minified graph.json: 543KB → 328KB (40% reduction).
* Texture and material caching in Three.js—shared materials for spines and covers.
* Reusable canvas elements for texture generation.
* Converted to TypeScript with Svelte 5 runes.

## Next

* Right-click context menu for graph nodes—remove, extend cache, recapture screenshots. [#55](https://github.com/caseyg/caseyagollan.com/issues/55)
