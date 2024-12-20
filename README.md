 ![image](https://github.com/user-attachments/assets/c323ce84-8d14-4ba6-b14a-4c4f1084af34)
 # Lab Assignment Final (Lab 03)

 ---

 ## Objective Target :
### Deployment and Observability:
- Deploy the Node.js application using Docker and Docker Compose.
- Set up observability for the application with Grafana, integrating:
    - Grafana Loki for centralized logging.
    - Grafana Mimir for metrics collection.
- Create Grafana dashboards to monitor logs and application metrics.

---

## Project Breakdown
### Main Code: [index.js](/index.js)
- A Node.js application using Express.js to provide APIs:
    - Endpoint ```/```: Returns a description of the lab.
    - Endpoint ```/user```: Returns personal information.
- The application listens on port ```8000```.
### Calculation Module: [calculator.js](/calculator.js)
- Supports basic mathematical operations: ```Add```, ```Subtract```, ```Multiply```, and ```Divide```.
### Unit Tests: [calculator.test.js](/calculator.test.js)
- Uses Jest to test the functions in ```calculator.js```.
    - Ensures that functions ```Add```, ```Subtract```, ```Multiply```, and ```Divide``` return correct results.
### Observability Integration: [datasources.yml](/grafana/provisioning/datasources/datasources.yml)
- Grafana Loki for logging [config.yml](/loki/config.yml):
    - Captures application logs and provides queryable log data in Grafana.
- Grafana Mimir for metrics [config.yml](/mimir/config.yml):
    - Scrapes application metrics via Prometheus and displays them in Grafana dashboards.
### Dockerfile: [Dockerfile](/Dockerfile)
- Defines the Docker image for the application:
    - Base image: ```node:20.17.0```.
    - Installs dependencies and copies source code into the container.
    - Exposes port ```8000``` and starts the app using ```npm start```.
### Docker Compose: [docker-compose.yml](/docker-compose.yml)
- Orchestrates multiple containers:
    - Runs the Node.js application.
    - Configures Loki and Mimir for observability.
    - Sets up Grafana as the visualization tool.
### ESLint Configuration: [eslint.config.mjs](/eslint.config.mjs)
- Configures ESLint to enforce coding standards.
- Includes support for global variables from Node.js and Jest.

---

## Steps to Set Up and Run the Pipeline
### Step 1: Clone the Project

```
git clone https://github.com/arifsetiawan/node-test-sample.git
cd node-test-sample
npm install
```

### Step 2: Configure Docker and Docker Compose
1. Install Docker and Docker Compose:
```
sudo apt-get install docker.io
sudo apt-get install docker-compose
```
2. Ensure Docker is running:
```
sudo systemctl start docker
```
### Step 3: Set Up Observability with Grafana, Loki, and Mimir
1. Grafana:
- Accessible at ```http://localhost:3000```.
- Default credentials: ```admin / admin```.
- Add data sources:
    - Loki: URL ```http://loki:3100```
    - Mimir: URL ```http://mimir:9009```
2. Loki Configuration:
- Loki service will be exposed at ```http://localhost:3100```.
- Stores logs from the Node.js application.
3. Mimir Configuration:
- Mimir service will be exposed at ```http://localhost:9009```.
- Collects application metrics via Prometheus scraping.
### Step 4: Deploy the Application
1. Start the Docker Compose services:
```
docker-compose up --build
```
2. Verify that the containers are running:
```
docker ps
```
### Step 5: Access the Application
- API Endpoints:
    - ```http://localhost:8000/``` - Returns a description of the lab.
    - ```http://localhost:8000/user``` - Returns personal information.
- Observability Dashboards:
    - Grafana Dashboards: Access via ```http://localhost:3000```
        - Log Dashboard:
            - Visualize application logs from Loki.
        - Metrics Dashboard:
            - Monitor application metrics collected by Mimir.


## Expected Outcome
- The Node.js application runs successfully in a Docker container.
- Observability is set up:
    - Logs are accessible via Grafana Loki.
    - Metrics are monitored via Grafana Mimir.
- Dashboards provide real-time insights into the application’s behavior.
## This lab is a complete set up the application and integrate Grafana for observability with Docker and Docker Compose