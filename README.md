# Reading List in Data Systems
A list of papers, articles, and online resources I have found essential to understanding data-intensive systems and building new data systems. The list is curated and maintained by Sujith Jay Nair ([@sujithjay](https://github.com/sujithjay/)). If you think a paper should be part of this list, please submit a pull request. I will add it to the list once I peruse the paper. Please make sure the subject-matter of the paper is within the realm of either i) understanding data systems, or ii) building data systems.

Data systems are defined to include:
- Database systems
- Data processing systems

This list is inspired by Reynold Xin's list on [Database Readings](https://github.com/rxin/db-readings).

## Table of Contents
1. [Algorithms](#Algorithms)
2. [Consistency and Consensus](#Consistency-and-Consensus)
3. [Query Processing](#Query-Processing)
4. [State and Stream](#State-and-Stream)
5. [Database Design](#Database-Design)
6. [Distributed Data Computation](#Distributed-Data-Computation)

### Algorithms

### Consistency and Consensus

- [Linearizability: A Correctness Condition for Concurrent Objects](http://courses.cs.vt.edu/~cs5204/fall07-kafura/Papers/TransactionalMemory/Linearizability.pdf) (1990): Defines linearizability as a correctness condition for a register, as opposed to serializability which is a correctness condition for the higher abstraction, 'transaction'.

### Query Processing

- [Apache Calcite: A Foundational Framework for Optimized Query Processing Over Heterogeneous Data Sources](https://arxiv.org/pdf/1802.10233.pdf) (2018): Explains the design of the Calcite project, which is a distributed query parser & optimizer for heterogenous data sources. Calcite is used in a host of data processing systems, such as Apache Flink, Apache Drill and others. This paper is particularly interesting to understand the concepts around query parsing (and transformation into relational algebra), query optimizations (such as predicate pushdown & column pruning), and logical & physical plan generation. It is worthwhile to compare and contrast this with the paper on Spark SQL (listed below). Although this paper came after the Spark SQL paper, the work predates it.

- [Spark SQL: Relational Data Processing in Spark](https://people.csail.mit.edu/matei/papers/2015/sigmod_spark_sql.pdf) (2015): Explains the design of a distributed relational processing system in Apache Spark.

### State and Stream
- [Data in Flight](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.462.4828&rep=rep1&type=pdf) (2010): Introduces a model of streams as a superset of the relational model. Streams introduce a notion of time (processing-time, IMO) to the relational model. I explore a similar idea in this [post](http://sujithjay.com/data-systems/A-Simple-Dichotomy-for-Modelling-Data-Intensive-Systems/). In a relational table, data is persistent and query is transient; in a stream, query is persistent and data is transient.

### Database Design
- [Dynamo: Amazon’s Highly Available Key-value Store](https://courses.cs.washington.edu/courses/csep552/18wi/papers/decandia-dynamo.pdf) (2007): This paper on Dynamo (not to be confused with DynamoDB, which is 'built on the principles of Dynamo') is an excellent primer on understanding concepts behind high-availability storage systems; concepts such as Consistent Hashing, Sloppy Quorum, Anti-entropy processes, and Gossip.

- [Cassandra - A Decentralized Structured Storage System](https://www.cs.cornell.edu/projects/ladis2009/papers/lakshman-ladis2009.pdf) (2009): Cassandra is one of many data storage systems heavily influenced by Dynamo. However, important differences exist. I summarise some in the table below:

| Problem       | Dynamo        | Cassandra  |
| ------------- |:-------------:| ----------:|
| High Availabilty for Writes      | Vector Clocks | Last Write Wins|
| Temporary Failures | Sloppy Quorum & Hinted Hand-offs      |    Strict Quorum & Hinted Hand-offs  |
| Partitioning      | Consistent Hashing      |  Consistent Hashing  |
| Permanent Failures | Anti-entropy using Merkle trees      |    Anti-entropy using Merkle trees |
| Failure Detection | Gossip Protocols      |    Gossip Protocols |

### Distributed Data Computation
