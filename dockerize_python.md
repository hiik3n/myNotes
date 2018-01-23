# Dockerize python

1. Run directly

        sudo docker run -it --rm --name python-script-name -v .:/usr/src/ python:3 python my_script.py
        sudo docker run --restart always -it --name python-script-name -v .:/usr/src/ python:3 python my_script.py

2. Run Dockerfile

        FROM python:3
        ADD . /src
        WORKDIR /src
        #RUN pip install -r requirements.txt
        CMD ["python", "-u", "app.py"]
  
  Command
  
        docker build -t dockerFileName .
        docker run --restart always dockerFileName

3. Combine 2 with docker-compose.yml

        version: '3'
        services:
          name:
            build: .
            ports:
             - "5000:5000"
            volumes:
            - .:/code

## Links:

https://docs.docker.com/compose/gettingstarted/

https://runnable.com/docker/python/dockerize-your-python-application

https://docs.docker.com/engine/admin/start-containers-automatically/#use-a-restart-policy
