# BACKEND DESIGN PATTERNS

### 1. <span style="color:yellow">Core OOP / GoF Design Patterns (Backend-Level Use)</span>

These are classic software development patterns — still used everywhere in backend codebases.

<span style="color:orange">Creational</span>
* Singleton
* Factory Method
* Abstract Factory
* Builder
* Prototype

<span style="color:orange">Structural</span>

* Adapter
* Bridge
* Composite
* Decorator
* Facade
* Flyweight
* Proxy

<span style="color:orange">Behavioral</span>

* Strategy
* Command
* Chain of Responsibility
* Observer
* Template Method
* Iterator
* Mediator
* State
* Memento
* Visitor

`Count: 23 patterns`

#### 2. <span style="color:yellow">Enterprise (Backend) Architectural Patterns</span>

These are NOT GoF patterns. These are high-level architecture principles used in services.

<span style="color:orange">Layered Architecture</span>
* N-tier / Clean / Onion architecture

<span style="color:orange">Component-Based</span>
* Microkernel
* Plugin Architecture

<span style="color:orange">Distributed / Microservices</span>
* Microservices
* Service-Based Architecture
* Self-contained Systems

<span style="color:orange">Communication Patterns</span>
* API Gateway
* Backend-for-Frontend (BFF)
* Gateway Aggregation / Routing
* Circuit Breaker
* Retry Pattern
* Bulkhead Pattern
* Timeout Pattern
* Rate Limiter
* Load Balancer Pattern

<span style="color:orange">Data-Oriented Architecture</span>
* Event Sourcing
* CQRS
* Domain-Driven Design (DDD)
* Table Module
* Active Record
* Data Mapper
* Repository Pattern
* Unit of Work

<span style="color:orange">Deployment / Scaling</span>
* Sidecar Pattern
* Ambassador Pattern
* Adapter/Proxy Pattern (service mesh)
* Strangler Fig Pattern

`Count: ~26 patterns`

### 3. <span style="color:yellow">Integration Patterns (Messaging + Distributed Systems)</span>

These come from enterprise integration, Kafka, RabbitMQ, event-driven systems.

<span style="color:orange">Message Routing</span>
* Message Router
* Content-Based Router
* Message Filter
* Splitter
* Aggregator
* Routing Slip

<span style="color:orange">Messaging Channels</span>
* Point-to-Point Channel
* Pub/Sub Channel
* Dead Letter Queue
* Priority Queue

<span style="color:orange">Message Transformation</span>
* Message Translator
* Envelope Wrapper

<span style="color:orange">Message Construction</span>
* Command Message
* Document Message
* Event Message

<span style="color:orange">Reliability Patterns</span>
* Idempotent Receiver
* Store and Forward
* Guaranteed Delivery

`Count: ~18 patterns`

### 4. <span style="color:yellow">Concurrency + Performance Patterns</span>

These are backend core patterns for multi-threading, high throughput API servers, and async systems.

<span style="color:orange">Concurrency</span>
* Producer–Consumer
* Thread Pool
* Reactor
* Proactor
* Scheduler
* Reader–Writer Lock
* Immutable Object
* Future / Promise
* Guarded Suspension

<span style="color:orange">Caching</span>
* Cache Aside
* Write Through
* Write Back
* Read/Write Replicas Pattern

<span style="color:orange">Performance</span>
* Sharding
* Partitioning
* Batching
* Debouncing / Throttling

`Count: ~17 patterns`

### 5. <span style="color:yellow">Cloud, Resilience, Reliability Patterns
Modern cloud-native patterns (AWS, Kubernetes, GCP).

<span style="color:orange">Resilience</span>
* Circuit Breaker
* Retry
* Timeout
* Bulkhead
* Chaos Engineering Pattern

<span style="color:orange">Data Storage</span>
* Saga Pattern
* Two-Phase Commit
* Orchestration vs. Choreography
* Event-Carried State Transfer

<span style="color:orange">API Reliability & Control</span>
* Rate Limiting
* Distributed Lock
* Leader Election

`Count: ~12 patterns`