

# A script to build open-mpi, NEURON-7.4, miniconda, python3, neuronunit-dev and sciunit-dev all working togethor.

Purpose: The building of development environments raises an unnecessary technical problem. In many cases even if someone has the technical capacity to build, it does not mean they will have time too. In order to remove this barrier to participation I have attempted to create a docker image. The docker image builds open-mpi, NEURON-7.4 and miniconda python3 as well as neuronunit/sciunit dev. 

# 1
Get docker 

# 2 
In accordance with the philosophy stated above don't build the docker image from source instead just download the pre-compiled image with
$docker pull russelljarvis/pyneuron-toolbox 

Run step 3 to confirm the presence of the image, and step 4 to enter the docker container.


# 2 The long way:
Assuming you have git, after running git clone navigate to the directory containing this file and run

$sudo docker build -t para-nrn-python .

This tells docker to build an image based on the contents of the file labelled Dockerfile located in the present working directory. The image that is output from this process is not actually output to this directory. The image is accessible in any directory visible to the shell in an instance of the docker daemon.

# 3
To confirm build made an image:

$docker images

# 4
To enter the built ubuntu image try interactively inorder to do neurounit development inside the image use:

$docker run -it para-nrn-python:latest /bin/bash

# 5
To throw commands at the docker image without actually entering it use syntactic pattern like:

$docker run para-nrn-python:latest python -c "import neuron; import neuronunit; import sciunit"

$docker run para-nrn-python:latest nproc


##The docker image is able to use the same number of CPUs available on the host system see below:
##http://stackoverflow.com/questions/20123823/how-does-docker-use-cpu-cores-from-its-host-operating-system

#To mount a directory containing development files inside the docker container using OSX as the base system use:
#docker run -v /Users/<path>:/<container path> ...
#Reference: https://docs.docker.com/engine/tutorials/dockervolumes/