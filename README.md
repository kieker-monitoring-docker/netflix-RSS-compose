# Netflix-RSS Example with Kieker

As the [netflix-RSS](https://github.com/Netflix/recipes-rss/wiki) example consists of currently three components (`netflix-RSS-eureka`, `netflix-RSS-middletier`, `netflix-RSS-edge`), we need some way to interconnect them in the docker context. To achieve this, we use Docker Compose (https://www.docker.com/docker-compose).

Docker Compose makes it easy to pull, start and interconnect several Docker containers by just providing one "recipe".
In this repository we provide a recipe to set up the netflix-RSS example and this short introduction on how to use it.

We used the [inspectIT Docker setup](https://inspectit-performance.atlassian.net/wiki/display/SAM/Netflix+RSS+Demo+Application) as a reference to set up an example that is similar to theirs but with Kieker instrumentation instead of inspectIT.

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

When the system has started properly (usually after 2-3 min) you can add RSS links to the input field on the second site ([http://localhost:9090/jsp/rss.jsp](http://localhost:9090/jsp/rss.jsp)) and see them in the listing below.

## How to use this example for analysis
As the containers are instrumented with Kieker, the monitoring logs can be found in `/tmp/netflix-rss/{edge|eureka|middletier}/logs`.
This data can be used for a trace analysis for example.

### Trace analysis with Kieker
To be able to do a trace analysis you have to download and extract the Kieker release ([http://kieker-monitoring.net](http://kieker-monitoring.net)).

This is an example of what you could do with the data. For further details on what else you can do with the monitored data, please refer to the Kieker documentation ([http://kieker-monitoring.net/documentation/](http://kieker-monitoring.net/documentation/)).

Steps:

1. Change into the `bin` folder in the extracted Kieker release folder.
2. Create a folder where the output file should be stored (in this case we assume this to be `/tmp/netflix-rss/trace-analysis`)
3. Execute `./trace-analysis.sh -i $(find "/tmp/netflix-rss" -type d -name kieker-*) -o "/tmp/netflix-rss/trace-analysis" --plot-Deployment-Operation-Dependency-Graph --ignore-invalid-traces` to do the trace analysis.
4. To convert the analysis data to PDF format, issue the command: `./dotPic-fileConverter.sh /tmp/netflix-rss/trace-analysis pdf`
5. Now there should be a PDF file representing the plotted monitored traces in the `/tmp/netflix-rss/trace-analysis pdf` folder.
6. 

### Customizing the monitoring
If you want to change the configuration for the monitoring right from the beginning you can provide your own configuration files (`kieker.monitoring.properties`, `aop.xml`). To do so, place them in the following directories:
* `/tmp/netflix-rss/{edge|eureka|middletier}/config/kieker.monitoring.properties`
* `/tmp/netflix-rss/{edge|eureka|middletier}/config/META-INF/aop.xml`

These files will replace the default configuration.
