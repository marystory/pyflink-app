## pyflink application example with Docker and docker-compose
This example shows how to set up a pyflink application  using docker container and docker-compose


1. Install Docker by downloading Docker.dmg https://docs.docker.com/get-docker/
2. Get the flink's docker image by running `docker pull flink:1.15.2`
    * It is important to specify the image ID version. In some cases, you dont want the image to be updated to newer version when `docker pull` is applied again , but prefer to use a fixed version of an image
3. To see which images are present locally, run `docker images`
4. Create a directory for this application and start adding files, `mkdir pyflink-app && cd pyflink-app`:
5. download Apache Flink from PyPI (look for the .tar.gz file) and place in this directory
6. download Apache Flink Libraries from PyPI (look for the .tar.gz file) and place in this directory.
7. Create a `Dockerfile` and paste the snippet below. Note this is purely a copy from [flink dock](https://nightlies.apache.org/flink/flink-docs-release-1.15/docs/deployment/resource-providers/standalone/docker/#using-flink-python-on-docker) except for the last line that set the work directory
8. build the image with a tag:  `docker build  --tag pyflink:1.15.2 .`
9. Add a python job: for this demo, I have used one of the datastream examples `state_access.py` provided by flink [here](https://github.com/apache/flink/tree/release-1.15/flink-python/pyflink/examples/datastream) and tweaked it a bit to increase the number of inputs for illustration purposes.
9. configure application services by creating `docker-compose.yml` file and pasting the following snippet
    1. Compose is a tool for defining and running multi-container Docker applications. With Compose, you can use a YAML file to configure your application’s services. Then, with a single command, you create and start all the services from your configuration.
    2. docker-compose file configure two containers: job-manager and task-manager, note the command used to run the job manager is `standalone-job` mode, which means flink cluster and job deploys at the same time.
10. To run the service: `docker compose up -d`  (-d flag is for detached mode to run your services in the background)
11. To inspect the running containers: `docker compose ps (or docker ps)`: 
12. browse Apache Flink Dashboard in localhost:8085
