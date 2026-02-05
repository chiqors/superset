# Apache Superset
This repo showcases a minimal setup with pre-configured database connections for `BigQuery`, `DuckDB`, and `PostgreSQL`.

It also presents a minimal setup to read `Parquet`, `JSON`, and `CSV` files with Apache Superset. Using an _in-memory_ DuckDB database, a live data connection is made between Superset and a filesystem.

## Build the image
```Shell
docker build -t chiqors/superset docker
```

## Run with Docker Compose (Postgres metadata)
```Shell
docker compose up -d
```
> Note: the local `./data` folder is mounted to make the data files accessible from within the container. Update `SUPERSET_SECRET_KEY` in `docker-compose.yml` with a strong key for production.

## Setup Superset
```Shell
./docker/setup.sh
```
This includes creating an admin user and configuring a DuckDB database connection.

## Navigate to UI
Go to http://localhost:8080/login/ and login with `username=admin` and `password=admin`.

## Check database connection
Go to _Database Connections_ (http://localhost:8080/databaseview/list/) to validate the database connection has been created:

![Overview of database connections in Superset UI](docs/img/database-connection-overview.png)

Click the _Edit_ button to see the connection details:

<img src='docs/img/duckdb-database-connection.png' alt='DuckDB database connection configuration in Superset UI' width='300'/>

SQLAlchemy URI:
```
duckdb:///:memory:
```

Click `TEST CONNECTION` and make sure you see this popup message:

![Popup message indicating a good connection](docs/img/connection-looks-good.png)
# Querying files from Superset using DuckDB
Go to _SQL Lab_ (http://localhost:8080/sqllab/) to query `Parquet`, `JSON`, or `CSV`, files as follows:

![Apache Superset DuckDB SQL Lab](docs/img/sql-lab-duckdb-parquet.png)

The queries use a glob syntax to read multiple files as documented on https://duckdb.org/docs/data/multiple_files/overview.html.

## Parquet
```sql
SELECT *
FROM '/data/parquet_table/*.parquet'
```

## JSON
```sql
SELECT *
FROM '/data/json_table/*.json'
```

## CSV
```sql
SELECT *
FROM '/data/csv_table/*.csv'
```
