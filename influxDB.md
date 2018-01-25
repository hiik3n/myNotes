# InfluxDB

Docker-Compose

 	influxdb:
		image: influxdb:latest
		container_name: influxdb
		ports:
		  - "8086:8086"
		environment:
		  - INFLUXDB_DATA_QUERY_LOG_ENABLED=false
		  - INFLUXDB_HTTP_AUTH_ENABLED=false
		  - INFLUXDB_HTTP_LOG_ENABLED=false
		  - INFLUXDB_DB="testdb"
		  - INFLUXDB_ADMIN_USER='user'
		  - INFLUXDB_ADMIN_PASSWORD='pwd'
		volumes:
		  - ./data/influxdb:/var/lib/influxdb
		restart: always

Login InfluxDb CLI:

		  influx -username user -password pwd
      
Gemeral command

      create database testdb
      use testdb
        
#References:

Official Docs:

		  https://docs.influxdata.com/influxdb/v1.4/introduction/getting_started/

Docker Hub:
		
		  https://hub.docker.com/_/influxdb/
