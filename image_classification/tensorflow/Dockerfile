FROM dustinvanstee:powerai-1.5.3-py3
#FROM nvidia/cuda:9.0-cudnn7-runtime-ubuntu16.04
#
USER root
WORKDIR /research

RUN apt-get update

RUN apt-get update && apt-get install -y --no-install-recommends \
    ca-certificates \
    build-essential \
    git \
    python \
    python-pip

# Use PowerAI Anaconda python
ENV PATH /root/anaconda3/bin/:$PATH


ENV HOME /research
ENV PYENV_ROOT $HOME/.pyenv
ENV PATH $PYENV_ROOT/shims:$PYENV_ROOT/bin:$PATH
RUN apt-get install -y python-setuptools
RUN apt-get install -y python-pip python3-pip virtualenv htop
RUN pip3 install --upgrade pip

# use PowerAI TF

RUN conda install numpy scipy
RUN conda install -c anaconda scikit-learn

RUN pip3 install --upgrade pip
RUN pip3 install --upgrade setuptools


# Mount data into the docker
LABEL VERSION="1.5"
ADD . /research/resnet
WORKDIR /research/resnet
RUN pip3 install -r official/requirements.txt

RUN chown -R pwrai:pwrai /research
RUN chown -R pwrai:pwrai /research/resnet

RUN mkdir /logs && chown -R pwrai:pwrai /logs/

USER pwrai
ENV PATH /home/pwrai/anaconda3/bin/:$PATH
RUN /bin/bash -c "source /home/pwrai/.profile"


CMD ["/bin/bash"]
