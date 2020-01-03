# 1

## Q

**What is Big Data? Give some examples about it.**

## Field

> big data is a **field** dedicated to **analysis**, **processing**, and **storage** of large collections of data that frequently originate from irrelevant sources. 

- example
  - combining of multiple unrelated datasets
  - processing of large amount of unstructured data
  - harvesting of hidden information in a time-sensitive manner

## Data

> big data refers to the large, diverse sets of information that grows at a ever-increasing rate. 

- It includes the **volume** of information, the **velocity** at which it is created and collected, and the **variety** of the data points being covered. 
- example
  - volume: Organizations and users world-wide create over 2.5 EBs of data a day. 
  - velocity: every 60 seconds, 300 hours of video is uploaded to YouTube
  - variety: structured data(financial transactions), semi-structured data(emails), unstructured data(images)
  - value: a 20 minute delayed stock price has little value compared to a price that is 20 milliseconds old

# 2

## Q

**How to address the challenges of Big Data’s 5 Vs, and give some examples.**

## Volume

- the incredible amount of data generated each second from social media, cell phones, credit cards, video. 
- solution
  - **distributed storage**: store data in different locations and brought together by software
  - **NoSQL** storage provide **scale out** capability while using inexpensive commodity servers. !
  - **distributed computing**: Batching Processing

## Velocity

- the speed of **generating**, **collecting** and **analyzing** a large amount of data
- solution
  - **NoSQL** storage devices enable fast writes by using **schema-on-read**(写入的时候不做检验, 读的时候, ) rather than schema-on-write(写的时候就做检验) principle. 
    - being highly available, NoSQL storage devices can ensure that write latency does not occur because of node or network failure. !
  -  **Distributed computing**

## Variety

- the different types of data, structured data, semi-structured data, unstructured data
- solution
  - using NoSQL storage devices
    - **NoSQL databases** support **schema evolution**: making schema changes as the data model of the data evolve. !
  - use **batch processing** to process data!

## Value

- the worth of data being extracted
- solution
  - data cleaning
  - Noise Filtering

## Veracity

- the quality or trustworthiness of the data
- solution
  - data cleaning
  - Noise Filtering

# 3

## Q

**Describe structured, semi-structured, and unstructured data in a Big Data Set, and give some examples.**

## structured

- frequently generated by enterprise applications and information like CRM and ERP systems. !
- often stored in **tabular form**. 

- **conforms**(follows遵循) **to a data model or schema**
- used to capture relationships between different entities. !
- example
  - banking transactions!
  - invoic1es
  - customer records

## semi-structured

- **has a defined level of structure and consistency**, but is **not relational** in nature. !
- **hierarchical** or graph-based, which is commonly stored in files that contain text.! 
- example
  - XML files
  - JSON files

## unstructured

- does not conform to a data model or data schema!
- form of data is either **textual** or **binary**
- often conveyed via files that are self-contained and non-relational
- example
  - image (binary)
  - audio (binary)
  - video (binary)
  - tweets (text file)

# 4

## Q

**Describe the Big Data Analytics Life cycle and gave some examples of automobile manufacturer or supermarket, etc.** 

数据分析: 通过销量调节生产策略(汽车), 根据日期调整供应量(超市)

## Lifecycle

### Business Case Evaluation

- (明确目标, 准备工具)

- present a clear understanding of the justification(理由), **motivation and goals** of carrying out the analysis

- any **required purchase**, such as tools, hardware and **training**, must be understood in advance

### Data Identification

- (标识)

- identifying the datasets required for the analysis project and their **sources**
- identify as many types of related data sources as possible
- sources
  - **internal datasets**: data marts, operational systems
  - **external datasets**: third-party data providers(eg. data markets), content-based web sites

### Data acquisition & Filtering

- 采集 过滤

- using web crawler
- remove corrupt data
- remove data that is considered to be of no value to the analysis

### Data Extraction

- (提取)!

- the format of some input data may be **incompatible** with the Big Data solution, so we need to **transforming** it into a format that can be used for analyzing
- example
  - user id, timestamp -> tabular form
  - XML -> tabular form

### Data Validation & Cleansing

- **establishing complex validation rules** and **removing any known invalid data**
- because often receive redundant data across different datasets, this redundancy can be used to explore interconnected datasets in order to !
  - assemble validation parameter
  - fill in missing valid data
- dataset A, dataset B… (p 91)

### Data Aggregation & Representation

- because data may be spread across multiple datasets, we can **join datasets together** via **common fields** (eg. date, ID)
- integrating multiple datasets together to arrive at a unified view

### Data Analysis

- **confirmatory analysis**!
  - bring an assumption according to the phenomenon
  - the data is analyzed to prove or disprove the assumption
- **exploratory analysis**
  - no assumptions are generated
  - explore the cause of the phenomenon

### Data Visualization

- using data visualization techniques and tools to **graphically show the analysis results** to business users effectively, so that business users can provide **feedback**
- example
  - bar charts, line graphs, scatter plots

### Utilization of Analysis Results

- support business decision-making

# 5

## Q

**Describe CAP, ACID, and BASE, and gave some examples for Big Data.**

## CAP

### Consistency

> 强一致性, 最终一致性

- a guarantee that **every node** in a distributed cluster **return the same, most recent, successful data**. !
- every client having same view of the data. 
- 数据存放在不同的服务器, 但返回相同的结果

### Availability

- every non-failing node returns **a response for all read and write requests** **in a reasonable amount of time**

### Partition Tolerant

>  能否避免单点故障导致数据丢失 

- In addition to the failure of the whole network, other failures can not cause the whole system to response incorrectly. 

### A+P

- example
  - buying a hottest phone: a few seconds ago, still have in stock, but when you click to buy, the system **prompts you that the order fails** and the goods are sold out. 
  - When a website has a large number of visits, the server may **degrade the web page** in order to provide services for a large number of users.

### C+P

- distributed database: redis
- strong consistency
- example
  - While the system is achieve **a state of consistency**, it will **sacrifice the user experience,** waiting for all data **to be consistent** before allowing the user to access the system. 

### A+C

- store everything in one server, MySQL

## ACID

> transaction management
>
> relational database management

### Atomicity

- atomicity ensures that all operations will always **succeed or fail completely**
- there are **no partial transactions**. 
- example:
  - a user attempts to update 3 records as part of a transaction, 2 records are successfully updated, and fail to update the third records, as a result, the database **roll backs** and put the system **back to its prior state**. 

### Consistency

- consistency ensures that the database will always **remain in a consistent state** by ensuring that only data that **conforms to the constrains** of the database schema can be written to the database. 
- example
  - user cannot update the a column of a float type table with a varchar type, because the value violates the constraint. 

### Isolation

- isolation ensures that the result of a transaction are **not visible to other operations until it is complete**. 
- example
- 
  - A update 2 records as part of a transaction. Before he update the second record, B attempts to update the same record, **the DB does not permit B’s update until A’s update succeeds of fails in full**, because **the record is locked by DB, until the transaction is complete**. 

### Durability

- Durability ensures that the results of an operation !are permanent. Once the transaction is complete, it cannot be rolled back. 
- example
  - A updates a record, the DB successfully updates the record, right after this update, a power failure occurs, when the power is resumed, the DB provides records based on the last update. !

## BASE

based on CAP theorem 

relaxing the strong consistency constrains 

### Basically Available

- DB will always acknowledge a client’s request, either in the form of the requested data or a success/failure notification
- example
  - the database is basically available. A network failure occurs, A and B still receive data, because the DB  is **partitioned** 

### Soft state

- database may be **in an inconsistent state** when data is read; thus, **the results may change if the same data is requested again**, because the data could be updated for consistency. 
- This property is closely related to eventual consistency. 
- example
  - A updates a record to Peer A, before the other peers are updated, B requests the same record from Peer C, the DB returned the **stale data** to B. 

### Eventual consistency

- also called *optimistic replication*
- reads by different clients immediately following a write to the DB, may not return consistent results. 
- the database will not be consistent until **changes are** **propagated** to all nodes
- while the DB is in the process of attaining the state of eventual consistency, it will be in a **soft state**
- example: 
  - A updates a record to Peer A, before the other peers are updated, B requests the same record from Peer C, the DB returned the **stale data** to B. Eventually, the data will be updated on Peer C, and the DB will be consistent again. 

# 6

## Q

**Describe the advantages and the risks of sharding(切片) and replication for RDB.**

## Sharding

- the process of **horizontally partitioning** a large dataset into a collection of smaller, more manageable datasets(shards).!

- shards are distributed across **multiple nodes**, where a node is a server or a machine
  - each shards shares the same schema
  - all shards collectively represent the complete dataset. 
  
  benefits
  - **fast processing**: since each node is responsible for only a part of the whole dataset, read/write times are greatly improved. 
  - **partial tolerance**: a node failure will only affect the data stored on that node. !
  - **horizontal scaling** can increasing a system’s capacity
  
- risks
  - one a DB is sharded, it can be very **difficult to return it to its unsharded architecture**. 
  - the shards will eventually become **unbalanced**:  Shards A is for customers whose name begin with A to M, Shards B is for customers whose name begin with N to Z, Shards A has more data. 
  - Sharding **isn’t natively supported** by every DB engine. 
  
- example

  - a dataset is spread across Node A and Node B, resulting in Shard A and Shard B, respectively. 
  - A query something that are located in Shard A and Shard B, the data will be fetched from both Node A and Node B. 

## Replication

- stores **multiple copies** of a dataset(Replicas) on multiple nodes. 

- advantage:
  - **fault tolerance** is achieved. data will not lost when an individual node fails!
  - **availability**: same data is replicated on various nodes
  - increased **parallelism**!
  - **less data movement** over network!
  
- risks

    - **increased overhead** on update: when an update is required, a DB system must ensure that all nodes are updated!
    - require **more disk space**: save copy of data need extra space
    - **expensive**: concurrency control and recovery techniques will be more advanced and hence more expensive

- example

  - a dataset is replicated to Node A and Node B, resulting in Replica A and Replica B
  
- two methods to implement replication

  - master-slave
  
    - read intensive loads
    - all data is written to a master node, once saved, the data is replicated over multiple salve nodes. 
    - master: write, insert, update, delete requests
    - slave: read requests
    - ideal for read intensive loads rather than write intensive loads
    - example: 
      1. A updates data, Master copies data to Slave A, 
      2. before the data is copied to Slave B, B tries to read the data from Slave B, which results in an inconsistent read. 
      3. The data will eventually become consistent when Slave B is updated by the Master.  
  
  - peer-to-peer
    - write intensive loads
    - all node operate at the same level. 
    
    - each node(peer), is equally capable of handing reads and writes. 
    
    - each write is copied to all peers. 
    
    - solution to write inconsistencies
    
      - pessimistic concurrency
    
        - uses locking to ensure that only one update to a record can occur at a time. 
        - The database is not available until all locks are released. 
    
      - optimistic concurrency
    
        - does not use locking
        - allows inconsistency to occur
        - eventually consistency will be achieved after all updates have propagated. 
    
    - solution to read inconsistency
    
      - voting system: a read is declared consistent if the majority of peers contain the same version of the record(requires a reliable and fast communication mechanism between the peers)
    
    - example
    
      1. A updates data
    
      2. data is copied over to Peer A. data is copied over to Peer B
        3. before the data is copied to Peer C, B tires to read the data from Peer C, resulting in an inconsistent read
        4. the data will eventually be updated on Peer C, and the database will once again become consistent. 

# 7

## Q

**The contents and examples of NoSQL Databases.**

## NoSQL DB

### features

not important

- schema-less data model
- scale out rather than scale up
- highly available
- eventually consistency
- BASE, not ACID
- Auto sharding and replication

## Type of data

#### key-value

- store data as **key-value pairs**
- act like **hash tables**
- **value cannot be queried** by the DB
- the value is **not transparent**
- partial updates are not possible, an update is either a **delete** or an **insert** operation
- do not maintain indexes, so writes are quite fast
- base on simple storage model, key-value storage devices are **highly scalable**
- example
  - **key is number**, value is text, binary(image), XML
  - redis
  - Dynamo DB

#### document

- **key-value pairs**
- **can be queried** by the DB
- can have a complex **nested structure**
- can be encoded using a **text-based encoding** schema, such as XML, JSON
- can be encoded using a **binary encoding** schema, such as BSON
- **partial updates** are supported
- example
  - MongoDB
  - CouchDB
  - Terrastore

#### column-family

- group related columns together in a row, resulting in column-families. 
- provide fast data access with random read/write capability
- example
  - SimpleDB
  - HBase

#### graph

- graph storage devices place emphasis on storing the **linkages** between entities. 
- graph storage devices provide consistency via ACID compliance. 
- example
  - Neo4J
  - Infinite Graph
  - Orient DB

# 8

## Q

Describe the rationale and examples of the batch processing and the Realtime processing.

## Batch processing

- data must be persisted to the disk before it can be processed!

- data is processed **offline** in batches and response time is vary from minutes to hours
- this work is expected to have **high latency**
- distributed and parallel computing
- based on the principle of **divide-and-conquer**!
- MapReduce is a widely used implementation of a batch processing framework. !
- MapReduce is a batch-oriented processing engine used to process large datasets using parallel processing deployed over clusters. 
- procedure
  1. a dataset is **broken down** into multiple smaller parts
  2. the data processing **algorithm is moved to the nodes** that store the data
  3. **operations are performed** on each part independently and in parallel
  4. the result from all operations are then **summarized** to get the answer

### example

calculate the total quantity of product

0. the input is divide into  splits

1. map(标上作为分类依据的标签)

   - extract product and quantity from respective split’s records in parallel. 

   - the output is key-value pair where product is the key, quantity is the value

2. combine(整合)

   - the combiner performs local summation of product quantities

3. partition(把不同部分整合到同个结点)

   - because there is only one reduce task, no partitioning is performed

4. shuffle (再整合)

   - output from two map tasks is copied to a third node

5. sort

   - the sort stage groups all quantities of the same product together as a list

6. reduce(全部结点合并)

   - sums up the quantities of each unique product in order to create the output

   ![image-20191204223721710](D:\Note\BD\BD_all.assets\image-20191204223721710.png)

## Realtime processing

- data is processed in-memory, then persisted to the disk for future use
- response time ranges from sub-second to under a min
- SCV
  - Speed
  - Consistency: accuracy
  - Volume: amount of data that can be processed
- procedure
  1. streaming data is **captured** via a data transfer engine
  2. it is simultaneously **saved** to an in-memory  storage device and an on-disk storage device. 
  3. a processing engine is used to **process data** in real time. 
  4. the results are fed to a **dashboard** for operational analysis

- EXAMPLE: STOCK , BANK

# 9

## Q

**Describe OLTP, OLAP, ETL, Data Warehouses, and Data Marts.**

## OLTP

> Online Transaction Processing

- store operational data that is **normalized**. !

- a software system that processes **transaction-oriented data** in real time, and is not batch processed. 
- perform simple database operations(insert, delete, update) against a relational database
- OLTP systems
  - point of sale system
  - ticket reservation system
  - banking system

## OLAP

> online analytical processing

- OLAP systems store **historical data** that is **aggregated** and **denormalized** !
- OLAP systems are used for processing data **analysis queries**. 
- serve as both a **data source** as well as a **data sink** that is capable of receiving data!
- OLAP systems perform long-running **complex queries** against a **multi-dimensional** databases. 

## ETL

> Extract transform load
>
> 
>
> a process of loading data from a source system(database, flat file, application) into a target system(database). 

- procedure
  1. **obtain** or **extract** required data from the sources
  2. data are **modified** or **transformed** by the application of rules
  3. data is **inserted** or **loaded** into the target system

## Data Warehouses

> a central enterprise-wide repository consisting of **historical or current** data

- usually **interface with an OLAP system** support multi-dimension analytical queries
- data are **loaded from operational systems** like ERP, CRM and SCM
- used by BI to run various **analytical queries**
- with the increase of data volume, the query will be slow, so data warehouses usually contain **optimized databases**(analytical databases), to handle reporting and data analysis tasks. 

## Data Marts

> a subset of the data stored in a data warehouse that typically belongs to a department, 

# 10

## Q

**Describe the DIKW pyramid and give some examples.**

## Data

> a collection of facts in a raw and unorganized form

- data + context = Information
- example
  - 12012012 + this is a date
- get hindsight

## Information

> cleaned data which is easier to measure, visualize and analyze for a specific purpose
>
> 
>
> description of collected facts

- know who, what, when, where

- information + meaning = knowledge
- example
  - when we ask how, when we know how the things work, the information become knowledge 
- get insight
- example
  - organize data in a way to expose relationship between various data points

## Knowledge

> understanding of how to apply information to achieve goals

- know how
- find out relationship that is not apparent
- knowledge + understanding = wisdom
- get foresight

## Wisdom

> knowledge applied in action

- use knowledge to take proactive decision
- know why do something
- know what is best