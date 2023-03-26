Requirements

0-simple_web_stack
------------------

• What is a server
A server is a piece of computer hardware or software that provide services to other computers called clients. The services include data sharing, web page rendering, mail provision e.t.c. The various kinds of servers include web servers, file servers, application servers, database servers e.t.c.

• What is the role of the domain name
The domain name is to enable a particular server's location to be easily remembered, it identifies a server's numerical IP address with a human-readable name
• What type of DNS record www is in www.foobar.com
It is an A record, it translates foobar.com to it's corresponding IP address

• What is the role of the web server
A web server is a piece of software on a dedicated hardware that facilitates serving of web pages to client devices. It serves up the static content of a page

• What is the role of the application server
Application server delivers business application to client dynamically, with the use of Application Programmable Interfaces (APIs), the contents are readily available to software developers

• What is the role of the database
The databases allow multiple users at the same time to quickly and securely access and query the data using highly complex logic and language. (Source: https://www.oracle.com/ke/database/what-is-database/)

• What is the server using to communicate with the computer of the user requesting the website
It uses HTTP protocols for communication 


The issues with this infrastructure 
• SPOF
Multiple infrastructure do not exist, so if one infrastructure goes down, services to the client will be automatically interrupted

• Downtime when maintenance needed (like deploying new code web server needs to be restarted)
When deploying new code, the server has to be temporarily unavailable which would cause service unavailability 

• Cannot scale if too much incoming traffic
There are not multiple servers that can distribute load, this infrastructure cannot handle too much incoming traffic and therefore cannot scale



1-distributed_web_infrastructure
--------------------------------

• For every additional element, why you are adding it
Load balancer: 
• This was added to reduce the work-load on individual servers.
• To enable concurrent use of multiple servers which boosts efficiency 
• It makes the servers respond more quickly which helps boost performance 
• Single point of failure is reduced. When one server fails, the active one provides availability 
A second server:
• To reduce the single point of failure (SPOF)
• To maximise availability and minimise downtime 



• What distribution algorithm your load balancer is configured with and how it works
Round robin: it passes each new connection request to the next server in line, eventually distributing connections evenly across the array of servers being load balanced

• Is your load-balancer enabling an Active-Active or Active-Passive setup, explain the difference between both:
It is enabling an active-active setup
In the active-active peer setup, both servers are actively handling user requests concurrently, while in the active-passive setup, only one server is active and the other one is passive or standby and only becomes effective when the active server fails 

• How a database Primary-Replica (Master-Slave) cluster works:
Master-slave replication enables data from one database server (the master) to be replicated to one or more other database servers (the slaves). The master logs the updates, which is effected on the slave. There is synchronous and asynchronous Replication.

• What is the difference between the Primary node and the Replica node in regard to the application:
The primary node is the node that receives all write operation from the client application, it logs the updates received. The Replica node has an instance of the updates received from the primary node

• You must be able to explain what the issues are with this infrastructure:

• Where are SPOF
• The dns server 
• The load balancer

• Security issues (no firewall, no HTTPS)
• Since there is no firewall, incoming and outgoing traffic cannot be monitored and intrusion detection is not possible 
• The communication is also nor secure as no HTTPS is used, therefore hackers can intercept and collect information about the client's traffic

• No monitoring
The state of each server cannot be known since there's no monitoring



2-secured_and_monitored_web_infrastructure
------------------------------------------





3-scale_up
----------
