# localdev

Quick and easy way to setup a local development environment with a reverse proxy, and database viewer.

## Prerequisites

- [Docker](https://www.docker.com/)   

## Installation

1. Clone this project locally.
2. Make sure the docker daemon is running.
3. Run `docker network create localdev`.
4. Add the following to your `/etc/hosts` file:

    ```bash
    127.0.0.1    localdev
    ```

5. From the project root, run `docker compose up -d`.

---

## Usage

### Database Viewer

> To use either of the database tools, simply comment out the other in the `docker-compose.yml` prior to starting the containers

- [Adminer](https://www.adminer.org/) (default)
- [DBeaver](https://dbeaver.io/)

## Exposing a project to the Reverse Proxy

1. Set the `VIRTUAL_HOST` environment variable in the project's `docker-compose.yml` file to the desired domain name. (e.g. `VIRTUAL_HOST=example.docker`)
2. Same value in your `/etc/hosts` file (e.g. `127.0.0.1    example.docker`)
3. Add the project to the `nginx-proxy` network by adding the following to the project's `docker-compose.yml` file:

    ```yml
    networks:
      <project-name>:
        external:
          name: localdev
    ```