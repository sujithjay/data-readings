# Reading List in Data Systems
A list of papers, articles, and online resources I have found essential to understanding data-intensive systems and building new data systems. The list is curated and maintained by Sujith Jay Nair ([@sujithjay](https://github.com/sujithjay/)). If you think a paper should be part of this list, please submit a pull request. I will add it to the list once I peruse the paper. Please make sure the subject-matter of the paper is within the realm of either i) understanding data systems, or ii) building data systems.

Data systems are defined to include:
- Database systems
- Data processing systems

This list is inspired by Reynold Xin's list on [Database Readings](https://github.com/rxin/db-readings), and is a work in progress. Where I have written about a paper on [my blog](https://sujithjay.com), its entry links to my notes.

_Last updated: September 2026._

## Table of Contents
1. [Consistency and Consensus](#consistency-and-consensus)
2. [Query Processing](#query-processing)
3. [State and Stream](#state-and-stream)
4. [Database Design](#database-design)
5. [Cluster Resource Management](#cluster-resource-management)

### Consistency and Consensus

- [Linearizability: A Correctness Condition for Concurrent Objects](http://courses.cs.vt.edu/~cs5204/fall07-kafura/Papers/TransactionalMemory/Linearizability.pdf) (1990): Defines linearizability as a correctness condition for a register, as opposed to serializability which is a correctness condition for the higher abstraction, 'transaction'.

- [On Scalable and Efficient Distributed Failure Detectors](https://doi.org/10.1145/383962.384010) (2001): The gossip-inspired failure detection protocol behind Dynamo-family databases. It establishes the optimum worst-case network load for a distributed failure detection scheme, and provides an algorithm of such an optimum scheme.

- [Paxos Made Simple](http://www.cs.utexas.edu/users/lorenzo/corsi/cs380d/past/03F/notes/paxos-simple.pdf) (2001): The consensus protocol behind many distributed systems explained in plain English.

### Query Processing

- [Apache Calcite: A Foundational Framework for Optimized Query Processing Over Heterogeneous Data Sources](https://arxiv.org/pdf/1802.10233.pdf) (2018): Explains the design of the Calcite project, which is a distributed query parser & optimizer for heterogenous data sources. Calcite is used in a host of data processing systems, such as Apache Flink, Apache Drill and others. This paper is particularly interesting to understand the concepts around query parsing (and transformation into relational algebra), query optimizations (such as predicate pushdown & column pruning), and logical & physical plan generation. It is worthwhile to compare and contrast this with the paper on Spark SQL (listed below). Although this paper came after the Spark SQL paper, the work predates it.

- [Spark SQL: Relational Data Processing in Spark](https://people.csail.mit.edu/matei/papers/2015/sigmod_spark_sql.pdf) (2015): Explains the design of a distributed relational processing system in Apache Spark.

- [How to Architect a Query Compiler, Revisited](https://www.cs.purdue.edu/homes/rompf/papers/tahboub-sigmod18.pdf) (2018): A study on how to design a query compiler from a query interpreter. There are places where the lack of foundational background might hamper your progress in reading this paper. For this, I would suggest skimming [Query Evaluation Techniques for Large Databases](http://infolab.stanford.edu/~hyunjung/cs346/graefe.pdf) as a primer. Also, I would suggest reading the [HyPer](https://www.vldb.org/pvldb/vol4/p539-neumann.pdf) paper (a part of this list as well) before reading this one.

- [Efficiently Compiling Efficient Query Plans for Modern Hardware](https://www.vldb.org/pvldb/vol4/p539-neumann.pdf) (2011): Also known as the HyPer paper, this paper introduced data-centric query evaluation as an alternative to the the traditional iterative approach.

- [Everything You Always Wanted to Know About Compiled and Vectorized Queries But Were Afraid to Ask](http://www.vldb.org/pvldb/vol11/p2209-kersten.pdf) (2018): Compares the two dominant designs for fast query engines, data-centric compilation (as in HyPer) and vectorized interpretation (as in VectorWise), by implementing both in the same system. Neither wins outright: compilation is faster on computation-heavy queries, while vectorization is better at hiding memory stalls. A good companion to the HyPer paper above.

- [Integration of Large-Scale Data Processing Systems and Traditional Parallel Database Technology](http://www.vldb.org/pvldb/vol12/p2290-abouzied.pdf) (2019): HadoopDB was a 2009 prototype of a hybrid SQL system, combining the Hadoop MapReduce framework with parallel database management systems. This paper revisits its design choices and investigates its legacy in existing data systems, which makes it a great review of the state of modern data analysis systems. My notes on it are [here](https://sujithjay.com/hadoopdb).

- [Velox: Meta's Unified Execution Engine](https://www.vldb.org/pvldb/vol15/p3372-pedreira.pdf) (2022): Velox is an open-source C++ library of reusable, vectorized execution components, which Meta uses across engines such as Presto, Spark and stream processing instead of each engine building its own. The paper makes the case for unifying execution engines and describes Velox's design.


### State and Stream
- [Data in Flight](https://doi.org/10.1145/1629175.1629195) (2010): Introduces a model of streams as a superset of the relational model. Streams introduce a notion of time (processing-time, IMO) to the relational model. I explore a similar idea in this [post](http://sujithjay.com/data-systems/A-Simple-Dichotomy-for-Modelling-Data-Intensive-Systems/). In a relational table, data is persistent and query is transient; in a stream, query is persistent and data is transient.

- [Kafka: a Distributed Messaging System for Log Processing](https://www.microsoft.com/en-us/research/wp-content/uploads/2017/09/Kafka.pdf) (2011): The original Kafka paper from LinkedIn. A topic is split into partitions, each an append-only log on disk; consumers pull messages and keep track of their own position in each partition, which keeps the brokers simple and fast.

- [The Dataflow Model: A Practical Approach to Balancing Correctness, Latency, and Cost in Massive-Scale, Unbounded, Out-of-Order Data Processing](http://www.vldb.org/pvldb/vol8/p1792-Akidau.pdf) (2015): A single model for batch and stream processing over unbounded, out-of-order data. It separates what is computed, where in event time it is computed (windowing), when in processing time results are emitted (watermarks and triggers), and how successive results relate (accumulation). This is the model behind Apache Beam.

- [State Management in Apache Flink: Consistent Stateful Distributed Stream Processing](http://www.vldb.org/pvldb/vol10/p1718-carbone.pdf) (2017): How Flink keeps large operator state consistent. Asynchronous snapshots, coordinated by barriers that flow with the stream, give exactly-once state semantics, and state partitioned into key groups lets a running job be rescaled.

- [Providing Streaming Joins as a Service at Facebook](http://www.vldb.org/pvldb/vol11/p1809-jacques-silva.pdf) (2018): Stream-stream joins trade off output latency, join accuracy and memory footprint. This paper describes Facebook's streaming join service, which sits in the middle of that trade-off: joins are best-effort, and accuracy improves by pacing the consumption of input streams with dynamically estimated event-time watermarks. My notes on it are [here](https://sujithjay.com/streaming-joins-at-facebook).

### Database Design
- [Dynamo: Amazon’s Highly Available Key-value Store](https://courses.cs.washington.edu/courses/csep552/18wi/papers/decandia-dynamo.pdf) (2007): This paper on Dynamo (not to be confused with DynamoDB, which is 'built on the principles of Dynamo') is an excellent primer on understanding concepts behind high-availability storage systems; concepts such as Consistent Hashing, Sloppy Quorum, Anti-entropy processes, and Gossip.

- [Cassandra - A Decentralized Structured Storage System](https://www.cs.cornell.edu/projects/ladis2009/papers/lakshman-ladis2009.pdf) (2009): Cassandra is one of many data storage systems heavily influenced by Dynamo. However, important differences exist. I have written about it in this [post](https://sujithjay.com/data-systems/Dynamo-vs-Cassandra/).

- [Delta Lake: High-Performance ACID Table Storage over Cloud Object Stores](http://www.vldb.org/pvldb/vol13/p3411-armbrust.pdf) (2020): Implements ACID tables on cloud object stores by keeping a transaction log of the table's metadata in the object store itself, alongside the data files. That log gives the table transactions, time travel and fast metadata operations, and it underpins the lakehouse architecture.

- [Data Management for Data Science - Towards Embedded Analytics](https://www.cidrdb.org/cidr2020/papers/p23-raasveldt-cidr20.pdf) (2020): Argues that data science needs an analytical database that runs embedded in the analysis process, the way SQLite does for transactional workloads, and describes the design of DuckDB, built to be that database.

- [FoundationDB: A Distributed Unbundled Transactional Key Value Store](https://www.foundationdb.org/files/fdb-paper.pdf) (2021): FoundationDB unbundles a database into separate transaction management, log and storage systems, and offers strictly serializable transactions over a key-value store. The paper is also known for its account of deterministic simulation testing, which runs the whole distributed system inside a single simulated process to find bugs.

- [Amazon Redshift Re-invented](https://www.amazon.science/publications/amazon-redshift-re-invented) (2022): How Redshift has changed since its launch: a compiled query engine, managed storage that separates compute from storage, concurrency scaling, and automated tuning using machine learning. A useful view of what a cloud data warehouse looks like after a decade in production.

### Cluster Resource Management
- [Omega: Flexible, Scalable Schedulers for Large Compute Clusters](https://static.googleusercontent.com/media/research.google.com/en//pubs/archive/41684.pdf) (2013): Classifies cluster resource managers into monolithic, two-level (such as Mesos) and shared-state schedulers, and presents Omega, the shared-state design that is one of the precursors to Kubernetes. I use its classification to explain Mesos in this [post](https://sujithjay.com/mesos).
