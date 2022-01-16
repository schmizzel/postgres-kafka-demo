# Debezium Postgres Source Connector for Kafka
Demo project for a basic postgres source connector setup, using debezium docker images.
On startup, the connector takes a snapshot of the postgres database and pushes all the data to kafka.
A topic is created for each table and a message is produced for each row. 
After the database snapshot is fully inserted into kafka, the connector uses postgres' Change Data Capture (CDC) to create new messages once data is commited to the database.

## Run 
To run this project, first start all containers:
```console
docker-compose up
```
Once the cluster is running, register the postgres connector:
```console
curl -i -X POST -H "Accept:application/json" -H  "Content-Type:application/json" http://localhost:8083/connectors/ -d @register-postgres.json
```
All database rows should now get synced to the kafka queue.

GUI access to postgres is provided by pgAdmin at endpoint `localhost:6969`

GUI access to kafka is provided by AKHQ at endpoint `localhost:8080`

## Connect API calls
### Connect Version
```console
curl -H "Accept:application/json" localhost:8083/
```
### Register Postgres Connector
```console
curl -i -X POST -H "Accept:application/json" -H  "Content-Type:application/json" http://localhost:8083/connectors/ -d @register-postgres.json
```
### Show registered connectors
```console
curl -H "Accept:application/json" localhost:8083/connectors/
```