# name: harrifeng/ubuntu:16.04
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


WORKDIR /github

RUN git clone https://github.com/harrifeng/dotfiles.git
RUN rm -f /root/.bashrc
RUN ln -s /github/dotfiles/bash/noproxy.bashrc /root/.bashrc
RUN ln -s /github/dotfiles/tmux/tmux.conf /root/.tmux.conf
RUN ln -s /github/dotfiles/tmux/tmux.conf.local /root/.tmux.conf.local
RUN ln -s /github/dotfiles/docker /root/.docker

RUN git clone https://github.com/harrifeng/dotemacsd.git
RUN ln -s /github/dotemacsd /root/.emacs.d
RUN emacs --batch -l ~/.emacs.d/config/helpfunc-setting.el -f install-my-packages
