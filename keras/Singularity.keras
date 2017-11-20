BootStrap: docker
From: nvidia/cuda:8.0-cudnn6-runtime-ubuntu16.04

################################################################################
%labels
################################################################################
MAINTAINER Wolfgang Resch
VERSION v3

################################################################################
%environment
################################################################################
export PATH=/bin:/usr/bin:/usr/local/bin:/usr/local/cuda/bin:

################################################################################
%post
################################################################################

###
### install keras + tensorflow + other useful packages
###
apt-get update
apt-get install -y libhdf5-dev graphviz locales python3-dev python3-pip
locale-gen en_US.UTF-8
apt-get clean

pip3 install tensorflow-gpu==1.3.0
pip3 install keras==2.0.8
pip3 install Pillow scikit-learn pandas matplotlib notebook ipython

###
### destination for NIH HPC bind mounts
###

mkdir /gpfs /spin1 /gs2 /gs3 /gs4 /gs5 /gs6 /gs7 /gs8 /data /scratch /fdb /lscratch
