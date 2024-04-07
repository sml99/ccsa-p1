# ownCloud Service Deployment

## Student Information

- **Name:** Smail Dahmani
- **Email:** smaildahmani@correo.ugr.es

## Development and Production Environment

- **Operating System:** Windows11 x64
- **Containerization Tools:** Docker 24.0.7 (build afdd53b), Docker-compose v2.23.3-desktop.2
- **Test/Production Server:** [Description of the test/production environment, e.g., Virtual Machine on AWS EC2, Digital Ocean, etc., with specifications]

## Practice Description

This practice involves deploying an ownCloud service using Docker containers, Docker-compose, and optionally Kubernetes to manage different service architectures based on system requirements. Services for user authentication with LDAP, database management with MariaDB, cache management with Redis were implemented, and optionally a load balancer with HAProxy.

## Deployed Services and Configuration

### Scenario 1: Small Business or Department - Small User Group

#### ownCloud Deployment
Sets up the core service for file sharing and collaboration, accessible via a web interface.
![owncloud](https://github.com/sml99/ccsa-p1/assets/29798184/1f9631cd-39c6-45ee-a32a-a1e692d983a2)

- **Container:** ownCloud
- **Port:** 8080
- ![image](https://github.com/sml99/ccsa-p1/assets/29798184/87bcb6de-cd7b-4f85-b702-9acef303277a)


#### MariaDB Database
Provides the relational database backend for ownCloud, storing application data including user information and files metadata.
![mariadb](https://github.com/sml99/ccsa-p1/assets/29798184/956a023b-9e9a-430c-9de4-68969411c4bb)

- **Container:** MariaDB

#### Cache Management with Redis
Enhances performance through caching mechanisms, reducing load times and database queries for frequent operations.
![redis](https://github.com/sml99/ccsa-p1/assets/29798184/b078e2de-fbe3-4378-9046-986bdacbb971)

- **Container:** Redis

#### User Authentication Service with LDAP
Integrates a directory service for centralized user management and authentication, simplifying user access control.
![ldap](https://github.com/sml99/ccsa-p1/assets/29798184/6493b473-c205-41f6-82df-9b4692461f57)

- **Container:** OpenLDAP

#### LDAP GUI Service using phpldapadmin
Offers a graphical interface for managing LDAP server settings and entries, improving ease of administration.
![phpldap](https://github.com/sml99/ccsa-p1/assets/29798184/a1a70189-4b0e-49ce-9b92-646a2782a45e)

![image](https://github.com/sml99/ccsa-p1/assets/29798184/9d8b2d3a-77d0-4b3f-b28b-ec7908c392d5)

- **Container:** phpldapadmin

#### Network file system 
Implements a storage solution that allows for shared file access across the network, demonstrating an alternative to direct disk storage.
  ![nfs](https://github.com/sml99/ccsa-p1/assets/29798184/0fa7c0bc-c602-4720-9670-80c76fdf4e14)

- **Container:** nfs-server
![image](https://github.com/sml99/ccsa-p1/assets/29798184/4dfa325b-1ffb-4927-8da8-d44c911a5a82)

### Scenario 2: Medium-sized Company

### Volumes
![volumes](https://github.com/sml99/ccsa-p1/assets/29798184/1e4bfdb3-87c8-4ae8-a62a-837d4b11308d)

- **nfs:** Stores persistent data for ownCloud with shared access, mapped to an NFS server container for high availability.
- **mysql:** Holds MariaDB master database data, using local storage for persistence of user and application data.
- **mysql_slave:** Stores data for the MariaDB slave, aiding in data redundancy and load distribution through replication.
- **redis:** Contains Redis data for caching to improve performance and response times, employing local storage for cache data persistence.

### Services

- **haproxy:** Provides load balancing for ownCloud servers, optimizing traffic distribution to ensure high availability.
  ![haproxy](https://github.com/sml99/ccsa-p1/assets/29798184/60e97ff3-6ed2-42a2-8d97-d199de33c5f6)

- **ocserver:** The ownCloud server container offering file sharing and collaboration, in this scenario We have to replicas of this service.
  ![oc](https://github.com/sml99/ccsa-p1/assets/29798184/c3d2e8a0-7dd1-4066-98fc-fc238556f24e)

- **mariadb_master:** The primary MariaDB service for ownCloud, configured for reliability and performance with health checks.
  ![mdb](https://github.com/sml99/ccsa-p1/assets/29798184/537c58ca-af5b-4fec-93b9-5a486b3071b0)

- **mariadb_slave:** A replica database for read scalability and backup, synchronized with the master database.
  ![sdb](https://github.com/sml99/ccsa-p1/assets/29798184/043f44a0-8a8a-40d1-aa03-0a0b07f837ff)

- **redis:** Enhances ownCloud performance by caching session and configuration data in memory, reducing database load.
- **ldap:** Centralizes authentication for ownCloud with LDAP, using environment variables for secure configuration.
- **phpldapadmin:** A web-based tool for managing the LDAP server, facilitating easy administration of LDAP entries.
- **nfs-server:** Simulates an NFS server within Docker, providing shared storage for ownCloud data across instances.


### Network

- **owncloud-net:** A Docker bridge network enabling secure, isolated communication between containers, essential for the ownCloud ecosystem.


## Bibliographic References and Resources Used

- Docker Documentation: https://docs.docker.com/
- OpenLDAP Official Website: https://www.openldap.org/
- MariaDB Docker Image: https://hub.docker.com/_/mariadb
- ownCloud Official Website: https://owncloud.com/
- HAProxy Documentation: http://docs.haproxy.org/
