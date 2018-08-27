{% if cookiecutter.use_nvidia_docker == 'yes' -%}
FROM nvidia/cuda:9.1-cudnn7-runtime-ubuntu16.04
{% else %}
FROM ubuntu:16.04
{%- endif %}

# Install some basic utilities
RUN apt-get update && apt-get install -y \
    curl \
    ca-certificates \
    sudo \
    git \
    bzip2 \
    wget \
    python3-pip \
 && rm -rf /var/lib/apt/lists/*

RUN pip3 install --upgrade pip

COPY ./requirements.txt /requirements.txt
RUN pip install -r /requirements.txt

# Create a non-root user and switch to it
ARG UID
RUN adduser --disabled-password  -u $UID --gecos '' --shell /bin/bash docker
RUN echo "docker ALL=(ALL) NOPASSWD:ALL" > /etc/sudoers.d/90-user
USER docker

WORKDIR /work

ENTRYPOINT ["/bin/bash"]
