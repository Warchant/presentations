#### Pattern: Event/Command Sourcing + CQRS

<img src="./event_sourcing.jpeg" />

+++

Does this sound familiar?

1. stores an ordered list of events that modify state in append-only log
2. recovers current state by applying all events from a store
3. current state is always determined by events

+++

Pros:
- solves atomicity problem in event-driven systems
- provides 100% reliable audit log of the changes made to a business entity
- makes it possible to implement temporal queries that determine the state of an entity at any point in time
- business logic units are loosely coupled that exchange events

+++

Cons:
- learning curve
- difficult to query, as you need to recover state of an entity from events. As a result, you have **eventually consistent data** in queries.
- not suitable for systems which depend on external data (e.g. bitcoin price indicator)

+++

CQRS - Command Query Responsibility Segregation

<img src="./cqrs.png" width=500px />
