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


ENV HOME /research
ENV PYENV_ROOT $HOME/.pyenv
ENV PATH $PYENV_ROOT/shims:$PYENV_ROOT/bin:$PATH
RUN apt-get install -y python-setuptools
RUN apt-get install -y python-pip python3-pip virtualenv htop
RUN pip3 install --upgrade pip

# Add conda to path
ENV PATH /root/anaconda3/bin/:$PATH
RUN /root/anaconda3/bin/conda install numpy scipy
#RUN pip3 install sklearn
RUN /root/anaconda3/bin/conda install -c anaconda scikit-learn
#RUN pip3 install http://ftp.unicamp.br/pub/ppc64el/ai_frameworks/tensorflow/tensorflow-1.10.0-cp36-cp36m-linux_ppc64le.whl

# Mount data into the docker
LABEL VERSION="1.5"
ADD . /research/resnet


WORKDIR /research/resnet
RUN pip3 install -r official/requirements.txt

# Revert to tensorflow 1.10 for now (see issue XX-XX in mlperf issues)
WORKDIR /tmp
# RUN /root/anaconda3/bin/conda create --name powerai_154_tf1.10
# RUN /root/anaconda3/bin/conda activate powerai_154_tf1.10
RUN apt-get install -y wget vim-gtk
# RUN wget http://ftp.unicamp.br/pub/ppc64el/ai_frameworks/tensorflow/tensorflow-1.10.0-cp36-cp36m-linux_ppc64le.whl
# RUN pip install tensorflow-1.10.0-cp36-cp36m-linux_ppc64le.whl

ENTRYPOINT ["/bin/bash"]
