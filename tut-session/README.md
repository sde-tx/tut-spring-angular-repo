* https://spring.io/guides/tutorials/spring-security-and-angular-js/

# Section: The Login Page, The Resource Server <br>

> Root <br>
> &nbsp;&nbsp;&#9495; pair-session <br>
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#9495; ui-session <br>
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#9495; resource-session <br>

Prepare Redis server
1. Install Docker
2. Launch Docker Quickstart Terminal
   - docker pull redis
   - docker run --name my-redis -d -p 6379:6379 redis

Set configuration for Redis in Spring Boot
1. Add configuration below to application.yml of both child projects
```
spring:
  ...
  redis:
    host: 192.168.99.100 // <-- user can get this ip from docker quickstart terminal
    port: 6379
```
