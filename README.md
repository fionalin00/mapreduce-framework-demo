# MapReduce-Based Search System

A distributed search system that separates offline batch indexing from online query serving to enable low-latency search over large document collections.  
This system precomputes an inverted index and ranking signals offline using MapReduce, then serves queries online through parallel index servers.

```mermaid
flowchart LR
  subgraph Offline["Offline Indexing"]
    A[Crawl] --> B[MapReduce]
    B --> C[Inverted Index and PageRank]
  end

  subgraph Online["Online Serving"]
    U[User] --> UI[UI]
    UI --> S[Search Server]
    S -->|parallel query| IS[Index Servers]
    IS --> R[Results]
  end

  C --> IS
````
## Key Components
- **Offline Indexing Pipeline**
  - Crawls and processes HTML documents
  - Uses a MapReduce framework to build an inverted index
  - Computes ranking signals (e.g., PageRank) ahead of time

- **Search Server**
  - Handles incoming user queries
  - Fans out queries to multiple index servers in parallel
  - Aggregates and ranks results before returning them

- **Index Servers**
  - Serve sharded portions of the inverted index
  - Respond with document IDs and relevance scores

- **Online Serving Path**
  - Designed for low latency by relying on precomputed data

  ## MapReduce Usage
  MapReduce is used in the offline indexing phase to process large document collections in parallel.  
The map phase extracts term–document pairs, while the reduce phase aggregates postings to construct inverted index shards.

## Design Rationale
- Expensive computation is moved to offline batch jobs
- Online queries avoid full document scans
- Sharding enables parallel query execution
- The system cleanly separates indexing from serving

## Code Access
Source code is private due to academic integrity and course policies.  
I’m happy to walk through the implementation, system design, or code structure in a private discussion.
