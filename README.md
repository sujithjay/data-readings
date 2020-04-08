# Reading List in Data Systems
A list of papers, articles, and online resources I have found essential to understanding data-intensive systems and building new data systems. The list is curated and maintained by Sujith Jay Nair ([@sujithjay](https://github.com/sujithjay/)). If you think a paper should be part of this list, please submit a pull request. I will add it to the list once I peruse the paper. Please make sure the subject-matter of the paper is within the realm of either i) understanding data systems, or ii) building data systems.

Data systems are defined to include:
- Database systems
- Data processing systems

This list is inspired by Reynold Xin's list on [Database Readings](https://github.com/rxin/db-readings), and is a work in progress.

## Table of Contents
1. [Consistency and Consensus](#consistency-and-consensus)
2. [Query Processing](#query-processing)
3. [State and Stream](#state-and-stream)
4. [Database Design](#database-design)

### Consistency and Consensus

- [Linearizability: A Correctness Condition for Concurrent Objects](http://courses.cs.vt.edu/~cs5204/fall07-kafura/Papers/TransactionalMemory/Linearizability.pdf) (1990): Defines linearizability as a correctness condition for a register, as opposed to serializability which is a correctness condition for the higher abstraction, 'transaction'.

- [On Scalable and Efficient Distributed Failure Detectors](http://www.ict.uom.gr/teaching/distrubutedSite/eceutexas/dist2/papers/On_scalable_and_efficient_distributed_failure_detectors.pdf) (2001): The gossip-inspired failure detection protocol behind Dynamo-family databases. It establishes the optimum worst-case network load for a distributed failure detection scheme, and provides an algorithm of such an optimum scheme.

- [Paxos Made Simple](http://www.cs.utexas.edu/users/lorenzo/corsi/cs380d/past/03F/notes/paxos-simple.pdf) (2001): The consensus protocol behind many distributed systems explained in plain English.

### Query Processing

- [Apache Calcite: A Foundational Framework for Optimized Query Processing Over Heterogeneous Data Sources](https://arxiv.org/pdf/1802.10233.pdf) (2018): Explains the design of the Calcite project, which is a distributed query parser & optimizer for heterogenous data sources. Calcite is used in a host of data processing systems, such as Apache Flink, Apache Drill and others. This paper is particularly interesting to understand the concepts around query parsing (and transformation into relational algebra), query optimizations (such as predicate pushdown & column pruning), and logical & physical plan generation. It is worthwhile to compare and contrast this with the paper on Spark SQL (listed below). Although this paper came after the Spark SQL paper, the work predates it.

- [Spark SQL: Relational Data Processing in Spark](https://people.csail.mit.edu/matei/papers/2015/sigmod_spark_sql.pdf) (2015): Explains the design of a distributed relational processing system in Apache Spark.

- [How to Architect a Query Compiler, Revisited](https://www.cs.purdue.edu/homes/rompf/papers/tahboub-sigmod18.pdf) (2018): A study on how to design a query compiler from a query interpreter. There are places where the lack of foundational background might hamper your progress in reading this paper. For this, I would suggest skimming [Query Evaluation Techniques for Large Databases](http://infolab.stanford.edu/~hyunjung/cs346/graefe.pdf) as a primer. Also, I would suggest reading the [HyPer](https://www.vldb.org/pvldb/vol4/p539-neumann.pdf) paper (a part of this list as well) before reading this one.

- [Efficiently Compiling Efficient Query Plans for Modern Hardware](https://www.vldb.org/pvldb/vol4/p539-neumann.pdf) (2011): Also known as the HyPer paper, this paper introduced data-centric query evaluation as an alternative to the the traditional iterative approach.


### State and Stream
- [Data in Flight](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.462.4828&rep=rep1&type=pdf) (2010): Introduces a model of streams as a superset of the relational model. Streams introduce a notion of time (processing-time, IMO) to the relational model. I explore a similar idea in this [post](http://sujithjay.com/data-systems/A-Simple-Dichotomy-for-Modelling-Data-Intensive-Systems/). In a relational table, data is persistent and query is transient; in a stream, query is persistent and data is transient.

### Database Design
- [Dynamo: Amazon’s Highly Available Key-value Store](https://courses.cs.washington.edu/courses/csep552/18wi/papers/decandia-dynamo.pdf) (2007): This paper on Dynamo (not to be confused with DynamoDB, which is 'built on the principles of Dynamo') is an excellent primer on understanding concepts behind high-availability storage systems; concepts such as Consistent Hashing, Sloppy Quorum, Anti-entropy processes, and Gossip.

- [Cassandra - A Decentralized Structured Storage System](https://www.cs.cornell.edu/projects/ladis2009/papers/lakshman-ladis2009.pdf) (2009): Cassandra is one of many data storage systems heavily influenced by Dynamo. However, important differences exist. I have written about it in this [post](https://sujithjay.com/data-systems/Dynamo-vs-Cassandra/).
