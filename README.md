# Flask on Docker

This repository contains a production-ready Flask web application fully containerized with Docker and orchestrated using Docker Compose. It demonstrates a clean separation between development and production environments, including a reverse proxy (Nginx), Gunicorn application server, and PostgreSQL database. The project showcases best practices for containerized Python services, environment-based configuration, and automated CI validation using GitHub Actions.

---

### Live Development Build Status

![Build Status](https://github.com/darrellopoku-kwat/flask-on-docker/actions/workflows/ci.yml/badge.svg)

---

## Demo

Below is a demonstration of:

- Running the application
- Uploading an image
- Viewing the uploaded image

<p align="center">
  <img src="demo.gif" width="700">
</p>

---

## Development Build Instructions

### What You Need
- [Docker Desktop](https://docs.docker.com/desktop/) installed and running
  (Includes Docker Engine and Docker Compose)

You can verify installation with: 
```bash
$ docker --version
$ docker compose version
```

## Development 

### 1) Clone the Repository

```bash
$ git clone https://github.com/darrellopoku-kwat/flask-on-docker.git
$ cd flask-on-docker 
```
### 2) Create Required Development Environment File

For security, environment files are not committed to the repository.

Create the following files in the project root directory:

-  `.env.dev`- used for development configuration
- `.env.prod`- used for production configuration

Each file should define the environment variables required by the application (for example: `FLASK_APP`, `FLASK_DEBUG`, `DATABASE_URL`,`SQL_HOST`, `SQL_PORT`, etc.)

These variables configure the Flask application and database connection for their respective environments.

**Ensure this file matches the variables referenced in** `docker-compose.yml` **and** `docker-compose.prod.yml`.

### 3) Build and Start the Services

```bash
docker compose up --build
```
This command  will:
- Build the Flask container
- Start the development server
- Initialize the required services

### 4) Access the Web Application

If Docker is running locally, open the application at:

**[http://localhost:1093](http://localhost:1093)**

##### Running on a Remote Server (SSH Port Forwarding Required)

If Docker is running on a remote server, you must forward the application port to your local machine to access the application from your local browser.

Open another terminal, and  run:
```bash
ssh -N your_username@your_server_address -p your_ssh_port -L 1093:127.0.0.1:1093
```

Replace: 
- `your_username` with your SSH username
- `your_server_address` with the server host name
- `your_ssh_port` with the  SSH port

After establishing the SSH connection, open:

**[http://localhost:1093](http://localhost:1093)**

**If Docker is running locally, port forwarding is not required.**

---
### Application Routes

**Home Page**: `http://localhost:1093`

**Static Hello Page**: `http://localhost:1093/static/hello.txt`

**Upload Page**: `http://localhost:1093/upload`

**View Uploaded Image**: `http://localhost:1093/media/FILE_NAME`

### Stopping the Development Services
To stop the running containers, Press:

`Ctrl +C`

in the terminal where `docker compose up` is running.

Then run:

```bash
docker compose down
```

This command will:
- Stop and remove the containers
- Remove the default Docker network 

If  you  also want to remove all associated volumes including database data:
```bash
docker compose down -v
```
### Resetting the Development Environment

To completely reset the environment (including the database) run:

```bash
docker compose down -v
docker compose up --build
```
---

For any issues reproducing the development or production environments, ensure Docker is running and that environment variables are correctly defined in `.env.dev` and `.env.prod`.

This repository demonstrates best practices for containerized Python services, structured environment configuration, and CI-validated Docker builds.
