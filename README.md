# Excalidraw Self-Hosted Stack

This repository provides a self-hosted stack for running Excalidraw with Docker containers.

## Prerequisites

Before you begin, ensure you have met the following requirements:

- Docker installed on your system ([Install Docker](https://docs.docker.com/get-docker/))
- Docker Compose installed on your system ([Install Docker Compose](https://docs.docker.com/compose/install/))
- Available domain en subdomains
- SSL Certificates
- Webproxy (NginxProxyManager for example )
  - Main Application: `https://exalidraw.my-own-domain.com -> DOCKER_HOST:3001`
  - Excalidraw Room: `https://exalidraw-ws.my-own-domain.com -> DOCKER_HOST:3002`
  - Excalidraw Room: `https://exalidraw-api.my-own-domain.com -> DOCKER_HOST:3003`

## Usage

### Building the Docker Image

1. Clone this repository to your local machine:

    ```bash
    git clone https://github.com/Nenodema/excalidraw-self-hosted-stack.git
    ```

2. Navigate to the repository directory:

    ```bash
    cd excalidraw-self-hosted-stack
    ```

3. Create a `.env` file and define the necessary environment variables for the Docker build:

    ```dotenv
    PUB_SRV_NAME=excalidraw.my-own-domain.com
    PUB_SRV_NAME_WS=excalidraw-ws.my-own-domain.com
    REDIS_PASSWORD=StrongPasswordInHere
    ```

4. Build the Docker image:

    ```bash
    docker build -t custom_excalidraw:latest .
    ```

### Running with Docker Compose

1. Modify the `.env` file to include the necessary environment variables for Docker Compose:

    ```dotenv
    VITE_APP_BACKEND_V2_GET_URL=https://excalidraw-api.my-own-domain.com/api/v2/scenes/
    VITE_APP_BACKEND_V2_POST_URL=https://excalidraw-api.my-own-domain.com/api/v2/scenes/
    VITE_APP_WS_SERVER_URL=https://excalidraw-ws.my-own-domain.com/
    ```

2. Modify the `docker-compose.yml` file if necessary.

3. Run the following command to start the containers:

    ```bash
    docker-compose up -d
    ```

4. Access Excalidraw via a web browser:

    - Main Application: `https://exalidraw.my-own-domain.com`
    - Excalidraw Room: `https://exalidraw-ws.my-own-domain.com`
    - Excalidraw Room: `https://exalidraw-api.my-own-domain.com`

5. To stop the containers, run:

    ```bash
    docker-compose down
    ```

## Configuration

- `PUB_SRV_NAME`: Public server name for Excalidraw (used in Docker build).
- `PUB_SRV_NAME_WS`: Public WebSocket server name for Excalidraw (used in Docker build).
- `REDIS_PASSWORD`: Password for Redis authentication (used in Docker build).
- `VITE_APP_BACKEND_V2_GET_URL`: API URL for fetching scenes.
- `VITE_APP_BACKEND_V2_POST_URL`: API URL for posting scenes.
- `VITE_APP_WS_SERVER_URL`: WebSocket server URL for Excalidraw.
