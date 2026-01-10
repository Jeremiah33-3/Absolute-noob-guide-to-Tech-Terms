## Video tutorials

- [How does NoSQL databases work](https://www.youtube.com/watch?v=0buKQHokLK8)

## SQL vs NoSQL

### The Core Difference
SQL (Relational Database Management Systems - RDBMS): Think of this like a Excel spreadsheet. Data is stored in strict rows and columns with predefined relationships. It is best for structured data where integrity is paramount.

NoSQL (Non-Relational or Distributed Database): Think of this like a file folder or a flexible laundry basket. You can throw different types of data in together without a predefined structure. It is best for unstructured data, rapid iteration, and massive scale.

| Feature          | SQL (Relational) | NoSQL (Non-Relational) |
|------------------|------------------|------------------------|
| Data Structure   | Table-based. Rigid schema; data must fit into rows and columns. | Flexible. Document, Key-Value, Wide-Column, or Graph-based. |
| Schema           | Pre-defined. You must define the structure (schema) before adding data. Changing it later can be difficult. | Dynamic. You can add fields on the fly. Each document can have a different structure. |
| Scalability      | Vertical (Scale Up). To handle more load, you add more CPU/RAM to a single server. | Horizontal (Scale Out). To handle more load, you add more servers to the pool (sharding). |
| Consistency      | ACID. Prioritizes strong consistency and data integrity (Atomicity, Consistency, Isolation, Durability). | BASE / CAP. Often prioritizes Availability and Partition Tolerance (Eventual Consistency), though some offer ACID. |
| Query Language   | SQL (Structured Query Language). Standardized and powerful for complex joins. | Unstructured. Varies by database (e.g., MongoDB uses JSON-like queries). No standard language. |
| Best For         | Complex queries, multi-row transactions, and data integrity (e.g., Banking). | Big data, real-time analytics, content management, and rapid prototyping. |

### Key Concepts

#### 1. Scalability: Up vs. Out
This is often the deciding factor for high-traffic applications.

- **SQL (Vertical Scaling)**  
  Imagine living in a building. If you have more people (data), you have to renovate your apartment to make it bigger (add RAM/CPU). Eventually, you hit a limit on how big the apartment can get.

- **NoSQL (Horizontal Scaling)**  
  Instead of renovating, you simply buy the apartment next door, and the one next to that. You distribute the people (data) across multiple apartments (servers).  
  This makes NoSQL preferred for massive datasets (**Big Data**).

#### 2. The 4 Types of NoSQL
Unlike SQL, which is almost always table-based, NoSQL comes in four distinct flavors:

- **Document Stores** (e.g., *MongoDB*)  
  Stores data in JSON-like documents.  
  *Great for CMS or catalogs.*

- **Key-Value Stores** (e.g., *Redis*)  
  The simplest form; holds a key and a value. Ultra-fast.  
  *Great for caching.*

- **Wide-Column Stores** (e.g., *Cassandra*)  
  Optimized for writing large amounts of data across many servers.  
  *Great for analyzing IoT logs.*

- **Graph Stores** (e.g., *Neo4j*)  
  Focuses on the relationships between data nodes.  
  *Great for social networks or recommendation engines.*

#### 3. Consistency Models (ACID vs. BASE)

- **SQL — ACID**  
  If a bank transfer fails halfway through, the database cancels the whole operation. The money never disappears.  
  *The data is always accurate and consistent.*

- **NoSQL — BASE** (*Basically Available, Soft state, Eventual consistency*)  
  If you post a photo on Instagram, it’s okay if your friend in another country sees it a few seconds later than you do.  
  *Availability and speed are prioritized over instant consistency.*

---
| Type   | Popular Technologies                                                                 |
|--------|---------------------------------------------------------------------------------------|
| SQL    | MySQL, PostgreSQL, Oracle Database, Microsoft SQL Server                               |
| NoSQL  | MongoDB (Document), Cassandra (Column), Redis (Key-Value), Neo4j (Graph), DynamoDB     |
---

### Which one should you choose?

Choose SQL if:
- You are dealing with financial data or systems where data integrity is critical.
- Your data is highly structured and unchanging.
- You need to perform complex queries involving many relationships (JOINS).

Choose NoSQL if:
- Your data requirements are changing rapidly (agile development).
- You are dealing with massive amounts of unstructured data (logs, social media feeds).
- You need ultra-low latency or need to scale to thousands of servers.
