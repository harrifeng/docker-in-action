FROM ubuntu:16.04

RUN apt-get update && \
DEBIAN_FRONTEND=noninteractive apt-get -y install \
silversearcher-ag \
tmux \
tmuxinator \
emacs \
git \
curl \
python-pip \
mysql-client \
python-dev

# The configuration file can be stored in /root, and thus no need to install here
RUN pip install powerline-status psutil rope flake8 importmagic autopep8 yapf flask

# For nodejs
RUN curl -sL https://deb.nodesource.com/setup_4.x | bash -
RUN apt-get install -y nodejs
RUN npm install -g js-beautify webpack tern
