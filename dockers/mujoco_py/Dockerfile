# syntax=docker/dockerfile:1

FROM python:3.8-slim-buster

WORKDIR /root

# To make apt-get work with packages
RUN apt-get update
RUN apt-get -y install curl
RUN apt-get -y install libglfw3
RUN apt-get -y install libglfw3-dev
RUN apt-get -y install gcc mono-mcs
RUN apt-get -y install libosmesa6-dev
RUN apt-get -y install patchelf

# python definitions
COPY requirements.txt requirements.txt
RUN pip3 install -r requirements.txt

# mujoco-py definitions
ADD https://mujoco.org/download/mujoco210-linux-x86_64.tar.gz .
RUN ls -lath
RUN mkdir ~/.mujoco
RUN tar -xzf mujoco210-linux-x86_64.tar.gz
RUN mv mujoco210 ~/.mujoco/

# Install mujoco
COPY minimal_example.py .
ENV LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/root/.mujoco/mujoco210/bin
CMD ["python3","minimal_example.py"]

COPY .bashrc /root/.bashrc

# CMD ["source",".bashrc"]
# ENTRYPOINT ["/bin/bash", "/root/.bashrc"]
# SHELL ["/bin/bash", "-c"]


# The build command:
# docker build --tag mujoco_py .

# The run command:
# docker container run -it mujoco_py /bin/bash

# To run the python:
# python minimal_example.py
