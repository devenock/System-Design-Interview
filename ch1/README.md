# Chapter 1: SCALE FROM ZERO TO MILLIONS OF USERS

Designing scalable systems is challenging because it is a journey that 
involves continuous improvements and endless refinements.

In this chapter, we design a system that supports a single user and gradually scale it up
to support millions of users.

## Single Server Setup
A journey of a thousand miles begins with a single step, and building a complex system 
is no different. To start with something simple, everything is running on a single server
web app, database, cache, etc.

![figure 1:1](./assets/fig1.png)

#### Request Flow and Traffic Source
To understand this setup well, let us examine the flow of the request and where the system traffic comes from.

![figure 1:1](./assets/fig2.png)

#### Request flow:
1. Websites are accessed through Domain Names e.g _api.mysite.com_ .
2. After that an IP is returned to the web browser or the mobile app. The IP is always associated with the domain name and resolved by the DNS(Domain Name System)
3. Once the IP address has been obtained HTTP requests are sent directly to the web server to request for the resources.
4. The web server then returns HTML pages or JSON response to be rendered on the browser or the app.

#### Sources of Traffic:
The traffic in this setup comes from two sources: **_web browser_** and the _**mobile app**_.

## Database
As the user base grows, we need multiple servers to cope with the growing traffic since one server will be overwhelmed.

We have one for the **_web/mobile traffic_**(web tier) and another one for the **_database_**(database tier). Separating the web/mobile and database servers allows them to be **_scaled_** independently.
![figure 1:1](./assets/fig3.png)
### Databases to Use
You can always choose between Relational DBs or Non-Relational DBs. Relational DBs store data in tables(rows and columns) e.g MySQL, PostgreSQL, OracleBD. 
Non-relational DBs store unstructured data and are grouped into document stores, graph stores ,key-value stores, and column stores, e.g: MongoDB, CouchDB, Neo4J, Cassandra, HBase, Amazon DynamoDB.
You can perform JOINS in relational DBs while NoSQL do not permit performing JOINS.

Most developers prefer Relational databases because they have been around for the longest time and have worked well for their use-cases. However if relational databases are not suitable for your use-case, non-relational DBs comes handy.

To understand if NoSQL is the right choice for your application:
1. Your application requires super-low latency.
2. Your data is unstructured or, you don't have any relational data.
3. You only need to serialize and deserialize data(JSON, XML, YAML, e.t.c)
4. You need to store a massive amount of data.

### Vertical Scaling vs Horizontal Scaling
**Vertical scaling**, also referred to as "scale up" involves adding more power(CPU/RAM) to the server. **Horizontal scaling** also referred to as "scale out" involves adding more servers into your pool of resources.

When the **system traffic** is low, vertical scaling works well due to it's simplicity but it comes with different limitations.
1. Vertical scaling has a hard limit because you can not add unlimited CPU and memory to a single server.
2. Vertical scaling does not have failover and redundancy hence if the server goes down, the website/app goes down with it completely.

Horizontal scaling is suitable for large scale applications due to the limitations of vertical scaling.

In the previous design users connected to the application server directly. Users will be unable to access the website if the server is offline. Additionally, if many users access the web server simultaneously, 
and the server reaches it's load limit, users will generally experience slower response or fail to connect to the server. Therefore, a **load balancer** is the right solution for this.

## Load Balancer
A load balancer evenly distributes incoming traffic among existing web servers that are defined in a load-balanced set.
![figure 1:1](./assets/fig4.png)
### Illustrations:
Users connect directly to the load balancer using a public IP. This setup makes it impossible for clients(web/mobile) to reach the web servers directly anymore. 
**Private IPs** are used for communication between the servers for security purposes. 
A private IP is an IP address that reachable by only servers on the same network but unreachable over the internet.
The load balancer communicates with web servers through private IPs.

After a load balancer and a second web server are added, we successfully solved the problem of failover and improved the availability of the web tier. Details explained below:
1. If server 1 goes offline, all the web traffic will be routed to server 2. This prevents the website from going offline. We will also add another new web server to the server pool to balance the load.
2. If the website traffic grows rapidly, and two servers are not enough to handle the traffic, the load balancer will handle this problem gracefully. You only need to add more servers to the web server pool and the load balancer starts to send requests to them.

Now the web tier looks good, what about the data tier? The current design has one database and hence does not support failover and redundancy. Database replication is a common practice to address these problems.

## Database Replication
Database replication can be used in many database management systems,usually with **master/slave** relationship between the **original**(master) and the **copies**(slave).

A master database generally only supports **_write_** operations. A slave database gets copies of the data from the master database and only supports **_read_** operations.

All the data-modifying commands like `insert`, `update` and `delete` must be sent to the master database. Most applications require a much higher ratio of reads to writes; thus the number of slave databases in a system is usually larger than the number of master databases as illustrated in the figure below.
![figure 1:1](./assets/fig5.png)
