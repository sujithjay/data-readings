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

- [Linearizability: A Correctness Condition for Concurrent Objects](http://courses.cs.vt.edu/~cs5204/fall07-kafura/Papers/TransactionalMemory/Linearizability.pdf) (1990): Defines linearizability as a property of a register, as opposed to serializability which is a property of the higher abstraction, 'transaction'.

### Query Processing

- [Apache Calcite: A Foundational Framework for Optimized Query Processing Over Heterogeneous Data Sources](https://arxiv.org/pdf/1802.10233.pdf) (2018): Explains the design of the Calcite project, which is a distributed query parser & optimizer for heterogenous data sources. Calcite is used in a host of data processing systems, such as Apache Flink, Apache Drill and others. This paper is particularly interesting to understand the concepts around query parsing (and transformation into relational algebra), query optimizations (such as predicate pushdown & column pruning), and logical & physical plan generation. It is worthwhile to compare and contrast this with the paper on Spark SQL (listed below). Although this paper came after the Spark SQL paper, the work predates it.

- [Spark SQL: Relational Data Processing in Spark](https://people.csail.mit.edu/matei/papers/2015/sigmod_spark_sql.pdf) (2015): Explains the design of a distributed relational processing system in Apache Spark.

### State and Stream
- [Data in Flight](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.462.4828&rep=rep1&type=pdf) (2010): Introduces a model of streams as a superset of the relational model. Streams introduce a notion of time (processing-time, IMO) to the relational model. I explore a similar idea in this [post](http://sujithjay.com/data-systems/A-Simple-Dichotomy-for-Modelling-Data-Intensive-Systems/). In a relational table, data is persistent and query is transient; in a stream, query is persistent and data is transient.

### Database Design

### Distributed Data Computation
