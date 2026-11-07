# Content and duplicate handling

This is the canonical Markdown content repository for caseyagollan.com, mounted as
the site's `content/` Git submodule. Keep publishing/import logic and index rendering
in the site repository; do not add a second content copy. Commit content changes
here first, then update the site's submodule pointer. Do not deploy or claim a live
fix based only on a local build.

## Identify before deleting

- Compare parsed `date`, `pesos-source`, `syndication`, `like-of`, and `repost-of`.
  Filenames can contain an old observed date; derive permalinks from the document's
  local date and slug, not the filename date alone. Preserve local time offsets.
- Match site permalinks and syndication URLs first. Mastodon author-origin and
  federated instance URLs can use different IDs for the same post; use saved
  snapshot `url`/`sourceUrl` or a public status lookup. Bluesky handles and DIDs can
  refer to the same actor. Do not equate unrelated actors by matching post IDs.
- For authored cross-network posts, compare normalized text (HTML entities,
  whitespace, and actual link destinations), posting times, and all media. A
  matching short caption or article URL alone is insufficient evidence to delete.
  Network copies can re-encode/resize photos: compare the actual images, count,
  order, and alt text rather than assuming different CDN URLs mean different media.
- Keep intentional repeated posts and different commentary. Do not use fuzzy text
  similarity to delete automatically. Do not present a liked post's publication
  time as a known action timestamp. When only that fallback is available, retain
  `pesos-date-source: original-post` and label its provenance in source lists.

## Index rollups versus duplicate records

- A like and repost are distinct activities. Keep their records, dates, source IDs,
  target relationships, saved snapshots, and individual permalinks.
- The site groups reactions by canonical target or the saved shared article URL
  (`_micropubSocialSnapshots[].preview.url`). Several people/networks can share the
  same article with different remote captions. Render one preview in indexes with
  links to every activity; do not rewrite those distinct sources into one authored
  post. Different commentary/media written on Casey's site remains separate.
- Group across networks, repeated action kinds, and dates within the displayed
  index. Place a combined entry under its latest activity's local date. Day/month/
  year/type/tag views only group the records included in that view. Preserve
  meaningful URL query parameters; remove only known tracking parameters/fragments.
- Example: July 12–13, 2026 reactions to `https://www.wrecka.ge/holdfast-0-situating/`
  include Mastodon and Bluesky, several reposts, and a like on another day. These
  belong in one index group, not four deleted activity records.

## Clean up confirmed duplicate authored posts

1. Prefer the original site-authored record; otherwise retain the earliest verified
   authored copy. Preserve its body, original date, media, slug, and permalink.
2. Merge every removed copy's `syndication` URL and `pesos-source` ID into the retained
   original. Preserve useful tags/alt text/metadata. This bookkeeping prevents both
   current polling and archive retries from recreating the removed copies.
3. Delete only confirmed redundant records. Keep unrelated likes/reposts. Review
   existing links and redirect needs before changing a published permalink.
4. Inspect the diff, parse all affected Markdown, and run site tests, type checks,
   production build, and post/date/tag index checks. Verify original permalinks,
   consolidated previews, and all activity links. Verify deployed routes separately
   before reporting a production cleanup as complete.

## Polling and POSSE

- PESOS imports must not request automatic outbound syndication. Imported documents
  carry `pesos-source`; the site excludes them from automatic POSSE destinations,
  including after snapshot refreshes. Keep send receipts/idempotency bookkeeping.
- Skip self-likes/reposts targeting an existing site permalink or syndicated copy.
  Keep likes/reposts of other people's content, even across networks; roll them up
  for display instead of losing their separate action identities.
- The live poller and archive importer can consolidate authored text-only copies
  only with one unambiguous imported original, exact substantial text/link content,
  different source networks, matching summary, and timestamps within 24 hours.
  Keep the existing canonical path/date during automatic consolidation. Add the new
  source ID and syndication URL atomically; never silently skip without recording
  those identities. Short captions, re-encoded media, replies, same-network repeats,
  and ambiguous matches require review. Never collapse different posts merely
  because they link to the same article.
- Polling writes must compare against the Git HEAD used to build the index; advance
  checkpoints only after content/bookkeeping commits succeed. Dry runs must not
  commit content or advance cursors. Check retry/conflict cases when changing this.
