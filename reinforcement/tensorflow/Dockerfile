FROM dustinvanstee:powerai-1.5.3-py3
# PowerAI Container defaults to pwrai user.  Set root user
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
#RUN pip3 install virtualenv
#RUN pip3 install virtualenvwrapper
#RUN pip3 install --upgrade numpy scipy sklearn tf-nightly-gpu
# use PowerAI TF

RUN conda install numpy scipy
RUN conda install -c anaconda scikit-learn

# Mount data into the docker
ADD . /research/reinforcement
WORKDIR /research/reinforcement
# RUN /bin/bash env_setup.sh

RUN pip3 install --upgrade pip
RUN pip3 install --upgrade setuptools
RUN pip3 install -r minigo/requirements.txt
#RUN pip3 install "tensorflow-gpu>=1.5,<1.6"

RUN chown -R pwrai:pwrai /research/
RUN mkdir /logs && chown -R pwrai:pwrai /logs/

USER pwrai
RUN /bin/bash -c "source /home/pwrai/.profile"
RUN /bin/bash -c "source /opt/DL/tensorflow/bin/tensorflow-activate"


ENTRYPOINT ["/bin/bash"]
