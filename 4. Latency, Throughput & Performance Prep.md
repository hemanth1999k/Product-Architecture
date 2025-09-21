# Latency, Throughput & Performance for Architecture Interviews

This guide covers three fundamental performance concepts in distributed systems and networking:  
**latency, throughput, and overall performance.**

---

## 1. Latency

### Definition
Latency is the time it takes for a request to travel from the client to the server and back (round-trip time).  

- **Measured in**: milliseconds (ms).  
- **Types of latency**:  
  - **Network latency** → caused by distance, hops, or congestion.  
  - **Processing latency** → time spent by servers to handle requests.  
  - **Disk latency** → time to read/write from storage.  

### Why It Matters
- Directly impacts **user experience** (slow apps feel unresponsive).  
- Critical for **real-time systems** (gaming, video calls, stock trading).  

### How to Reduce Latency
- Place servers closer to users (**CDN, edge computing**).  
- Optimize queries and avoid unnecessary computation.  
- Use **caching** to reduce repeated work.  
- Reduce payload size (e.g., compression, pagination).  

---

## 2. Throughput

### Definition
Throughput is the amount of data or number of requests a system can handle in a given period.  

- **Measured in**: requests per second (RPS) or bits per second (bps).  
- High throughput means the system can handle **more concurrent users or data volume**.  

### Why It Matters
- Ensures the system scales to handle growth.  
- Important for **batch systems** (ETL jobs, streaming analytics) and **real-time apps**.  

### How to Improve Throughput
- Add **parallelism** (multi-threading, async I/O).  
- Use **horizontal scaling** (more servers).  
- Introduce **message queues** (Kafka, RabbitMQ) to spread load.  
- Optimize databases with **sharding** and **replication**.  

---

## 3. Performance

### Definition
Performance is the overall **responsiveness and efficiency** of a system, balancing both **latency** and **throughput**.  

- **Low latency + High throughput = High performance.**  
- Trade-offs:  
  - A system can be optimized for **low latency** (fast responses) but may not handle large load.  
  - Or optimized for **high throughput** (handle many requests) but with slightly higher response times.  

### Example Trade-offs
- **Realtime chat app** → prioritize **low latency**.  
- **Data warehouse** → prioritize **throughput** (process terabytes overnight).  
- **Streaming platforms** → balance both.  

---

## 4. Real-World Examples

### Netflix
- Uses **CDN** to reduce latency in video delivery.  
- Optimizes throughput with distributed servers across the globe.  

### WhatsApp
- Prioritizes **low latency** for instant message delivery.  
- Uses **message queues** for scaling throughput when sending millions of messages per second.  

### Amazon
- Focuses on both latency (fast checkout experience) and throughput (millions of orders per day).  

---

## 5. Recap

- **Latency** = speed of a single request (how fast).  
- **Throughput** = system capacity (how much).  
- **Performance** = balance of latency and throughput.  
- Optimizations depend on use case:  
  - **Low latency** → real-time apps (chat, gaming, trading).  
  - **High throughput** → batch systems (ETL, data processing).  
  - **Balanced** → consumer platforms (ecommerce, streaming).  

---
