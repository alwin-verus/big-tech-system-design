# System design interview problems

Classic system design interview questions, each walked through in the order you'd actually tackle it
in a 45-minute interview: clarify requirements, estimate scale, design the API and data model, draw the
high-level design, go deep on the 2-4 hardest parts, then talk failure modes and wrap with a strong
summary. Every problem links out to the real company pages in [`../companies/`](../companies/) that
solved the same hard part at production scale — read those first if you want the "why" behind a
pattern, not just the pattern itself.

Each file also links to the concept pages in `../concepts/` for the underlying building blocks
(caching, sharding, consistent hashing, and so on) — those are reference material shared across every
problem, not specific to any one of them.

## Suggested reading order

New to system design interviews? Read top to bottom — each problem below builds on ideas the previous
one introduced.

| # | Problem | Difficulty | Read this company page first | The one hard part it's really testing |
|---|---|---|---|---|
| 1 | [URL Shortener](url-shortener.md) | Beginner | [Instagram](../companies/instagram.md) | Generating unique IDs across shards without a central bottleneck |
| 2 | [Rate Limiter](rate-limiter.md) | Beginner–Intermediate | [Stripe](../companies/stripe.md) | Layered limits that fail open, shared across a whole fleet |
| 3 | [News Feed](news-feed.md) | Intermediate | [Twitter/X](../companies/twitter-x.md) | Fan-out on write vs. fan-out on read — the celebrity problem |
| 4 | [Chat Application](chat-app.md) | Intermediate–Advanced | [WhatsApp](../companies/whatsapp.md) | Routing a message to whichever server holds the recipient's live connection |
| 5 | [Ride-Hailing Service](ride-hailing.md) | Advanced | [Uber](../companies/uber.md) | Geo-indexing two things that never stop moving, at ~1M+ writes/sec |
| 6 | [File Sync Service](file-sync.md) | Advanced | [Dropbox](../companies/dropbox.md) | Detecting and transferring only the bytes that actually changed |
| 7 | [Video Streaming Service](video-streaming.md) | Advanced | [Netflix](../companies/netflix.md), [YouTube](../companies/youtube.md) | Transcode fan-out plus CDN placement at tens-of-terabits-per-second scale |
| 8 | [Payment System](payment-system.md) | Advanced | [Stripe](../companies/stripe.md) | Idempotency and a double-entry ledger — never double-charge, never lose money |

## Problems by theme

**Getting the fundamentals down** (start here if this is your first pass):
[URL Shortener](url-shortener.md) → [Rate Limiter](rate-limiter.md)

**Fan-out and real-time delivery**:
[News Feed](news-feed.md) → [Chat Application](chat-app.md)

**Data that has to move, physically, at scale**:
[Ride-Hailing Service](ride-hailing.md) → [File Sync Service](file-sync.md) →
[Video Streaming Service](video-streaming.md)

**Correctness matters more than anything else**:
[Payment System](payment-system.md) — read this last; it's the one place in this set where the right
answer is sometimes "reject the request" instead of "make it fast and available."

## How each problem is laid out

Every file follows the same nine sections, in interview order:

1. Clarify requirements — the questions to ask, then the functional/non-functional list you settle on.
2. Back-of-the-envelope estimates — worked math with every assumption labeled as an assumption.
3. API design — endpoints with real request/response examples.
4. Data model — an entity diagram plus why those specific keys were chosen.
5. High-level design — a flowchart, walked through step by step.
6. Deep dives — the 2-4 hardest parts of the problem, each with a diagram where one helps.
7. Bottlenecks and failure modes.
8. How real companies did it — links to the specific pages and headings in `../companies/` that back
   up every claim, plus the relevant `../concepts/` pages.
9. What a strong answer sounds like — an 8-10 bullet summary you could say out loud in about two
   minutes, followed by the common mistakes that separate a weak answer from a strong one.
