#image name hfeng/ct:15.10
FROM ubuntu:15.10

RUN apt-get update && \
DEBIAN_FRONTEND=noninteractive apt-get -y install \
build-essential \
curl \
emacs \
ffmpeg \
git \
imagemagick \
libcurl4-openssl-dev \
libffi-dev \
libicu-dev \
libmagick++-dev \
libmysqlclient-dev \
libreadline-dev \
libssl-dev \
libxml2-dev \
libxslt1-dev \
libyaml-dev \
mysql-client \
openjdk-8-jre \
opensaml2-tools \
openssh-server \
p7zip-full \
phantomjs \
poppler-utils \
python-dev \
python-pip \
silversearcher-ag \
supervisor \
tmux \
unixodbc-dev \
zlib1g-dev

# powerline
RUN pip install powerline-status psutil

WORKDIR /github

RUN curl -O http://ftp.ruby-lang.org/pub/ruby/ruby-2.1.5.tar.gz && \
tar -zxvf ruby-2.1.5.tar.gz && \
cd ruby-2.1.5 && \
CFLAGS="-march=native -O3" ./configure --disable-install-doc && \
CFLAGS="-march=native -O3" make -j 9 && \
make install && \
cd .. && \
rm -r ruby-2.1.5 ruby-2.1.5.tar.gz && \
echo 'install: --no-rdoc --no-ri' > /.gemrc && \
echo 'update: --no-rdoc --no-ri' >> /.gemrc
ENV LANG C.UTF-8
ENV LC_ALL C.UTF-8
RUN gem install bundler

RUN curl -O http://www.javascriptlint.com/download/jsl-0.3.0-src.tar.gz && \
tar -zxvf jsl-0.3.0-src.tar.gz && \
cd jsl-0.3.0/src && \
make -f Makefile.ref BUILD_OPT=1 && \
cp Linux_All_OPT.OBJ/jsl /usr/local/bin && \
cd - && \
rm -r jsl-0.3.0 jsl-0.3.0-src.tar.gz
ENV TZ US/Pacific
RUN git clone https://github.com/harrifeng/fonts.git
RUN /github/fonts/install.sh

RUN git clone https://github.com/harrifeng/dotfiles.git
RUN rm -f /root/.bashrc
RUN ln -s /github/dotfiles/bash/proxy.bashrc /root/.bashrc
RUN ln -s /github/dotfiles/tmux/old/tmux.conf /root/.tmux.conf
RUN ln -s /github/dotfiles/linux /root/.tumxinator

RUN git clone https://github.com/harrifeng/dotemacsd.git
RUN ln -s /github/dotemacsd /root/.emacs.d
RUN emacs --batch -l ~/.emacs.d/config/helpfunc-setting.el -f install-my-packages

# hide the translation
ENV TAG_WITH_I18N_ORIGIN_OFF true

RUN echo "root:root" | chpasswd
EXPOSE 22 3000
RUN mkdir -p /var/run/sshd
RUN sed -i 's/PermitRootLogin without-password/PermitRootLogin yes/' /etc/ssh/sshd_config
