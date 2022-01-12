# Installation from Docker

For the ease of deployment in production, the fidesctl community releases production-ready Docker Images, which are container reference images for running fidesctl. 

Each time a new version of fidesctl is released, the updated images are available in the [ethyca/fidesctl DockerHub](https://hub.docker.com/r/ethyca/fidesctl/tags). There are also mid-release versions (dirty versions) that get uploaded to DockerHub on every commit to the main branch.

These reference images contain all of the extras and dependencies for running the Python application, but do not contain the required Postgres database, covered in this guide's [next steps](../installation/database/).

Fidesctl requires multiple components to function, as it is a multi-part application. To launch fidesctl in a Docker Compose environment, additional resources are available for [Running Fidesctl with Docker Compose](../quickstart/docker.md).
