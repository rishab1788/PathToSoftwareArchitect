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
  
  
