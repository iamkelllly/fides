# Installation from Docker

Docker is a platform as a service that bundles software into containers, each of which contains everything the software needs to run, software, libraries, and configuration files. [Docker Hub](https://docs.docker.com/docker-hub/) makes it easy to manage container images.

The fidesctl community releases a production-ready reference container image of fidesctl for the ease of deployment in production.

## Docker Hub Releases

The following is an overview of the fidesctl Docker Hub release process, including release cadence and what's included. 

**Release Cadences**

Every time a new version of fidesctl is released, the images are available in the [ethyca/fidesctl DockerHub](https://hub.docker.com/r/ethyca/fidesctl/tags).

There are also mid-release versions (dirty versions) that get uploaded to DockerHub on every commit to the main branch. Implementation is not finalized in mid-release versions. 

**What's Included**

These reference images contain all of the extras and dependencies for running the Python application. However they do not contain the required Postgres database. Continue to [Setting up the database](./database.md).

## Installation

Install Docker and Docker Compose, then pull the latest container image from Docker Hub.

1. Install `docker` locally (see [Docker Desktop](https://www.docker.com/products/docker-desktop) or your preferred installation). The minimum verified Docker version is `20.10.8`
2. If your `docker` installation did not include `docker-compose`, make sure to get at least version `1.29.0`. Installation instructions can be found in the [Docker Compose documentation](https://docs.docker.com/compose/install/).
3. Run `docker pull ethyca/fidesctl` to pull the latest fidesctl container image from Docker Hub.

Congratulations! Fidesctl is now installed on your machine. 
## Next Steps

You're now ready to start enforcing privacy with Fidesctl! Below are suggestions for continuing your journey.

- See  [Setting up the database](./database.md) to set up the Postgresql for fidesctl.
- See [Running Fidesctl in Docker](../quickstart/docker.md) for more information on launching fidesctl in Docker Compose. Fidesctl requires multiple components to function as it is a multi-part application.
- See the [Tutorial](../tutorial/index.md) for a hands-on guide that solves real data privacy problems by setting up a Fidesctl data privacy workflow.