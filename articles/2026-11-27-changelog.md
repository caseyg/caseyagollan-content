---
date: 2026-11-27T17:30:00-05:00
title: 2026-11-27 Changelog
summary: Live cursors and cursor chat on every page. The site is now an MCP
  server, so Claude can search it, read my saves, and open a table as a live
  canvas. The chat gained skills, a model switcher, archiving, and one call
  that maps everything I saved in a week onto a table. The site keeps a
  private, searchable copy of my Readwise, Raindrop and Are.na.
category: changelog
draft: false
---

## Live cursors

<figure class="align-right"><img src="https://files.caseyagollan.com/publishing/2026/11/c705fd9c-c1bc-43e4-b7be-96b6451b6fdc.webp" alt="A post with a video, and two other visitors' cursors over it: a green one with a bubble reading hello from the other browser, and a pink one reading hi Casey with a waving hand."><figcaption>Two visitors on the same page, chatting by their cursors.</figcaption></figure>

* Everyone on the same page sees everyone else's pointer, each in a color of its own. Press **C** to type a short message in a bubble by your cursor, which others see as it's typed. A gray "others here" button shows when someone else is on the page. [#229](https://github.com/caseyg/caseyagollan.com/pull/229)
* On phones and tablets you see others without showing a cursor yourself. ⌘K can hide live cursors, and they stay off my own tools like the composer and account page. [#229](https://github.com/caseyg/caseyagollan.com/pull/229)

## The site as a Claude connector

* `https://caseyagollan.com/mcp` is the site as a remote MCP server, signed in to through the site's own IndieAuth. Claude gets the same tools as the site's chat: search, read pages, view images, my saves, posts through Micropub, and tables. [#281](https://github.com/caseyg/caseyagollan.com/pull/281)
* A table opens inside Claude as the live canvas, with the site's own toolbar and Add menu, and Claude's table tools change it while I watch. [#284](https://github.com/caseyg/caseyagollan.com/pull/284)
* Links to a table from the connector carry a short-lived pass, so a draft table opens in a browser that can't use my passkey. A pass covers that one table and can't publish, see other drafts or use the chat. [#287](https://github.com/caseyg/caseyagollan.com/pull/287)

## Chat

<figure class="align-right narrow"><img src="https://files.caseyagollan.com/publishing/2026/11/2f52ecfa-414c-4004-8ddf-9af666e75ede.webp" alt="The chat composer with a slash typed and a menu beneath it listing skill-creator, find-skills and link-roundup, each with a one-line description, and a Manage skills link."><figcaption>Typing <code>/</code> lists the chat's skills.</figcaption></figure>

* Skills: saved instructions in the [Agent Skills](https://agentskills.io/specification) shape. Typing `/` in the composer opens a menu of them, and the assistant also picks one by its description. A manager on the account page turns skills on and off, writes, uploads, edits and exports them, and finds published ones on skills.sh. A skill installed from the chat lands on a review card first. [#268](https://github.com/caseyg/caseyagollan.com/pull/268)

<figure class="align-right narrow"><img src="https://files.caseyagollan.com/publishing/2026/11/e913a79b-e5c5-492e-8feb-91797d2afe29.webp" alt="The Model menu open from the chat composer on a phone: GLM Flash and GLM 5.3 under inference.coop, then Claude Haiku 5.5, Claude Sonnet 5.5 with a check mark, and Claude Opus 5.5 under Anthropic, each with a short note."><figcaption>Each chat picks its own model.</figcaption></figure>

* A Model menu in the composer picks the model per chat, from a registry of providers: inference.coop, Anthropic and Cerebras. [#279](https://github.com/caseyg/caseyagollan.com/pull/279)
* Archive and delete chats, from a ⋯ menu on each chat, the open chat's trail, or ⌘K. Archived chats live on their own page and still turn up in search. [#277](https://github.com/caseyg/caseyagollan.com/pull/277)
* A new chat from `/chat` opens the moment Send is pressed, with the thread made in the background. [#274](https://github.com/caseyg/caseyagollan.com/pull/274)
* Fixed the errors behind a table that never got built: the chat can start a table when none is open, a cut-off reply carries on, and it no longer claims its own tools are missing. Readwise sign-in asks for the scopes the service lists. [#272](https://github.com/caseyg/caseyagollan.com/pull/272) [#278](https://github.com/caseyg/caseyagollan.com/pull/278)

## Saves & Tables

<figure class="align-right"><img src="https://files.caseyagollan.com/publishing/2026/11/26e709fd-a461-401b-b827-fa8286fca339.webp" alt="A table titled This week in Readwise: dozens of small cards with pictures and blue quote blocks set out as a round network, with thin lines from each to a hub in the middle."><figcaption>A week of Readwise saves, mapped in one call.</figcaption></figure>

* "Make a canvas with everything I saved to Readwise this week" is one step for the chat. It gathers what was saved across Readwise, Are.na, Raindrop and the site's posts, links related items, picks a quote and a picture for each, and lays the result out as a network. [#282](https://github.com/caseyg/caseyagollan.com/pull/282)

<figure class="align-right narrow"><img src="https://files.caseyagollan.com/publishing/2026/11/8c600f3c-2e40-456d-8b56-346274deb9e6.webp" alt="The Saved copies panel on the account page: a paragraph explaining the private copy, then progress bars for Readwise, Raindrop and Are.na with item counts and how far each sync has got."><figcaption>Each source shows how far its copy has got.</figcaption></figure>

* The site keeps its own private, full-text copy of what I save on Readwise (whole documents and every highlight), Raindrop and Are.na. The chat searches that copy in one call instead of asking each service in turn. Only I can read it. [#283](https://github.com/caseyg/caseyagollan.com/pull/283)
* Live progress bars for each source on the account page, and a sync that runs in the background in small steps so it can't be cut off or run out of memory. [#285](https://github.com/caseyg/caseyagollan.com/pull/285) [#288](https://github.com/caseyg/caseyagollan.com/pull/288)
* ⌘K on tables lists every table and searches the words on them. Choosing a result opens the table with that block selected and in view. [#280](https://github.com/caseyg/caseyagollan.com/pull/280)

## Publishing

<figure class="align-right narrow"><img src="https://files.caseyagollan.com/publishing/2026/11/200ec328-c2ed-4960-af1b-f6957e1750b0.webp" alt="The composer's Drafts menu on a phone, with Save draft and Publish above it: under In the content repository, the 2026-11-25 Changelog on pull request 21 and an older post marked draft."><figcaption>The last changelog, waiting as a draft on its pull request.</figcaption></figure>

* The Drafts menu on `/new` also lists drafts in the content repository, on the published branch and on open pull requests. They open in the post editor, which shows Save draft and Publish. Publishing a pull request's draft merges it. [#275](https://github.com/caseyg/caseyagollan.com/pull/275)
* Mastodon posting connects with OAuth from the account page, the way Bluesky does, with the saved token as a fallback. [#273](https://github.com/caseyg/caseyagollan.com/pull/273)

## Navigation & Design

<figure class="align-right narrow"><img src="https://files.caseyagollan.com/publishing/2026/11/9cacdbf8-c654-4478-93d2-284787062ed2.webp" alt="The homepage section menu open: a Casey Gollan button with a divider and an upturned chevron in its own segment, above a list of Casey Gollan, Currently and Exploring."><figcaption>Menu buttons are split buttons now.</figcaption></figure>

* Menu buttons draw as split buttons: the label, a divider, and a chevron that turns over while the menu is open. [#286](https://github.com/caseyg/caseyagollan.com/pull/286)
* A 👤 account button in the nav before Search, shown only while I'm signed in. [#289](https://github.com/caseyg/caseyagollan.com/pull/289)
* Simplified with built-in platform features: `Intl.RelativeTimeFormat` for relative dates, the browser's own passkey JSON methods in place of a library, and newer JavaScript built-ins. Agents working on the site get a modern web guidance skill. [#276](https://github.com/caseyg/caseyagollan.com/pull/276)
