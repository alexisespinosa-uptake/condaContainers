#Starting from a miniconda3 container
#FROM continuumio/miniconda3:4.8.3
#AEG: (4.8.3 is still not available)
FROM continuumio/miniconda3:4.8.2

MAINTAINER Alexis Espinosa <alexis.espinosa@pawsey.org.au>

RUN mkdir /build && \
    mkdir /apps

WORKDIR /apps
#Official installation instructions
RUN git clone https://github.com/hCoV-2019/pangolin.git \
 && cd pangolin \
 && conda env create -f environment.yml \
 && python setup.py install

#AEG: This is a fix because snakemake is not working properly when following original instructions
#AEG: Will update several packages, including an update to the latest miniconda version
RUN conda install -c conda-forge -c bioconda snakemake-minimal -y

#Trying to load pangolin environment by default
RUN echo "source activate pangolin" >> $HOME/.bashrc
ENV PATH="/opt/conda/envs/pangolin:$PATH"

#Other recommendations for containers:
RUN rm -rf /build && \
    mkdir /home/none && \
    mkdir /home/none/.cache && \
    cp -p $HOME/.bashrc $HOME/.profile /home/none/ && \
    chmod -R go+w /home/none
ENV HOME="/home/none"

VOLUME /data
WORKDIR /data
