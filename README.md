# SysMetrics Monitor
SysMetrics Monitor is a real-time monitoring tool that captures and visualizes system-level metrics, including CPU, memory, disk, and network utilization. Designed for system administrators and DevOps professionals, it provides insights into infrastructure performance and health, leveraging the power of Telegraf, InfluxDB, and Grafana.

## Key Features:
- **Real-Time Monitoring**: Continuously track the health and performance of your system's CPU, memory, disk, and network.
- **Historical Data Analysis**: Leverage InfluxDB's efficient time-series data storage to analyze past performance and identify trends.
- **Customizable Dashboards**: With Grafana, create and customize dashboards to focus on the metrics that matter most to you.

## Prerequisites

Before you begin, ensure you have met the following requirements:
* You have installed the latest version of [Docker](https://docs.docker.com/get-docker/) and [Docker Compose](https://docs.docker.com/compose/install/).
* You have a `<Windows/Linux/Mac>` machine.


## Cloning the Repository

To clone the repository and run the application, follow these steps:

```bash
# Clone the repository
git clone https://github.com/nicolemah99/tig-stack.git

# Navigate to the repository directory
cd tig-stack
```
## Configuration
1. Rename the `.env.example` file to `.env`
2. Fill in the environment variables in the `.env` file with your desired InfluxDB and Grafana settings.

## Running the Application
Start SysMetrics Monitor using Docker Compose. This will run in detached mode, remove the `-d` to run in your terminal.
```bash
docker-compose up -d
```

## Accessing the Application
SysMetrics Monitor components are accessible at the following URLs:

- **InfluxDB**: http://localhost:8086 - for database management.
- **Grafana**: http://localhost:3000 - for data visualization and monitoring dashboards.

## Initial InfluxDB Setup
Once InfluxDB is running:

1. Navigate to http://localhost:8086 and complete the initial setup.
2. Create an initial user, password, organization, and bucket.
    - Use the values from the environment variables in the `.env` file.
3. Generate a Read/Write Token for Telegraf and Grafana.
    - Place the token in the `INFLUX_TOKEN` environment variable in the `.env` file.

## Connecting InfluxDB to Grafana
1. Access Grafana at http://localhost:3000.
2. Click on **Add your first data source**
3. Choose InfluxDB and add the following:
    - **Query language**: Flux
    - **URL**: `http://influxdb:8086`
    - **Organization**: `INFLUX_TOKEN` from `.env`
    - **Token**: `INFLUX_ORG` from `.env`
    - **Default Bucket**: `INFLUX_BUCKET` from `.env`
4. Click **Save & test** 
    - You should see a a green success box if the data source is properly configured.
5. Restart Telegraf to apply the changes:
```bash
docker-compose restart telegraf
```

## Create a Dashboard in Grafana
- Go back to Grafana and create a new dashboard.
- Add a panel and select the InfluxDB data source you added.
- Create a query in the panel to visualize data from InfluxDB. You should see the data reflected in the panel if everything is set up correctly.