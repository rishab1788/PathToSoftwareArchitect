Architecting Solution with platform & Frameworks
* Platforms for
    * WebApps
    * Services
    * Datastores
    * Analytics
* Platform Functionality
* Platform Architecture
    * Performance
    * Scalability
    * Reliability
* Platform Use-cases
* Platform Alternatives
* Architecting Solution
    * End-to-End
 
Refrence System 
<img width="1158" alt="image" src="https://github.com/user-attachments/assets/53bea21a-6eef-424a-b4a6-717f5aeafb3e">
build the system. functionallity of the product 


Web Applications - (Frontend Systems.) DB gets less load.
Request load every request to frontend and may or may not be sent to DB.

Solutions for WebApplications - 
* Static Content
    * Apache Web Server
    * Nginx web server
    * Cloud storage
* Dynamic Content
    * Web server - apache HTTPD, NodeJS
    * Java Web Container - Tomcat, Jettey, Spring-boot
* Content Caching
    * Ngnix
* Content Distribuition
    * CDN

Apache WebServer - 
   * Store Static Content - (cache in RAM Disk take alot of time)
     * HTML/CSS/JS files 
     * Images Files 
     * Documents
   * Genreate Dynmiac Content - php, scripts - apahce will fetch data from page
      * Get Data & gennerate pages 
      * PHP, python, perl
      * No JSP/Servlets
   * Act As a reverse proxy - not great

  Apache Webserver Architecture - Request Response model
  <img width="1167" alt="image" src="https://github.com/user-attachments/assets/df22375c-b41b-4e4d-a531-489a16edbd3c">

apache as webserver (CPU Bound)

      [Webserver]
LB -> [Webserver]
      [Webserver]



NGNIX Webserver - 
   Store Static Content
      * HTML/CSS/JS files 
      * Images Files 
      * Documents
    Generate Dynamic Content - Not the best
    Act as REverce Proxy -
    Really well

   NGING Architecture - event-driven

<img width="1167" alt="image" src="https://github.com/user-attachments/assets/f82400d1-c3f3-4d74-9d9e-4d2183269936">

one single thread T1 -> only one 1 million connection handling is done.
Reverse proxy - 

WebContainers (complex logic, servlet logic, ) & Spring Framework 
Tomcat and jetty - Servlet engineer
Applocation Servers -
wildfly]/Jboss 
Sprint boot 
* runs embedded web container - tomcat, jetty
  
MVC architecture 
* Servlets for logic
* JSP for presentation

Spring Containers 
*Runs inside a web container
* provides
     * IOC/DI
        * For business logic 
     * MODEL view controller
       * For frontends
     * JDBC TEMPLATE
        * For accessing DB
     * Connection pools
        * HTTP, DB

Web server
Jetty is also a web server. It can be used to monitor a network, server, storage, cloud, containers, and more.     

Jetty & Spring                         webapp 
                                 [JETTY/spring]
[Webbrowser] ----> [NGNIX] --->  [JETTY/spring]  
                                 [JETTY/spring]   

Node.Js
   * HTTP Server
   * uses javascript engine to process requests
   * Highly efficient at handling a large number of connections
     * For requests that are IO-bound (very less time either making DB or file operations) and not CPU-bound
     * Single thread to handle all connections
          * Saves memory
          * Avoids context switching

<img width="1167" alt="image" src="https://github.com/user-attachments/assets/e46e3f49-725a-42ee-a0b9-a85f00cb9a74">

node.js never vacant the CPU it continues to run it with a single thread.
Poll IO

For incoming network calls, we always make an async way.

Cloud Solution for Web - 
Manged Services - 
   * Hardened Solutions
   * Automated deployment
   * Built-in Scalability & reliability
   * Global deployment solutions

