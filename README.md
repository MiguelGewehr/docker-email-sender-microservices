# Docker Email Sender Microservices

A complete email sender application built with microservices architecture using Docker Compose. This project demonstrates the orchestration of multiple services including a web frontend, Python API, PostgreSQL database, Redis queue, and background worker.

## Architecture

This application consists of 5 main services:

- **Frontend (Nginx)**: Serves the HTML interface and acts as reverse proxy
- **App (Python)**: Flask API that receives email requests and queues them
- **Database (PostgreSQL)**: Stores email records
- **Queue (Redis)**: Message queue for background processing
- **Worker (Python)**: Background service that processes queued emails

## Services Overview

### Frontend Service
- **Image**: nginx:1.13
- **Port**: 80
- **Function**: Serves web interface and proxies API calls

### App Service
- **Image**: python:3.6
- **Dependencies**: bottle, psycopg2, redis
- **Function**: REST API that handles email submission

### Database Service
- **Image**: postgres:9.6
- **Function**: Persistent storage for email records
- **Volume**: Named volume for data persistence

### Queue Service
- **Image**: redis:3.2
- **Function**: Message broker for asynchronous processing

### Worker Service
- **Custom Build**: Built from Dockerfile
- **Function**: Background email processing simulation

## Getting Started

### Prerequisites
- Docker
- Docker Compose

### Installation

1. Clone the repository:
```bash
git clone https://github.com/yourusername/docker-email-sender-microservices.git
cd docker-email-sender-microservices
```

2. Start all services:
```bash
docker-compose up -d
```

3. Access the application at `http://localhost`

### Project Structure

```
.
├── docker-compose.yml          # Main orchestration file
├── app/
│   ├── sender.py              # Flask API application
│   └── app.sh                 # Application startup script
├── worker/
│   ├── worker.py              # Background worker
│   ├── app.sh                 # Worker startup script
│   └── Dockerfile             # Worker container build
├── web/
│   └── index.html             # Frontend interface
├── nginx/
│   └── default.conf           # Nginx configuration
└── scripts/
    ├── init.sql               # Database initialization
    └── check.sql              # Database verification
```

## Usage

1. Open your browser and navigate to `http://localhost`
2. Fill in the email form with subject and message
3. Submit the form
4. The message will be queued and processed by the background worker
5. Check the worker logs to see email processing simulation

## Docker Compose Features Demonstrated

- **Multi-service orchestration**
- **Service dependencies** (depends_on)
- **Named volumes** for data persistence
- **Custom networks** for service isolation
- **Environment variables** configuration
- **Port mapping** and service exposure
- **Volume mounts** for code and configuration
- **Custom Dockerfile** integration

## Monitoring

To view service logs:
```bash
# All services
docker-compose logs -f

# Specific service
docker-compose logs -f worker
```

To check service status:
```bash
docker-compose ps
```

## Stopping the Application

```bash
docker-compose down
```

To remove volumes as well:
```bash
docker-compose down -v
```

## Technologies Used

- Docker & Docker Compose
- Python (Flask/Bottle framework)
- PostgreSQL database
- Redis message queue
- Nginx web server
- HTML/CSS frontend
