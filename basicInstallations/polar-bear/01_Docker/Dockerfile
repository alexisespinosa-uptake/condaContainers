#Starting from a miniconda3 container
#FROM continuumio/miniconda3:4.8.3
#AEG: (4.8.3 is still not available)
FROM continuumio/miniconda3:4.8.2

MAINTAINER Alexis Espinosa <alexis.espinosa@pawsey.org.au>

RUN mkdir /build && \
    mkdir /apps

WORKDIR /apps
#Official installation instructions
#Last time used: Jun-09-2020
#Version in git repo: 0
#Latest commit in git repo: 213
RUN git clone https://github.com/aidenlab/Polar.git \
 && conda env create -n Polar_conda_env -f ./Polar/Polar_conda_env.yml

#Trying to load pangolin environment by default
RUN echo "source activate Polar_conda_env" >> $HOME/.bashrc
ENV PATH="/opt/conda/envs/Polar_conda_env:$PATH"

#Other recommendations for containers:
RUN rm -rf /build && \
    mkdir /home/none && \
    mkdir /home/none/.cache && \
    cp -p $HOME/.bashrc $HOME/.profile /home/none/ && \
    chmod -R go+w /home/none
ENV HOME="/home/none"

VOLUME /data
WORKDIR /data
