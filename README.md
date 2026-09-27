<h1 align="center">Big tech system design</h1>
<p align="center"><i>How big companies actually build their systems: high-level and low-level architecture breakdowns, with diagrams and sources.</i></p>
<p align="center">Inspired by "System Design in 60 Seconds" short videos (e.g. <a href="https://youtube.com/shorts/xMlsVPH_SWA">TechPrep: Uber</a>). Last reviewed: September 2026.</p>

**Why this repo:** most system design material is either generic ("design Twitter") or a single blog post. Here, every design is traced back to what the company actually published, every number has a source, every claim was fact-checked against that source, and each company is paired with concept explainers, practice questions and interview walkthroughs.

## Table of contents

* [How to read this repo](#how-to-read-this-repo)
* [Learning path](#learning-path)
* [Companies](#companies)
* [Comparisons](#comparisons)
* [Concepts](#concepts)
* [Interview problems](#interview-problems)
* [Common building blocks](#common-building-blocks)
* [Engineering blogs](#engineering-blogs)
* [Learning resources](#learning-resources)
* [Contributing](#contributing)

---

## How to read this repo

Each company page follows the same layout ([TEMPLATE.md](TEMPLATE.md)):

1. **Before you read: design it yourself**: 4 questions to try first, with hidden hints and answers.
2. **In 60 seconds**: the short-video version.
3. **The problem**: one real user action and what has to happen in the next few seconds.
4. **Scale**: real numbers, each one linked to a source.
5. **Back-of-the-envelope math**: worked whiteboard estimates (requests per second, storage per day) built from those numbers.
6. **How it evolved**: what broke at each stage and what replaced it.
7. **High-level design (HLD)**: the big boxes: apps, gateways, services, queues, databases.
8. **Low-level design (LLD)**: one core request traced step by step (sequence diagram), the data model, and the one clever component that makes it work.
9. **Deep dives** and **What happens when things break**: the key technologies, and real outages.
10. **Key design decisions** and **Interview takeaways**: why they chose it, what they gave up, and what to reuse.
11. **Glossary**: every jargon word in plain English, linked to the [concept pages](concepts/README.md).

Diagrams are written in [Mermaid](https://mermaid.js.org/), which GitHub draws automatically. Where a company hasn't published the details, the page says so and labels the diagram as a simplified reference design.

Short on time? Every company also has a one-page **cheat sheet** (linked in the table below): the summary, one diagram, key numbers and a ready-made interview answer outline.

<p align="right"><a href="#table-of-contents"><b>↥ Back to top</b></a></p>

## Learning path

New to system design? Read in this order. Each stage adds one big idea on top of the last, and ends with a comparison page that ties the stage together.

| Stage | Big idea | Read | Then compare |
|---|---|---|---|
| 1. Storing lots of data | One database is not enough: caching, sharding, unique IDs | [Instagram](companies/instagram.md), [Twitter / X](companies/twitter-x.md) | [Databases and sharding](comparisons/databases-and-sharding.md), [Feeds and fan-out](comparisons/feeds-and-fan-out.md) |
| 2. Real-time connections | Keeping millions of connections open and pushing messages instantly | [WhatsApp](companies/whatsapp.md), [Slack](companies/slack.md), [Discord](companies/discord.md) | [Real-time messaging](comparisons/real-time-messaging.md) |
| 3. Big files and media | Moving huge files: chunking, encoding, CDNs | [Dropbox](companies/dropbox.md), [YouTube](companies/youtube.md), [Netflix](companies/netflix.md), [Spotify](companies/spotify.md) | [Media delivery](comparisons/media-delivery.md) |
| 4. Marketplaces and location | Matching two sides of a market, searching by place | [Uber](companies/uber.md), [Airbnb](companies/airbnb.md) | [Monolith to microservices](comparisons/monolith-to-microservices.md) |
| 5. Correctness and money | When a bug means someone gets charged twice | [Stripe](companies/stripe.md) | [Money and correctness](comparisons/money-and-correctness.md) |

<p align="right"><a href="#table-of-contents"><b>↥ Back to top</b></a></p>

## Companies

| Company | Problem it solves | Signature ideas | Cheat sheet |
|---|---|---|---|
| [Uber](companies/uber.md) | Match riders to nearby drivers in seconds | H3 hex geo-index, DISCO dispatch, Ringpop | [1 page](cheatsheets/uber.md) |
| [Netflix](companies/netflix.md) | Stream video to hundreds of millions of screens | Open Connect CDN, microservices on AWS, per-title encoding | [1 page](cheatsheets/netflix.md) |
| [YouTube](companies/youtube.md) | Upload, transcode and serve video at planet scale | Transcode pipeline, Vitess, global edge caching | [1 page](cheatsheets/youtube.md) |
| [WhatsApp](companies/whatsapp.md) | Deliver billions of encrypted messages a day | Erlang, store-and-forward, Signal protocol | [1 page](cheatsheets/whatsapp.md) |
| [Discord](companies/discord.md) | Real-time chat and voice for huge communities | Elixir gateways, ScyllaDB, Rust data services | [1 page](cheatsheets/discord.md) |
| [Slack](companies/slack.md) | Real-time workplace messaging | Channel/gateway servers, Vitess, Flannel edge cache | [1 page](cheatsheets/slack.md) |
| [Instagram](companies/instagram.md) | Share photos and build a ranked feed | Django at scale, sharded Postgres IDs, Cassandra | [1 page](cheatsheets/instagram.md) |
| [Twitter / X](companies/twitter-x.md) | Build home timelines for hundreds of millions | Fan-out on write, Snowflake IDs, Manhattan | [1 page](cheatsheets/twitter-x.md) |
| [Spotify](companies/spotify.md) | Stream music and recommend what's next | Backstage, GCP event delivery, Discover Weekly | [1 page](cheatsheets/spotify.md) |
| [Airbnb](companies/airbnb.md) | Search, rank and book homes | Monolith to SOA, search ranking, availability calendar | [1 page](cheatsheets/airbnb.md) |
| [Stripe](companies/stripe.md) | Move money through an API safely | Idempotency keys, DocDB, ledger, rate limiters | [1 page](cheatsheets/stripe.md) |
| [Dropbox](companies/dropbox.md) | Sync files across devices reliably | Magic Pocket, Nucleus sync engine, block dedupe | [1 page](cheatsheets/dropbox.md) |

<p align="right"><a href="#table-of-contents"><b>↥ Back to top</b></a></p>

## Comparisons

Same problem, different companies. These pages put the answers side by side, which is where the patterns become obvious.

| Page | Compares |
|---|---|
| [Real-time messaging](comparisons/real-time-messaging.md) | WhatsApp, Discord, Slack |
| [Feeds and fan-out](comparisons/feeds-and-fan-out.md) | Twitter / X, Instagram (Discord, Slack as contrast) |
| [Media delivery](comparisons/media-delivery.md) | Netflix, YouTube, Spotify, Instagram |
| [Databases and sharding](comparisons/databases-and-sharding.md) | Instagram, Slack, YouTube, Discord, Uber, Stripe, Dropbox, Twitter / X, Airbnb |
| [Monolith to microservices](comparisons/monolith-to-microservices.md) | Airbnb, Twitter / X, Uber, Netflix, Instagram, Spotify |
| [Money and correctness](comparisons/money-and-correctness.md) | Stripe, Airbnb, Uber |

<p align="right"><a href="#table-of-contents"><b>↥ Back to top</b></a></p>

## Concepts

The building blocks every company page relies on, each explained from zero: the problem it solves, how it works (with diagrams), variants, where the companies here use it, common mistakes and interview questions. See the [concepts index](concepts/README.md).

| Group | Pages |
|---|---|
| Storing and finding data | [Caching](concepts/caching.md), [Sharding](concepts/sharding.md), [Replication](concepts/replication.md), [Consistent hashing](concepts/consistent-hashing.md), [Geo-indexing](concepts/geo-indexing.md) |
| Consistency and correctness | [CAP theorem and consistency](concepts/cap-and-consistency.md), [Idempotency](concepts/idempotency.md) |
| Talking between services | [Message queues and logs](concepts/message-queues-and-logs.md), [Fan-out](concepts/fan-out.md), [Persistent connections](concepts/persistent-connections.md) |
| Handling traffic | [CDN](concepts/cdn.md), [Load balancing](concepts/load-balancing.md), [Rate limiting](concepts/rate-limiting.md) |
| System shape | [Microservices](concepts/microservices.md) |

<p align="right"><a href="#table-of-contents"><b>↥ Back to top</b></a></p>

## Interview problems

The classic system design interview questions, walked through in the order you'd answer them in a 45-minute interview: clarify, estimate, API, data model, high-level design, deep dives, failure modes, and a 2-minute summary. Each one links to the real company that solved the same hard part. See the [problems index](problems/README.md).

| Problem | Difficulty | Real-world reference |
|---|---|---|
| [URL shortener](problems/url-shortener.md) | Beginner | [Instagram](companies/instagram.md) |
| [Rate limiter](problems/rate-limiter.md) | Beginner to intermediate | [Stripe](companies/stripe.md) |
| [News feed](problems/news-feed.md) | Intermediate | [Twitter / X](companies/twitter-x.md) |
| [Chat app](problems/chat-app.md) | Intermediate to advanced | [WhatsApp](companies/whatsapp.md) |
| [Ride hailing](problems/ride-hailing.md) | Advanced | [Uber](companies/uber.md) |
| [File sync](problems/file-sync.md) | Advanced | [Dropbox](companies/dropbox.md) |
| [Video streaming](problems/video-streaming.md) | Advanced | [Netflix](companies/netflix.md), [YouTube](companies/youtube.md) |
| [Payment system](problems/payment-system.md) | Advanced | [Stripe](companies/stripe.md) |

<p align="right"><a href="#table-of-contents"><b>↥ Back to top</b></a></p>

## Common building blocks

The same ideas show up again and again. Learn these once and every page gets easier.

| Building block | Plain English | Seen at |
|---|---|---|
| [Load balancer](concepts/load-balancing.md) | A traffic cop that spreads requests across many servers | Everyone |
| [CDN (content delivery network)](concepts/cdn.md) | Copies of files kept in servers near users, so downloads are short trips | Netflix, YouTube, Spotify, Instagram |
| [Cache](concepts/caching.md) | A fast short-term memory in front of a slow database | Everyone |
| [Message queue / log (Kafka)](concepts/message-queues-and-logs.md) | A waiting line of events, so one service can hand work to another without waiting | Uber, Netflix, Spotify, Slack |
| [Sharding](concepts/sharding.md) | Splitting one big database into pieces by some key (user, region) | Instagram, Slack, Discord, YouTube |
| [Replication](concepts/replication.md) | Keeping copies of data on several machines so one crash loses nothing | Everyone |
| [Fan-out](concepts/fan-out.md) | Copying one event (a tweet, a message) to many receivers | Twitter/X, Discord, Slack, WhatsApp |
| [Idempotency](concepts/idempotency.md) | Making "do it twice" have the same result as "do it once", so retries are safe | Stripe, Uber |
| [WebSocket / persistent connection](concepts/persistent-connections.md) | A phone line held open so the server can push updates instantly | WhatsApp, Discord, Slack, Uber |
| [Geo-index](concepts/geo-indexing.md) | A map split into cells so "who's near me" is a quick lookup | Uber, Airbnb |
| [Microservices](concepts/microservices.md) | Many small apps, each owning one job, instead of one giant app | Netflix, Uber, Spotify, Airbnb |

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
