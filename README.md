# netflix-RSS-compose

As the netflix-RSS example consists of currently three containers (`netflix-RSS-eureka`, `netflix-RSS-middletier`, `netflix-RSS-edge`), we need some way to interconnect them in the docker context. To achieve this, we use Docker Compose (https://www.docker.com/docker-compose).

Docker Compose makes it easy to pull, start and interconnect several Docker containers by just providing one "recipe".
In this repository we provide a recipe to set up the netflix-RSS example and this short introduction on how to use it.

## How to set it up

First of all we need Docker and Docker Compose for this to work:
* Docker: https://www.docker.com
* Docker Compose: https://docs.docker.com/compose/install/

Now you can use the `docker-compose.yml` file in this repository to create the netflix-RSS example as follows.
**Note: To have this example working, the ports `8080`and `9090` should be free. Otherwise you have to change the port mapping in the `docker-compose.yml`.**

* Open a terminal and change to the directory where the `docker-compose.yml` file is.
* Execute the command: `sudo docker-compose up` (if you are root, you can leave out the `sudo`)

Now Docker should pull the containers if they are not present and start the netflix-RSS example.

To test the example application on your machine, you can open the URLs:

1. [http://localhost:8080/eureka](http://localhost:8080/eureka)
2. [http://localhost:9090/jsp/rss.jsp](http://localhost:9090/jsp/rss.jsp)

When the system has started properly (usually after 2-3 min) you can add RSS links to the input field on the second URL [2]. and see them in the listing below.

## How to use the example for monitoring
Will be added soon
