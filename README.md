# Lelit-Marax-Dashboard

## Create docker Stack with docker compose :

By default, the docker compose create db0 database.

Chronograf can only by accessed by the host machine.

### Influx db : 

If you want to create a DB and user manually, connect to your container.
- ~# docker container ls
- ~# docker exec -it <CONTAINER_NAME> /bin/bash

### Then you can create databases and users directly from the container.
- ~# inlfux
- \> SHOW DATABASES

## Dashboard Gafana :

In grafana add a datasource : InfluxDB

Specify your credentials here : 

![image](https://user-images.githubusercontent.com/62135577/209438914-1b1ca26f-ae94-4c36-ab8f-42a8e3cd4b77.png)

### Then you can import the dashboard : 

![image](https://user-images.githubusercontent.com/62135577/209438413-c6101bad-1012-4434-9827-6914426d5544.png)
