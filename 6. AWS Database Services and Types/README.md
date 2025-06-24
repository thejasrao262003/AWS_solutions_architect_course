
# AWS Database Services and Types

## AWS Database Portfolio(SQL and No SQL)

- Refer to aws_different_databases.png for understanding what are all the database services present and what category of database do they fall into (Relational, Document etc)
- Our focus is mainly on **RDS**, **DynamoDB**

## AWS Relational Database (RDS)
- It is often called as tabled data.
- Data is always stored with fixed schema in the form of rows and columns.
- The different types of SQL commands are:
    - **DDL**: create, alter, drop etc.
    - **DML**: insert, update, delete etc.
    - **DQL**: select.
    - **DCL**: grant, revoke etc.
    - **TCL**: commit, rollback etc.
- The relational database schemas are fixed.

### The different relational databases are:
- **Aurora**
- **MySQL**
- **PostgreSQL**
- **MariaDB**
- **Oracle**
- **Microsoft SQL Server**
- **IBM DB2**

### Note:
- **Aurora** -> (Cloud database) and it is Amazon proprietary, serverless.
    - Compatible with MySQL, PostgreSQL.
    - 5x faster than MySQL, 3x faster than PostgreSQL.
    - Creates 6 copies in 3 availability zones.
    - Creates 15 read replicas and updates each replica in 10ms.

### RDS Multi AZ Deployment:
- Deploy database in multiple Availability Zones.
- One is for write. The other ones just synchronize data and act as fault-tolerant systems.
- If the primary DB fails, the standby will change to primary, and once the old primary DB is up, that is made the new standby.

### AWS RDS Read replicas:
- Creates multiple read replicas to handle load.
- The updates to read replicas happen asynchronously.
- There will be a delay for the new data to be shown in the read replicas (within 10ms).
- Stale data for a few milliseconds.
- Burstable classes have the ability to take more stress.

## AWS Database Caching Strategy

### i) Lazy loading:
- We don't want to fetch frequently accessed data from memory always. So instead, we store it in cache to be able to fetch it easily and quickly.
- **Disadvantages**:
    - Each cache will have a TTL. If TTL is 30 minutes, the data won't change till 2:30.
    - So in case data changes in the database, for 30 minutes, the change won't be shown.
    - This can lead to discrepancies.

### ii) Write through:
- Changes made in the database will be made in the cache as well.

### Eviction strategy:
- FIFO (First-In-First-Out)
- LFU (Least Frequently Used)
- LRU (Least Recently Used)

## AWS DynamoDB

### Features:
- **NoSQL**
- **Key-Value**
- Serverless database of Amazon.

### Characteristics:
- Designed to handle 10 trillion requests per day.
- Use case:
    - E-commerce applications.
    - Creating player profile pages.
- It can provide **single-digit (0-9) ms latency**.

### When you create a DynamoDB table:
- Creating partition/primary key is mandatory.
- Represented as items → collection of attributes.
- In DynamoDB, item size should not be greater than 400KB.
    - If more than 400KB, store in S3 and put the link in DynamoDB.

- **Dynamo + Cache → DAX** (DynamoDB Accelerator) 0-9 microseconds latency.
- **RCU (Read Capacity Unit)**:
    - **Eventual Consistency Read**.
    - **Strong Consistency Read**.
- **WCU (Write Capacity Unit)**:
    - For 1 WCU, 1KB of data.

### Note:
- DynamoDB replicates data across 3 Availability Zones and takes 1000ms.
    - AZ1, AZ2, and AZ3 are the 3 AZs.
- **For Eventual Consistency**:
    - Allows you to read from other replicas before the write happens to each replica (get stale data).
    - This is suitable when you don’t care about the correctness of data for a latency of 1 second.
    - Example: Streaming match data.
    - In 0.5 RCPU, it can read 4 KB, or 8 KB per 1 RCPU.
- **For Strong Consistency**:
    - Doesn’t allow you to read from other AZs until data is replicated throughout all replicas.
    - Example: Booking systems, financial transactions.
    - This approach is usually slower. In one RCPU, we can read only 4 KB of data.

### DynamoDB is good for **read-heavy purposes**:
- Example: **E-Commerce**.
