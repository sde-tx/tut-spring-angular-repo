# Section: The API Gateway

* Build an API Gateway to control the authentication and access to the backend resources using Spring Cloud.

Make the UI server into a reverse proxy to the backend resource server

An API Gateway is a single point of entry (and control) for front end clients, which could be browser based (like the examples in this section) or mobile. The client only has to know the URL of one server, and the backend can be refactored at will with no change, which is a significant advantage. There are other advantages in terms of centralization and control: rate limiting, authentication, auditing and logging. 


Trouble shooting
1. Depending on the dependencies on the local, may need to add dependency below to pom.xml of ui
```
<dependency>
    <groupId>org.aspectj</groupId>
    <artifactId>aspectjtools</artifactId>
    <version>1.8.13</version>
</dependency>
```