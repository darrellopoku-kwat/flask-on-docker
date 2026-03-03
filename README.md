# Flask on Docker

This repository contains a production-ready Flask web application fully containerized with Docker and orchestrated using Docker Compose. It demonstrates a clean separation between development and production environments, including a reverse proxy (Nginx), Gunicorn application server, and PostgreSQL database. The project showcases best practices for containerized Python services, environment-based configuration, and automated CI validation using GitHub Actions.

### Live Development Build Status

![Build Status](https://github.com/darrellopoku-kwat/flask-on-docker/actions/workflows/ci.yml/badge.svg)

## Demo

Below is a demonstration of:

- Running the application
- Uploading an image
- Viewing the uploaded image

<p align="center">
  <img src="demo.gif" width="700">
</p>

## Development Build Instructions

### What You Need
- [Docker Desktop](https://docs.docker.com/desktop/) installed and running
  (Includes Docker Engine and Docker Compose)

### Development 

1) **Clone the repo and enter flash-on-docker**
```bash
$ git clone https://github.com/darrellopoku-kwat/flask-on-docker.git
$ cd flask-on-docker 
```
2) **Create dev environment file**
I keep `.env.dev` values private, youll have to make your own locally.
Create a file named `env.edv` in  flask-on-docker the project root and the
variables your app expects( ex. `FLASK_APP`, `FLASK_DEBUG`, `DATABASE_URL`, etc.)

3) Build and start the services

```bash
docker compose up --build
```
3) To use the Web App
#### Accessing the Application if running on a remote server
If Docker is running on a remote server, you must enable SSH port forwarding to access
the application from your local browser.

In another terminal, run:
```bash
ssh -N your_username@your_server_address -p your_ssh_port -L 1093:127.0.0.1:1093
```

Replace: 
- `your_username` with your SSH username
- `your_server_address` with the server host name
- `your_ssh_port` with the  SSH port

**If Docker is running locally, port forwarding is not required.**

**Then Open**: `http://localhost:1093`
**Uploading images files can be accessed at**: `http://localhost:1093/upload`
**Viewing uploaded images can be accessed at**: `http://localhost:1093/media/FILE_NAME`
**Viewing the Updated hello message can be accessed at**: `http://localhost:1093/static/hello.txt`

