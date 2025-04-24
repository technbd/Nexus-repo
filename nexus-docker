## Nexus Repo on Docker:

To install Sonatype Nexus Repository Manager using Docker, you can follow these steps. 


### Prerequisites:
- Docker installed
- Docker Compose (optional, but recommended for PostgreSQL setup)


#### Jenkins plugins:
  - Nexus Artifact Uploader 


### Option 1: Run with docker run:

To run, binding the exposed port 8081 to the host, use: 

```
docker run --name nexus -d -p 8081:8081 sonatype/nexus3
```




### Option 2: Run with docker compose:

Create a `docker-compose.yaml` file:

```
services:
  nexus:
    image: sonatype/nexus3
    container_name: nexus
    restart: always
    volumes:
      - ./nexus_data:/nexus-data
    ports:
      - "8081:8081"
      - "8085:8085"
#volumes:
#  nexus_data: {}
```



```
docker compose -f docker-compose.yaml config
```


```
docker compose up -d
```



### Access Nexus:


_The default admin password is stored inside the container:_

```
docker exec -it nexus cat /nexus-data/admin.password
```


Once everything is up, go to `http://server_ip:8081`

Default credentials:
- Username: admin
- Password: Admin#123456




### Create repositories on Nexus:

Create a private (hosted) repository for our own images. 

What we will do:
- Create a private (hosted) repository for our own images.
- Create a proxy repository pointing to Docker Hub or others. 
- Create a group repository to provide all the above repos under a single URL.


#### Private repository: 

1. `Settings` → `Repositories` → click `Create repository`:
    - select `Maven 2 (hosted)`
      - Name: `nexus-jenkins-repo`
      - [✓] If checked, the repository accepts incoming requests

      - Maven 2:
        - Version policy: Mixed
        - Layout policy: Permissive 

      - Storage:
        - Blob store: default 
        - Strict content type validation:
          - [✓] Validate that all content uploaded to this repository is of a MIME type appropriate for the repository format

      - Hosted
        - Deployment policy: Allow redeploy

      - Cleanup:
    - click `Create repository`



#### Proxy repository:

1. `Settings` → `Repositories` → click `Create repository`:
    - select `Maven 2 (proxy)`
      - Name: `nexus-jenkins-proxy`
      - [✓] If checked, the repository accepts incoming requests

      - Maven 2:
        - Version policy: Mixed
        - Layout policy: Permissive 

      - Proxy:
        - Remote Storage: `Enter a URL`
        - Blocked:
          - Auto bloking enable: [] Auto-block outbound connections on the repository if remote peer is detected as unreacable/unresponsive
          - Maximum component age:
          - Maximum metadata age:
      - Storage:
        - Blob store: default 
        - Strict content type validation:
          - [✓] Validate that all content uploaded to this repository is of a MIME type appropriate for the repository format
        - Routing role: 
        - Negative cache:
        

      - Cleanup:
    - click `Create repository`




#### Group repository:

1. `Settings` → `Repositories` → click `Create repository`:
    - select `Maven 2 (group)`
      - Name: `nexus-jenkins-group`
      - [✓] If checked, the repository accepts incoming requests

      - Maven 2:
        - Version policy: Mixed
        - Layout policy: Permissive 

      - Storage:
        - Blob store: default 
        - Strict content type validation:
          - [✓] Validate that all content uploaded to this repository is of a MIME type appropriate for the repository format

      - Group
        - Member repositories: 

    - click `Create repository`






### Links:
- [Nexus Repository | hub.docker.com](https://hub.docker.com/r/sonatype/nexus3/)
- [Nexus | Docker](https://medium.com/@chiemelaumeh1/install-sonatype-nexus-3-using-docker-compose-setup-nexus-repository-manager-for-node-js-project-47a3c5efe1ee)
- [Nexus Repository 3](https://www.sonatype.com/blog/using-sonatype-nexus-repository-3-part-3-docker-images)
- [Nexus Container Registry](https://octopus.com/docs/packaging-applications/package-repositories/guides/container-registries/nexus-container-registry)






