# (RE)presentational (S)tate (T)ransfer API Basics (REST)

### Six Design Rules/Constraints define characteristics of REST systems

1. **Uniform Interface**: This constraint defines the interface between the clients and servers.  It simplifies and decouples the architecture which enables each part to evolve independently.  

4 Principles Guiding this Interface
---------------------------------------
* *Resource-based* - individual resources are defined using URIs as resource identifiers.
* *Manipulation of Resources through Representations* - Client will have enough information to modify or delete the resource on the server if it has permission to do so.  
* *Self-Descriptive Messages* - Each message includes enough information to describe how to process the message.  e.g. which parser to use.
* *Hypermedia a the Engine of Application State (HATEOAS)* - Clients deliver state via body contents, query-string parameters, request headers and the requested URI (the resource name).  Services deliver state to clients via body content, response codes, and response headers.  (technically referred to as hypermedia)
2. **Client-Server**: Separation between a service offering server and service consuming client.  By creating this differentiation, we increase portability of the user-interface and increase scalability by simplifying server components.  
3. **Stateless**: Session state is kept completely on the client.  Communication between client-server must be stateless in nature, such that each request from client to server must contain all of the relevant information necessary to understand the request.  Additionally, if state is needed for multiple requests, the client is responsible for resending that state. Resource State is the data that defines the resource representation - the data stored in the database, for instance.  Application State is what the server needs in order to fulfill a request.  Application State can vary by client, and per request, while Resource state is constant across every client who requests it.  

The following properties are affected by this constraint:
* visibility - improves because a monitoring system does not have to look beyond a single request.
* reliability - eases the task of recovering from partial failures.
* scalability - improved because the server doesn't have to manage resource usage across requests.  

Obvious design trade-offs occur from this constraint.  A decrease in network performance by increasing repetitive data sent in a series of requests, since data cannot be left on the server in a shared context.  Client-side control of state reduces server control over consistent application state.  

4. **Cache**: clients can cache responses, so these responses must specify whether or not they are to be cached.  This enables the client to re-use data from a previous response for later, equivalent requests.

Advantages include: increased scalability, efficiency and user-perceived performance by reducing latency in interactions.  
Disadvantages include: Cache use can decrease reliability if stale data within cache differs significantly from the data that would be obtained had the request beens sent directly to the server.   

5. **Layering**: Provides encapsulation of services.  Client cannot tell if they are connected directly to the end server or to an intermediary along the way.  These intermediary servers improve scalability by enabling load balancing and providing shared caches.  Layers also can enforce security procedures.  

6. **Code on Demand**: Servers can temporarily extend functionality of the client by transferring logic to be executed.  e.g. client-side scripts such as javascript.  

### REST Architectural Elements





##### Resource List:
1. [Pearson E-College Rest API Tutorial](http://www.restapitutorial.com)
2. [Fielding Dissertation Chapter 5](http://www.ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm)
