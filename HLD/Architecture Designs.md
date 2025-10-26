
---

# 🧱 Software Architecture — Patterns & Styles

## 1. Monolithic vs Microservices

### Monolithic

- **Definition:** All components (UI, logic, DB access) in a _single codebase_; deployed as one unit.
    
- **✅ Pros:**
    
    - Simple to develop & deploy
        
    - Easy for small apps
        
    - Less complex (single codebase)
        
- **❌ Cons:**
    
    - Hard to scale (all must scale together)
        
    - Tight coupling → difficult maintenance
        
    - Single point of failure
        
- **💡 Use Case:** Small/startup apps needing quick deployment.
    

### Microservices

- **Definition:** App split into _independent services_, each with its own business logic; communicate via APIs or messaging.
    
- **✅ Pros:**
    
    - Independent scaling
        
    - Fault tolerance (isolated failures)
        
    - Tech stack flexibility
        
- **❌ Cons:**
    
    - Complex communication & data management
        
    - Needs strong DevOps automation
        
    - Hard to maintain consistency
        
- **💡 Use Case:** Large, complex, or scalable systems (e.g., e-commerce, cloud apps)
    

---

## 2. When to choose Layered over Microservices

- **Use Layered when:**
    
    - Simpler systems with few components.
        
    - Tight _budget/time constraints_ (microservices have infra overhead).
        
    - Working with _legacy layered systems_.
        
- **💡 Use Case:** CRMs, enterprise apps needing separation of concerns but not independent scaling.
    

---

## 3. Event-Driven Architecture (EDA)

- **Definition:** Components react to _events/messages_ instead of direct calls.
    

### ✅ Pros

- Loose coupling → independent updates
    
- Asynchronous → better performance
    
- Highly scalable (IoT, real-time systems)
    

### ❌ Cons

- Complex debugging/tracing
    
- Data consistency challenges (async)
    
- Needs event bus/message infra (e.g., Kafka)
    

### 💡 Use Case

Real-time, IoT, trading systems, event-heavy apps.

---

## 4. Architecture Impact on Scalability & Performance

### Scalability

- **Microservices:** Independent scaling → efficient.
    
- **Monolithic:** Must scale whole app → wasteful.
    

### Performance

- **Event-driven:** Async → fast for real-time.
    
- **Layered:** Layer overhead adds latency.
    
- **Microservices:** Network latency due to inter-service calls.
    

👉 **Architecture defines traffic capacity (scalability)** and **response efficiency (performance).**

---

## 5. Business Requirements & Architectural Choices

|Business Need|Suitable Architecture|
|---|---|
|Rapid development / Speed to market|Monolithic|
|Independent scaling / growth|Microservices|
|Real-time / scalable workloads|Event-driven|
|Limited budget / simplicity|Layered or Monolithic|

---

## 6. Layered vs Client-Server Architecture

### Layered

- Multiple logical layers (UI, Logic, Data).
    
- Strong **separation of concerns**.
    
- Common in enterprise apps.
    

### Client-Server

- **Client** requests → **Server** provides.
    
- Focused on interaction, not layers.
    
- Simpler but less modular.
    

---

## 7. Challenges in Large Monolithic Systems

- **Tight coupling:** Hard to modify one part.
    
- **Scaling issues:** Must scale entire app.
    
- **Deployment risk:** Redeploy whole system.
    
- **Team slowdown:** Coordination complexity increases.
    

---

## 8. Choosing Between Monolithic & Microservices

|Situation|Recommended|
|---|---|
|Small/medium app, fast MVP|Monolithic|
|Large, modular, scalable system|Microservices|
|Need independent teams & services|Microservices|
|Simplicity & quick iteration|Monolithic|

---

## 9. Fault Tolerance in Microservices

- **Key benefit:** One service failure ≠ total failure.
    
- **Mechanisms:**
    
    - Circuit breakers
        
    - Retry logic
        
    - Load balancing
        
- Ensures reliability & resilience.
    

---

## 10. Real-Time Data in Event-Driven Systems

- **Immediate reaction:** Process data as events occur.
    
- **Asynchronous pub-sub:** Fast, non-blocking.
    
- **Queues/Brokers:** Kafka, RabbitMQ manage event flow.
    



---

# 🧩 Microservices Architecture — Interview Q&A

## 1. What are Microservices? (vs Monolithic)

**Definition:**  
Microservices = application built as **small, loosely coupled services**, each handling a specific business function.  
Each service runs **independently**, communicates via **APIs**, and can be **developed, deployed, and scaled separately**.

### 🔄 Difference: Monolithic vs Microservices

|Feature|Monolithic|Microservices|
|---|---|---|
|**Scalability**|Must scale whole app|Scale services independently|
|**Deployment**|Full redeployment required|Independent deployments|
|**Tech Stack**|Single stack|Polyglot (any tech per service)|
|**Fault Tolerance**|One failure = total crash|Failures isolated|
|**Development**|Slower, shared codebase|Faster, independent teams|

---

## 2. Benefits & Challenges

### ✅ Benefits

- **Independent Scalability** – Scale only what’s needed.
    
- **Faster Development** – Teams deploy separately.
    
- **Tech Flexibility** – Choose per-service stack.
    
- **Fault Isolation** – One service fails ≠ system down.
    
- **Continuous Deployment** – Enables frequent, smaller releases.
    

### ❌ Challenges

- **System Complexity** – Coordination, deployment harder.
    
- **Data Management** – Distributed DB consistency is tough.
    
- **Communication Overhead** – REST/gRPC/events require robust design.
    
- **Monitoring Difficulty** – Requires observability tools (Jaeger, Prometheus).
    

---

## 3. Identifying & Designing Microservices

### 🧭 Principles

1. **Domain Decomposition (DDD)** – Split by business capability (Order, Payment, User).
    
2. **Single Responsibility Principle (SRP)** – Each service handles one concern.
    
3. **Database per Service** – Avoid shared DBs → loose coupling.
    
4. **Well-defined APIs** – REST, gRPC, or event-driven comms.
    
5. **Scalability Focus** – Design high-traffic services for independent scaling.
    

---

## 4. API Gateway

**Definition:** Reverse proxy acting as a **single entry point** for all external requests.

### 🚪 Why Use It

- ✅ Central **Authentication & Security**
    
- ✅ **Load Balancing** & traffic control
    
- ✅ **Request Routing / Aggregation**
    
- ✅ **Rate Limiting & Monitoring**
    

**Examples:** Kong, Nginx, Apigee, AWS API Gateway

---

## 5. Inter-Service Communication

### 1️⃣ Synchronous

- **REST (HTTP APIs)** – Simple, easy but adds latency
    
- **gRPC** – Faster, binary format → low latency
    

### 2️⃣ Asynchronous

- **Event-driven Messaging (Kafka, RabbitMQ, SNS/SQS)** – Decoupled & scalable
    
- **Pub/Sub Model** – Publisher emits → Subscribers consume
    

---

## 6. Ensuring Data Consistency

Since each service owns its DB → strong consistency is difficult.

### ⚙️ Strategies

1. **Eventual Consistency** – Updates propagate asynchronously
    
2. **SAGA Pattern** – Distributed transactions via compensating actions
    
3. **Two-Phase Commit (2PC)** – Strong consistency, low scalability
    
4. **Event Sourcing** – Log changes as events for reliable replay
    

---

## 7. Deployment Strategies

🚀 **CI/CD Pipelines** – Automate build, test, deploy  
🚀 **Blue-Green Deployment** – Run old (Blue) & new (Green) → switch traffic  
🚀 **Canary Deployment** – Gradual rollout to small user subset  
🚀 **Service Mesh (Istio, Linkerd)** – Manages security, observability, comms

---

## 8. Scaling Strategies

- 🔹 **Horizontal Scaling** – Add more service instances
    
- 🔹 **Auto-Scaling** – Use K8s or ECS to auto-adjust capacity
    
- 🔹 **Database Sharding** – Split data across shards
    
- 🔹 **Read Replicas** – Improve DB read performance
    

---

## 9. Real-World Examples

📌 **Netflix** – Microservices for content delivery, recommendations  
📌 **Uber** – Ride-matching, payments, navigation as separate services  
📌 **Amazon** – Product, payments, shipping = independent services

---

## 10. Monitoring & Debugging Best Practices

🔍 **Centralized Logging** – ELK Stack (Elastic, Logstash, Kibana), Graylog  
🔍 **Distributed Tracing** – Jaeger, Zipkin for cross-service request flow  
🔍 **Metrics & Monitoring** – Prometheus + Grafana dashboards  
🔍 **Health Checks** – Liveness/readiness probes detect failed services


---

# ⚡ Event-Driven Architecture (EDA) — Interview Q&A

## 1. Fundamentals

### 🧩 What is Event-Driven Architecture (EDA)?

- **Definition:**  
    A software pattern where system components communicate via **events** instead of direct synchronous calls.  
    Producers publish events → Consumers react asynchronously.
    

### 🔄 Differences: EDA vs Request-Response

|Feature|Request-Response|Event-Driven|
|---|---|---|
|**Coupling**|Direct dependency|Loosely coupled via events|
|**Scalability**|Harder to scale|Easier to extend by new consumers|
|**Processing**|Synchronous|Asynchronous / non-blocking|

---

## 2. Pub-Sub vs Event Streaming

|Feature|Pub-Sub|Event Streaming|
|---|---|---|
|**Communication**|One-to-many event distribution|Events stored & replayed|
|**Persistence**|Transient (lost after consumption)|Persistent (can replay history)|
|**Ordering**|No strict order|Strict ordering per partition|
|**Examples**|RabbitMQ, AWS SNS, Redis Pub/Sub|Apache Kafka, AWS Kinesis|

**Use Cases:**

- 🟢 _Pub-Sub:_ Real-time notifications (need latest state).
    
- 🟢 _Event Streaming:_ Replay, analytics, state reconstruction.
    

---

## 3. Components of an Event-Driven System

1. **Event Producers** → Emit events (e.g., user action).
    
2. **Event Brokers** → Route/distribute events (Kafka, RabbitMQ, EventBridge).
    
3. **Event Consumers** → Process events asynchronously.
    
4. **Event Store (optional)** → Persist events for replay/audit.
    

---

## 4. Challenges & Eventual Consistency

### ⚠️ Challenges

- Asynchronous → **Eventual consistency**
    
- **Event ordering** in distributed systems
    
- **Debugging complexity**
    
- **Failure handling** (consumer errors, retries)
    

### 🧠 Handling Eventual Consistency

- Use **idempotent operations**
    
- Apply **SAGA pattern** (orchestration/choreography)
    
- Adopt **Event Sourcing** for reconstructing state
    

---

## 5. Ensuring Event Ordering

To preserve sequence where order matters:

- **Partitioning:** (e.g., Kafka ensures order per partition)
    
- **Event Versioning:** Include version numbers
    
- **Global Ordering Service:** Assign sequence IDs
    
- **Deduplication:** Discard out-of-order or repeated events
    

---

## 6. Dead-Letter Queues (DLQs)

**Definition:**  
A queue for failed or unprocessable messages.

**🧰 Importance**

- Prevents **infinite retries**
    
- Enables **debugging of failed events**
    
- Improves **system reliability**
    

**Example:**  
Kafka → dedicated _dead-letter topic_ for failed messages.

---

## 7. Kafka vs RabbitMQ vs AWS EventBridge

|Feature|Apache Kafka|RabbitMQ|AWS EventBridge|
|---|---|---|---|
|**Type**|Event Streaming|Pub-Sub|Managed Event Bus|
|**Persistence**|Persistent (replayable)|Transient|No persistence|
|**Ordering**|Guaranteed (per partition)|Not guaranteed|No strict order|
|**Scalability**|High (partition-based)|Horizontal|Auto-scales (AWS)|
|**Use Case**|Large-scale streaming|Messaging, task queues|AWS service integration|

**Usage Summary:**

- 🧠 _Kafka:_ Analytics & event pipelines
    
- 🧠 _RabbitMQ:_ Real-time messaging / tasks
    
- 🧠 _EventBridge:_ AWS-native integrations
    

---

## 8. Idempotency in Event Processing

**Goal:** Prevent duplicate side effects if the same event reprocesses.

### 🛠 Techniques

- **Unique Event IDs** → Track processed IDs
    
- **Processed State Tracking** → Mark completed events
    
- **Idempotent Logic** → Avoid state change unless needed
    
- **Broker Deduplication** → Kafka log compaction prevents duplicates
    

---

## 9. Real-World Use Case — E-Commerce Order System

**Scenario:** Customer places an order

- 🧾 Order Service → emits `OrderPlaced`
    
- 💳 Payment Service → listens, processes payment
    
- 📦 Inventory Service → updates stock
    
- ✉️ Notification Service → sends confirmation
    

**✅ Benefits:**

- Asynchronous scaling
    
- Fault isolation
    
- Easy addition of new services (analytics, fraud detection)
    

---

## 10. Schema Evolution Strategies

When event schema changes over time → ensure compatibility.

### 🧰 Best Practices

- **Backward Compatibility:** New consumers handle old events.
    
- **Versioning:** Add `schema_version` field.
    
- **Schema Registry:** (Kafka Avro/Protobuf) for validation.
    
- **Field Deprecation:** Mark old fields instead of removing.
    
- **Transformation Layer:** Convert old → new schema format.
    

**Example:**  
Kafka Schema Registry ensures producer-consumer compatibility.

---

Would you like me to make a **visual Obsidian map-style summary** next (like collapsible “cheat bullets” with only the key recall points per question)? It’s ideal for fast last-minute prep.