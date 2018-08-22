# Reading List in Data Systems
A list of papers, articles, and online resources I have found essential to understanding data-intensive systems and building new data systems. The list is curated and maintained by Sujith Jay Nair ([@sujithjay](https://github.com/sujithjay/)). If you think a paper should be part of this list, please submit a pull request. I will add it to the list once I peruse the paper & am convinced of its utility & novelty. Please make sure the subject-matter of the paper is within the realm of either i) understanding data systems, or ii) building data systems.

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
### Query Processing
### State and Stream
- [Data in Flight](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.462.4828&rep=rep1&type=pdf) (2010): Introduces a model of streams as a superset of the relational model. Streams introduce a notion of time (processing-time, IMO) to the relational model. I explore a similar idea in this [post](http://sujithjay.com/data-systems/A-Simple-Dichotomy-for-Modelling-Data-Intensive-Systems/). In a relational table, data is persistent and query is transient; in a stream, query is persistent and data is transient.
### Database Design
### Distributed Data Computation
