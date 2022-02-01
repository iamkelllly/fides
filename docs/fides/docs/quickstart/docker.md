# Running Fidesctl with Docker Compose

---

The recommended method for running Fidesctl is via a Docker Compose environment. 

## System Requirements

Docker and Docker-Compose are all that is needed to get started.

1. Install `docker` locally (see [Docker Desktop](https://www.docker.com/products/docker-desktop) or your preferred installation), or verify an existing `docker` version by running `docker -v`. The minimum verified Docker version is `20.10.8`.
1. Confirm your `docker-compose` installation and version by running `docker-compose -v`. If your `docker` installation did not include `docker-compose`, or if your version is below `1.29.0`, follow the `docker-compose` installation instructions in the [Docker Documentation](https://docs.docker.com/compose/install/).

## Docker Setup

Copy and paste the following reference into a local `docker-compose.yml` file created at the root of your project directory. It will create a database and spin up the fidesctl webserver. Make sure that you don't have anything else running on port `5432` or `8080` before using this file.

```docker-compose title="docker-compose.yml"
services:
  fidesctl:
    image: ethyca/fidesctl:1.0.0
    command: fidesctl webserver
    healthcheck:
      test: ["CMD", "curl", "-f", "http://0.0.0.0:8000/health"]
      interval: 5s
      timeout: 5s
      retries: 5
    depends_on:
      fidesctl-db:
        condition: service_healthy
    expose:
      - 8080
    ports:
      - "8080:8080"
    environment:
      - FIDESCTL__CLI__SERVER_URL=http://fidesctl:8080
      - FIDESCTL__API__DATABASE_URL=postgresql+psycopg2://postgres:fidesctl@fidesctl-db:5432/fidesctl
    volumes:
      - type: bind
        source: ./fides_resources/ # Update this to be the path of your fides_resource folder
        target: /fides/fides_resources/
        read_only: False

  fidesctl-db:
    image: postgres:12
    healthcheck:
      test: ["CMD-SHELL", "pg_isready -U postgres"]
      interval: 5s
      timeout: 5s
      retries: 5
    volumes:
      - postgres-fidesctl:/var/lib/postgresql/data
    expose:
      - 5432
    ports:
      - "5432:5432"
    environment:
      - POSTGRES_USER=postgres
      - POSTGRES_PASSWORD=fidesctl
      - POSTGRES_DB=fidesctl

volumes:
  postgres-fidesctl:

```

Now you can start interacting with your installation. Run the following commands to launch and verify your setup:

1. `docker-compose up -d` -> This will spin up the docker-compose file in the background
1. `docker-compose run --rm fidesctl /bin/bash` -> Opens a shell within the fidesctl container
1. `fidesctl ping` -> This confirms that your `fidesctl` CLI can reach the server and everything is ready to go!

    ```bash
    root@796cfde906f1:/fides/fidesctl# fidesctl ping
    Pinging http://fidesctl:8080/health...
    {
        "data": {
            "message": "Fidesctl API service is healthy!"
        }
    }
    ```

## Next Steps

Now that you're up and running, you can use `fidesctl` from the shell to get a list of all the possible CLI commands. You're now ready to start enforcing privacy with Fidesctl!

See the [Tutorial](../tutorial/index.md) page for a step-by-step guide on setting up a Fidesctl data privacy workflow.
