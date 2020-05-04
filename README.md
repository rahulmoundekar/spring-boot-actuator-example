# Spring Boot Actuator :

The spring-boot-actuator module provides all of Spring Boot’s production-ready features. The simplest way to enable the features is to add a dependency to the spring-boot-starter-actuator ‘Starter’.

Spring Boot Actuator is available since April 2014, together with the first Spring Boot release.

With the release of Spring Boot 2, Actuator has been redesigned, and new exciting endpoints were added.

In essence, Actuator brings production-ready features to our application.
Monitoring our app, gathering metrics, understanding traffic or the state of our database becomes trivial with this dependency.

The main benefit of this library is that we can get production grade tools without having to actually implement these features ourselves.

Actuator is mainly used to expose operational information about the running application – health, metrics, info, dump, env, etc. It uses HTTP endpoints or JMX beans to enable us to interact with it.

Once this dependency is on the classpath several endpoints are available for us out of the box. As with most Spring modules, we can easily configure or extend it in many ways.
#### Getting Started

  - To enable Spring Boot Actuator we'll just need to add the spring-boot-actuator dependency to our package manager. In Maven:
    ```
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-actuator</artifactId>
    </dependency>
    ```
  - Endpoints :Most applications choose HTTP, where the ID of the endpoint along with a prefix of /actuator is mapped to a URL. For example, by default, the health endpoint is mapped to /actuator/health.
    
    * /health – Shows application health information (a simple ‘status' when accessed over an unauthenticated connection or full message details when authenticated); it's not sensitive by default
    * /info – Displays arbitrary application info; not sensitive by default
   
    
  - Enabling Endpoints (application.properties):
    ```java
    management.endpoints.enabled-by-default=false
    management.endpoint.info.enabled=true
    ```
 - you could include it in your application.properties, as shown in the following example but this is static way:
     ```java
     spring.profiles.active=dev
     ```
  - run on your Postman
    * The /health endpoint is used to check the health or state of the running application. It's usually exercised by monitoring software to alert us if the running instance goes down or gets unhealthy for other reasons. E.g. Connectivity issues with our DB, lack of disk space…
         ```java
        {
            "status" : "UP"
        } 
        ```
    * We can also customize the data shown by the /info endpoint – for example: 
        ```java
       info.app.name=Spring Application
        info.app.description=This is spring boot application
        info.app.version=1.0.0
        ```
        ```java
        {
            "app" : {
                "version" : "1.0.0",
                "description" : "This is spring boot application",
                "name" : "Spring Application"
            }
        }
        ```
    * http://localhost:8080/actuator/
         ```java
        {
            "_links": {
                "self": {
                    "href": "http://localhost:8080/actuator",
                    "templated": false
                },
                "health": {
                    "href": "http://localhost:8080/actuator/health",
                    "templated": false
                },
                "health-path": {
                    "href": "http://localhost:8080/actuator/health/{*path}",
                    "templated": true
                },
                "info": {
                    "href": "http://localhost:8080/actuator/info",
                    "templated": false
                }
            }
        }
        ```
