# syntax=docker/dockerfile:1

FROM python:3.8-slim-buster

WORKDIR /app

COPY requirements.txt requirements.txt
# To make apt-get work with packages
RUN apt-get update
RUN apt-get -y install curl
RUN apt-get install -y libglfw3
RUN apt-get install -y libglfw3-dev
RUN pip3 install -r requirements.txt


# COPY . .
COPY minimal_example.py .

CMD ["python3"]

# The build command:
# docker build --tag python-docker .

# The run command:
# docker container run -it mujoco_gym /bin/bash
