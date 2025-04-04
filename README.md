# Log Analytics Platform

A comprehensive monitoring and observability platform that provides real-time insights into API performance, errors, and system health using a modern stack of Grafana, Loki, Kafka, and Prometheus.

## Quick Start Guide

### Prerequisites
- Docker Desktop installed and running
- At least 4GB of free RAM
- 2GB of free disk space

### First Time Setup
1. Clone the repository:
```bash
git clone <repository-url>
cd <repository-directory>
```

2. Start all services:
```bash
docker-compose up -d
```

3. Wait approximately 30-60 seconds for all services to initialize

4. Access the dashboards:
   - Grafana: http://localhost:3001
     - Username: admin
     - Password: admin
   - API Server: http://localhost:3000
   - Prometheus: http://localhost:9090

## Operations Guide

### Basic Commands

1. **Start the Platform**:
```bash
docker-compose up -d
```

2. **Stop the Platform**:
```bash
docker-compose down
```

3. **Restart Specific Services**:
```bash
# Restart one service
docker-compose restart workload-simulator

# Restart multiple services
docker-compose restart grafana api-server
```

4. **View Logs**:
```bash
# View all logs
docker-compose logs

# View specific service logs
docker-compose logs api-server
docker-compose logs workload-simulator

# Follow logs in real-time
docker-compose logs -f api-server
```

5. **Check Service Status**:
```bash
docker-compose ps
```


## Features

- Real-time API monitoring and metrics collection
- Log aggregation and analysis with Loki
- Request/Response tracking with detailed metrics
- Error detection and visualization
- Continuous workload simulation for testing
- Automated dashboard provisioning
- Containerized deployment with Docker

## Prerequisites

- Docker
- Docker Compose

## Components

- **API Server**: Node.js REST API with built-in monitoring
- **Workload Simulator**: Automated request generator for testing
- **Kafka**: Message broker for log streaming
- **Log Consumer**: Service that processes logs from Kafka to Loki
- **Loki**: Log aggregation system
- **Prometheus**: Metrics collection and storage
- **Grafana**: Visualization and dashboards

## Getting Started

1. Clone the repository:
```bash
git clone <repository-url>
cd <repository-directory>
```

2. Start all services:
```bash
docker-compose up -d
```

3. Access the services:
- API Server: http://localhost:3000
- Grafana: http://localhost:3001 (username: admin, password: admin)
- Prometheus: http://localhost:9090
- Loki: http://localhost:3100

## API Endpoints

### Tasks
- `GET /api/tasks`: List all tasks
- `POST /api/tasks`: Create a new task
- `GET /api/tasks/:id`: Get a specific task
- `PUT /api/tasks/:id`: Update a task
- `DELETE /api/tasks/:id`: Delete a task

### Users
- `GET /api/users`: List all users
- `POST /api/users`: Create a new user
- `GET /api/users/:id`: Get a specific user
- `PUT /api/users/:id`: Update a user
- `DELETE /api/users/:id`: Delete a user

### System
- `GET /health`: Health check endpoint
- `GET /metrics`: Prometheus metrics endpoint

## Grafana Dashboards

The platform includes a pre-configured dashboard with four panels:

1. **Request Count per Endpoint**
   - Shows request rate per API endpoint
   - Grouped by HTTP method
   - 5-minute rate windows

2. **Response Time Trends**
   - Average response time per endpoint
   - Historical trends
   - Grouped by HTTP method and route

3. **Most Frequent Errors**
   - Error count by endpoint
   - 1-minute aggregation windows
   - Stacked visualization by error type

4. **Real-Time Logs**
   - Live log stream
   - Formatted as "METHOD PATH - STATUS (DURATION ms)"
   - Direct integration with Loki

## Workload Simulation

The platform includes a workload simulator that:
- Generates continuous API traffic
- Simulates various HTTP methods (GET, POST, PUT, DELETE)
- Creates different types of errors (400, 401, 403, 404, 500)
- Runs indefinitely with auto-restart capability
- Configurable request interval (default: 1 second)

## Monitoring Setup

### Prometheus
- Scrapes metrics every 15 seconds
- Retains data based on storage configuration
- Accessible via PromQL at http://localhost:9090

### Loki
- Receives logs via the log-consumer service
- Labels: app="api-server", level="info/error"
- Query logs using LogQL in Grafana

### Grafana
- Auto-provisioned datasources (Prometheus, Loki)
- Pre-configured dashboard
- 5-second refresh rate
- 15-minute time window by default

## Screenshots 
![image](https://github.com/user-attachments/assets/cd7e4ef9-cf9d-4f36-a91e-e59aa362a2d8)


## Troubleshooting

1. View service logs:
```bash
docker-compose logs -f [service-name]
```

2. Check service status:
```bash
docker-compose ps
```

3. Restart specific services:
```bash
docker-compose restart [service-name]
```

4. Common issues:
   - If graphs are empty, ensure workload-simulator is running
   - For missing logs, check log-consumer and Loki connection
   - If metrics are missing, verify Prometheus targets

## Development

### Adding New Endpoints
1. Add route to API server
2. Update workload simulator endpoints array
3. Restart affected services

### Modifying Dashboards
1. Make changes in Grafana UI
2. Export dashboard JSON
3. Update `grafana/provisioning/dashboards/api-monitoring.json`
4. Restart Grafana

### Updating Metrics
1. Add new metrics in API server
2. Update Prometheus configuration if needed
3. Modify Grafana dashboard to visualize new metrics

## Contributing

1. Fork the repository
2. Create a feature branch
3. Commit your changes
4. Push to the branch
5. Create a Pull Request 
