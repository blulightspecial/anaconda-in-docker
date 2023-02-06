# Why this?

Many of the classes that we teach use the conda default install 
as the basis for the class. I want to make sure that I'm not 
suggesting use of libraries that the students don't have access to.
For example the `scipy-notebook` from docker has a bunch of bells
and whistles that may not be in the default anaconda installation.

# Installing anconda inside of a docker container

Just run...

``` bash
docker run -i -t -p 8888:8888 -v /Users/kevinmartin/Documents/anaconda-in-docker:/opt/notebooks \
    --name conda continuumio/anaconda3 /bin/bash -c "\
    conda install jupyter -y --quiet && \
    mkdir -p /opt/notebooks && \
    jupyter notebook \
    --notebook-dir=/opt/notebooks --ip='*' --port=8888 \
    --no-browser --allow-root"
```
 
:point_down: this version doesn't have the wierd install that you have to do. 
the 5 second sleep just gives time for the container to come online. 
``` bash
docker run --rm -i -t -p 8888:8888 -v $(pwd)/..:/opt/notebooks \
    --name conda continuumio/anaconda3:2022.10 /bin/bash -c "\
    sleep 5 \
    && jupyter notebook --ip='*' --port=8888 \
    --notebook-dir=/opt/notebooks --no-browser --allow-root"
```

See the 
[documentation on docker hub](https://hub.docker.com/r/continuumio/anaconda3) 
for details



_I thought that this would maybe be more complicated. I initially
built a container then installed conda in it. I considered bulding
my own container and just pulling that. But, conda has a pre-built
container, so there was no need to re-invent the wheel. You can 
run jupyter from just the base conda without re-installing it as
the container instructions do in their free-standing run of the 
container_

<!--
**Spin up the machine:** Navigate to this folder on your local 
machine after cloning the repo and use the command:

```bash
docker run -d -v ${pwd}:/home/jovyan/work --name ubuntu -p 8888:8888 -it ubuntu:jammy-20230126 bash
```


**Terminal into the running container:** Open up a terminal 
connection into the running docker container using the following
command:

```bash
docker exec -it ubuntu bash
```

**Update the package manager iand install wget**

```bash
apt update
apt upgrade
apt install wget
```

**Download anaconda to the container** go the the home folder in
the container (`cd home`) then download anaconda with:

```bash
wget https://repo.anaconda.com/archive/Anaconda3-2022.10-Linux-x86_64.sh
```

**Run the Anaconda installation script**

```bash
bash Anaconda3-2022.10-Linux-x86_64.sh
```
-->