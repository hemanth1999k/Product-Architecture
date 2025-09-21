# 📚 Storage Systems for Architecture Interviews

This guide teaches **storage fundamentals** for system design interviews.  
We’ll cover relational databases, NoSQL models, schemas, ACID vs BASE, and when to use each.  

---

## 1. Relational Databases (SQL)

- **Structure**: Data stored in **tables** with **rows** (records) and **columns** (attributes).  
- **Schema**: A **blueprint** of the table — defines what columns exist and what data types they hold.  
  👉 *Schema enforces rules, ensuring every record follows the same structure.*  

### Example Table (Users)

| id | name     | email              | created_at          |
|----|----------|--------------------|---------------------|
| 1  | Alice    | alice@email.com    | 2024-05-12 10:00:00 |
| 2  | Bob      | bob@email.com      | 2024-06-20 14:22:00 |

**Strengths**:  
- Strong integrity with **ACID** guarantees.  
- Supports **complex queries** (joins, aggregations).  

**Weaknesses**:  
- Harder to scale horizontally.  
- Schema changes can be expensive.  

**When to use**: Banking, ERP, ecommerce checkout — anywhere **data correctness matters most**.  

---

## 2. Non-Relational Databases (NoSQL)

- **Flexible or schema-less**.  
- Designed for **scale, speed, and availability**.  
- Store data in different formats, depending on the model.

### Types of NoSQL Databases

1. **Key-Value Stores**  
   - Format: `{ key: value }`  
   - Example: `{ "user123": "Alice" }`  
   - Databases: **Redis, DynamoDB**  
   - Use for: caching, sessions, leaderboards.

2. **Document Stores**  
   - Format: JSON-like documents.  
   - Example:  
     ```json
     {
       "id": 1,
       "name": "Alice",
       "preferences": { "theme": "dark", "language": "EN" }
     }
     ```  
   - Databases: **MongoDB, Couchbase**  
   - Use for: user profiles, product catalogs, CMS.

3. **Column-Oriented Stores**  
   - Store data by **columns**, not rows.  
   - Databases: **Cassandra, HBase**  
   - Use for: time-series data, event logging, IoT.

4. **Graph Databases**  
   - Store nodes & edges (relationships).  
   - Example: `Alice — follows → Bob`  
   - Databases: **Neo4j, Amazon Neptune**  
   - Use for: social networks, fraud detection, recommendations.

```mermaid
graph TD
  A[Databases] --> B[Relational - SQL]
  A --> C[Non-Relational - NoSQL]
  C --> C1[Key-Value: Redis, DynamoDB]
  C --> C2[Document: MongoDB]
  C --> C3[Columnar: Cassandra]
  C --> C4[Graph: Neo4j]

## 2. SQL vs NoSQL at a Glance

| Feature     | SQL (Relational)          | NoSQL (Non-Relational)        |
|-------------|---------------------------|-------------------------------|
| Schema      | Strict (rows/columns)     | Flexible (dynamic JSON)       |
| Consistency | Strong (ACID)             | Eventual (BASE)               |
| Scaling     | Vertical (scale-up)       | Horizontal (scale-out)        |
| Use Cases   | Banking, ERP, ecommerce   | Social media, IoT, analytics  |

---

## 3. ACID vs BASE

### ACID (SQL → Data Integrity)

1. **Atomicity** → all-or-nothing  
   - Prevents partial updates.  
   - Protects: correctness.  
   - Example: In a bank transfer, if money leaves Account A, it must also enter Account B.  

2. **Consistency** → always valid state  
   - Enforces constraints and schema rules.  
   - Protects: validity.  
   - Example: A column `age` cannot have negative values.  

3. **Isolation** → transactions do not interfere  
   - Prevents dirty reads and lost updates.  
   - Protects: concurrency correctness.  
   - Example: Only one person can book the last flight seat.  

4. **Durability** → once saved, always saved  
   - Data survives crashes or restarts.  
   - Protects: reliability.  
   - Example: Order confirmation persists after system restart.  

---

### BASE (NoSQL → Availability and Scalability)

1. **Basically Available** → system always responds  
2. **Soft state** → data may change over time  
3. **Eventual consistency** → data becomes correct eventually  

- Protects: availability and scale.  
- Example: In Instagram, when you like a photo, it may take seconds before all friends see it.  

---

## 4. Popular Databases — When to Use

- **PostgreSQL** → relational, strong ACID + JSON support. (ERP, ecommerce, financial apps)  
- **MongoDB** → document-based, flexible schema. (user profiles, product catalogs)  
- **Redis** → in-memory, sub-millisecond. (cache, rate-limiting, real-time leaderboards)  
- **Cassandra** → distributed columnar. (time-series, logs, IoT, high write throughput)  

```mermaid
flowchart TD
   Start[Choose DB] --> Q1{Need ACID transactions?}
   Q1 -->|Yes| SQL[(Relational: PostgreSQL, MySQL)]
   Q1 -->|No| Q2{Need horizontal scale?}
   Q2 -->|Yes| NoSQL[(MongoDB, Cassandra, DynamoDB)]
   Q2 -->|No| Q3{Need Cache/Speed?}
   Q3 -->|Yes| Redis[(Key-Value: Redis)]
   Q3 -->|No| Graph[(Graph DB: Neo4j)]
