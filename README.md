**Overview**
------------

This repository provides a Docker-based database stack with added tools to collect and visualize system metrics using Telegraf, TimescaleDB, and Grafana. The stack is designed to be easy to set up and use, with a focus on providing a robust and scalable solution for your timeseries database needs.

**Components**
------------

The stack consists of the following components:

* **TimescaleDB**: A time-series database optimized for storing and querying large amounts of time-stamped data.
* **Telegraf**: A data collector that collects system metrics and sends them to TimescaleDB.
* **Grafana**: A visualization tool that provides a web-based interface for creating dashboards and visualizing data.
* **PgAdmin**: A database administration tool that provides a web-based interface for managing TimescaleDB.

**Setup and Configuration**
-------------------------

### Prerequisites

* Docker and Docker Compose installed on your system.

### Setup

1. Clone the repository and navigate to the root directory.
2. Create a `.env` file with the following environment variables:
	* `POSTGRES_USER`
	* `POSTGRES_PASSWORD`
	* `POSTGRES_DB`
	* `PGADMIN_DEFAULT_EMAIL`
	* `PGADMIN_DEFAULT_PASSWORD`
	* `GF_SECURITY_ADMIN_PASSWORD`
	* `GF_SERVER_ROOT_URL`
	* `GF_PLUGINS_PREINSTALL`

3. Create or modify telegraf.conf. A connection string needs to be set under outputs.postgres.
	* `connection="postgresql://user:password@host:port/dbname"`
	* If using env variables they should be set in `/etc/default/telegraf`

4. Run `docker-compose up -d` to start the stack in detached mode.

### Telegraf Configuration

Telegraf is configured to collect metrics from the system and send them to TimescaleDB. The configuration file is located at `telegraf.conf`. You can modify this file to collect additional metrics or change the output plugin.

### Grafana Configuration

Grafana is configured to provide a web-based interface for visualizing data. The component files is located at `grafana-examples/*.sql`.

### PgAdmin Configuration

PgAdmin is configured to provide a web-based interface for managing TimescaleDB. The configuration file is located at `config.env`.

**Improvements and Suggestions**
-------------------------------

* **Connection Pooling**: Consider adding PgBouncer for connection pooling to improve performance.
* **Replication**: Consider adding TimescaleDB replication for backup and disaster recovery.

**Troubleshooting**
------------------

* **Postgres Port Conflict**: If Postgres fails to start due to a port conflict, use `pg_lsclusters` and `sudo pg_ctlcluster 14 main stop` to resolve the issue.
* **Telegraf Configuration**: Use `docker run --rm telegraf telegraf --input-filter cpu:mem:disk:net  --output-filter=postgresql config > telegraf.conf` to generate a Telegraf configuration file.

**Documentation**
---------------

* **TimescaleDB Documentation**: https://deepwiki.com/timescale/timescaledb
* **Telegraf Documentation**: https://docs.tigerdata.com/integrations/latest/telegraf/
* **Grafana Documentation**: https://docs.tigerdata.com/integrations/latest/grafana/
* **PgAdmin Documentation**: https://www.pgadmin.org/

