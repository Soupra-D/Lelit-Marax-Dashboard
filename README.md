# Lelit-Marax-Dashboard
This project was made to visualise data from the Lelit MaraX coffee machine.

Sources for this project :

- https://www.home-barista.com/espresso-machines/lelit-marax-data-visualisation-mod-t66187-10.html

- https://github.com/alifib/lelit_dashboard

- https://github.com/jkehres/docker-compose-influxdb-grafana

## Hardware 

For this project you need at least :
- USB to TTL com RS232 (got it from Amazon, with a PL2303TA chip)
- Raspberry pi with wifi (I used a pi zero W + OTG USB type A to micro USB)

Connect the USB to TTL on your coffee Machine. Pin 0 (closer th the edge/outside) is not connected, then green to PIN 1 and white to PIN 2.
![image](https://user-images.githubusercontent.com/62135577/209440068-4e53648a-7fcc-4596-91ef-93a80424e6cf.png)

Connect th USB to the rpi. You can see the raw data in /dev/ttyUSB0.

You can verify everything is correct with this command 


~# tail -f /dev/ttyUSB0

![image](https://user-images.githubusercontent.com/62135577/209440164-f714c4de-7c29-4a78-86d9-3020a155485c.png)

## Python 

#### Create a virtual env and download the dependency.

- ~# python -m venv /MYPATH/MyVenv
- ~# source /MYPATH/MyVenv/bin/activate
- ~# python -m pip install -r requirements.txt
- ~# deactivate

#### Modify the first line of reporter.py and specify your virtual env.
- #!/MYPATH/MyVenv/bin/python

#### Then you can make it executable and start it in background.
- ~# chmod +x reporters.py 
- ~# nohup ./reporters.py >/dev/null 2>&1 &

## Docker

You can install docker on your raspberry pi, or use a server.

I used my nas to host thoses containers.

You can install InfluxDB and Grafana, bare metal, on your raspberry if you don't want docker. 


### Create docker Stack with docker compose :

By default, the docker compose create db0 database.

Chronograf can only by accessed by the host machine.

### Influx db : 

If you want to create a DB and user manually, connect to your container.
- ~# docker container ls
- ~# docker exec -it <CONTAINER_NAME> /bin/bash


Then you can create databases and users directly from the container.
- ~# inlfux
- \> SHOW DATABASES

### Dashboard Gafana :

In grafana add a datasource : InfluxDB

Specify your credentials here : 

![image](https://user-images.githubusercontent.com/62135577/209438914-1b1ca26f-ae94-4c36-ab8f-42a8e3cd4b77.png)

Then you can import the dashboard : 

![image](https://user-images.githubusercontent.com/62135577/209470358-e92f55a5-a07c-4a3d-8bf2-dbd4f298d822.png)

