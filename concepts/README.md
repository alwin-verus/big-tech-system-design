# Concepts

Plain-English explanations of the recurring building blocks behind the [company deep dives](../companies/) in this repo. Each page explains the idea like you're five, then goes deeper: how it works, when to use which variant, where the companies here actually use it, common mistakes, and interview questions.

New to the basics underneath these? The companion glossary has beginner deep dives on [API styles](https://github.com/alwintwk/dev-knowledge/blob/main/topics/api-styles.md), [authentication and authorization](https://github.com/alwintwk/dev-knowledge/blob/main/topics/auth.md), and [databases](https://github.com/alwintwk/dev-knowledge/blob/main/topics/databases.md).

## Storing and finding data

- [Caching](caching.md) — keeping a copy of data somewhere faster to reach than where it really lives.
- [Sharding](sharding.md) — splitting one big database into smaller pieces so no single machine holds it all.
- [Replication](replication.md) — keeping more than one copy of data so losing one machine doesn't lose the data.
- [Consistent hashing](consistent-hashing.md) — assigning keys to servers so adding/removing one server only moves a small slice of keys.
- [Geo-indexing](geo-indexing.md) — organizing location data so "what's nearby" is a fast lookup, not raw geometry.

## Consistency and correctness

- [CAP theorem and consistency](cap-and-consistency.md) — why a system split by a network partition must choose between a fast answer and a guaranteed-correct one.
- [Idempotency](idempotency.md) — making a request safe to retry so it never runs twice by accident.

## Talking between services

- [Message queues and logs](message-queues-and-logs.md) — handing off work asynchronously instead of making the caller wait.
- [Fan-out](fan-out.md) — delivering one event to many recipients without the delivery itself becoming the bottleneck.
- [Persistent connections](persistent-connections.md) — keeping a connection open so the server can push updates instantly, instead of the client repeatedly asking.

## Handling traffic

- [CDN](cdn.md) — caching content at servers close to users around the world.
- [Load balancing](load-balancing.md) — spreading requests evenly across a pool of servers.
- [Rate limiting](rate-limiting.md) — capping how much one caller can use so it can't starve everyone else.

## System shape

- [Microservices](microservices.md) — splitting one application into many small, independently deployable services.
