# 2 types of databases

## 1. Relational

### Advantages:
    -it has been legacy and hence most of the services would still be using it
    - alloows join operations


## 2. Non-relational 

### Dis-advnatages
1. join operations are generally not supported


### 4 Crucial Types
1. key-value stores
2. column stores
3. document stores
4. graph stores

### When to use: 
• Your application requires super-low latency.
• Your data are unstructured, or you do not have any relational data.
• You only need to serialize and deserialize data (JSON, XML, YAML, etc.).
• You need to store a massive amount of data



# Vertical and Horizontal Scaling

Vertical scaling, referred to as “scale up”, means the process of adding more power (CPU, RAM, etc.) to your servers. Horizontal scaling, referred to as “scale-out”, allows you to scale by adding more servers into your pool of resources.


- when traffic is low vertical scaling is a great option


### vertical scaling limitations

1. has a hard limit --> cant really scale a single server INFINITELY by adding resources
2. adter adding all this shit, it still does not have failover and redundancy as if that one server goes down - everything goes down





## TRANSITION TO ADDING LOAD BALANCER --> In another scenario, if many users access the web server simultaneously and it reaches the web server’s load limit, users generally experience slower response or fail to connect to the server. A load balancer is the best technique to address these problems.


# Load Balancer

1. A load balancer evenly distributes incoming traffic among web servers that are defined in a load-balanced set.
2. Now we are NOT exposing the ip address of our server but the IP address of the Load Balancer itself.
3. For security we have a PUBLIC IP fot Load Balancer && internally the LB can communicate with Server using PRIVATE IP Addresses


### PROGRESS

AFter adding a load balancer and a second web server, we successfully SOLVED **no failover issue** and **improved availability of the web tier**: 

1. If one server goes offline, all the traffic will be routed to server which prevents the website from going offline  --> In that time we can also add a new healthy web server to the server pool to balance the load.
2. If the website traffic grows rapidly and the current servers are not enough to handle the traffic --> the LOAD BALANCER can handle this problem gracefully till then by distributing the requests --> this wpuld result in delay of responses for people in back in queue --> BUT --> atleast the people that are using the app would not have slow processes --> BASICALLY, it helps us to "NOT FUCK IT UP FOR EVERYONE" --> Meanwhile we can add more servers though


# Strenthening Database Tier

- we still have a sibgle db which is basically a single point of failure for the application && can also get overwhelmed --> need to do something about this

## Database Replication

