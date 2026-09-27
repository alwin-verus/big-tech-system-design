<h1 align="center">Big tech system design</h1>
<p align="center"><i>How big companies actually build their systems: high-level and low-level architecture breakdowns, with diagrams and sources.</i></p>
<p align="center">Inspired by "System Design in 60 Seconds" short videos (e.g. <a href="https://youtube.com/shorts/xMlsVPH_SWA">TechPrep: Uber</a>). Last reviewed: September 2026.</p>

## Table of contents

* [How to read this repo](#how-to-read-this-repo)
* [Companies](#companies)
* [Common building blocks](#common-building-blocks)
* [Engineering blogs](#engineering-blogs)
* [Learning resources](#learning-resources)
* [Contributing](#contributing)

---

## How to read this repo

Each company page follows the same layout ([TEMPLATE.md](TEMPLATE.md)):

1. **In 60 seconds**: the short-video version.
2. **Scale**: real numbers, each one linked to a source.
3. **High-level design (HLD)**: the big boxes: apps, gateways, services, queues, databases.
4. **Low-level design (LLD)**: one core request traced step by step (sequence diagram), the data model, and the one clever component that makes it work.
5. **Key design decisions**: why they chose it, and what they gave up.
6. **Glossary**: every jargon word in plain English.

Diagrams are written in [Mermaid](https://mermaid.js.org/), which GitHub draws automatically. Where a company hasn't published the details, the page says so and labels the diagram as a simplified reference design.

<p align="right"><a href="#table-of-contents"><b>↥ Back to top</b></a></p>

## Companies

| Company | Problem it solves | Signature ideas |
|---|---|---|
| [Uber](companies/uber.md) | Match riders to nearby drivers in seconds | H3 hex geo-index, DISCO dispatch, Ringpop |
| [Netflix](companies/netflix.md) | Stream video to hundreds of millions of screens | Open Connect CDN, microservices on AWS, per-title encoding |
| [YouTube](companies/youtube.md) | Upload, transcode and serve video at planet scale | Transcode pipeline, Vitess, global edge caching |
| [WhatsApp](companies/whatsapp.md) | Deliver billions of encrypted messages a day | Erlang, store-and-forward, Signal protocol |
| [Discord](companies/discord.md) | Real-time chat and voice for huge communities | Elixir gateways, ScyllaDB, Rust data services |
| [Slack](companies/slack.md) | Real-time workplace messaging | Channel/gateway servers, Vitess, Flannel edge cache |
| [Instagram](companies/instagram.md) | Share photos and build a ranked feed | Django at scale, sharded Postgres IDs, Cassandra |
| [Twitter / X](companies/twitter-x.md) | Build home timelines for hundreds of millions | Fan-out on write, Snowflake IDs, Manhattan |
| [Spotify](companies/spotify.md) | Stream music and recommend what's next | Backstage, GCP event delivery, Discover Weekly |
| [Airbnb](companies/airbnb.md) | Search, rank and book homes | Monolith to SOA, search ranking, availability calendar |
| [Stripe](companies/stripe.md) | Move money through an API safely | Idempotency keys, DocDB, ledger, rate limiters |
| [Dropbox](companies/dropbox.md) | Sync files across devices reliably | Magic Pocket, Nucleus sync engine, block dedupe |

<p align="right"><a href="#table-of-contents"><b>↥ Back to top</b></a></p>

## Common building blocks

The same ideas show up again and again. Learn these once and every page gets easier.

| Building block | Plain English | Seen at |
|---|---|---|
| Load balancer | A traffic cop that spreads requests across many servers | Everyone |
| CDN (content delivery network) | Copies of files kept in servers near users, so downloads are short trips | Netflix, YouTube, Spotify, Instagram |
| Cache | A fast short-term memory in front of a slow database | Everyone |
| Message queue / log (Kafka) | A waiting line of events, so one service can hand work to another without waiting | Uber, Netflix, Spotify, Slack |
| Sharding | Splitting one big database into pieces by some key (user, region) | Instagram, Slack, Discord, YouTube |
| Replication | Keeping copies of data on several machines so one crash loses nothing | Everyone |
| Fan-out | Copying one event (a tweet, a message) to many receivers | Twitter/X, Discord, Slack, WhatsApp |
| Idempotency | Making "do it twice" have the same result as "do it once", so retries are safe | Stripe, Uber |
| WebSocket / persistent connection | A phone line held open so the server can push updates instantly | WhatsApp, Discord, Slack, Uber |
| Geo-index | A map split into cells so "who's near me" is a quick lookup | Uber, Airbnb |
| Microservices | Many small apps, each owning one job, instead of one giant app | Netflix, Uber, Spotify, Airbnb |

<p align="right"><a href="#table-of-contents"><b>↥ Back to top</b></a></p>

## Engineering blogs

| Company | Blog |
|---|---|
| Uber | [uber.com/blog/engineering](https://www.uber.com/blog/engineering/) |
| Netflix | [netflixtechblog.com](https://netflixtechblog.com/) |
| Meta (Instagram, WhatsApp) | [engineering.fb.com](https://engineering.fb.com/) |
| Discord | [discord.com/category/engineering](https://discord.com/category/engineering) |
| Slack | [slack.engineering](https://slack.engineering/) |
| X / Twitter | [blog.x.com/engineering](https://blog.x.com/engineering/en_us) |
| Spotify | [engineering.atspotify.com](https://engineering.atspotify.com/) |
| Airbnb | [medium.com/airbnb-engineering](https://medium.com/airbnb-engineering) |
| Stripe | [stripe.com/blog/engineering](https://stripe.com/blog/engineering) |
| Dropbox | [dropbox.tech](https://dropbox.tech/) |

<p align="right"><a href="#table-of-contents"><b>↥ Back to top</b></a></p>

## Learning resources

| Name | Description |
|---|---|
| [TechPrep](https://www.youtube.com/@TechPrepYT) | Short "System Design in 60 Seconds" videos. |
| [ByteByteGo](https://bytebytego.com/) | Visual system design explainers and newsletter. |
| [The System Design Primer](https://github.com/donnemartin/system-design-primer) | The classic free guide to large-scale system design. |
| [Designing Data-Intensive Applications](https://dataintensive.net/) | The book on databases, replication and streams. |
| [High Scalability](https://highscalability.com/) | Long-running archive of real-world architecture write-ups. |
| [InfoQ](https://www.infoq.com/architecture-design/) | Conference talks and articles from engineers at scale. |
| [engineering-blogs](https://github.com/kilimchoi/engineering-blogs) | A list of hundreds of company engineering blogs. |

<p align="right"><a href="#table-of-contents"><b>↥ Back to top</b></a></p>

## Contributing

Add a company by copying [TEMPLATE.md](TEMPLATE.md) into `companies/<name>.md`. Rules: every number needs a source, prefer the company's own engineering blog, and label anything that is a guess as a simplified reference design.
