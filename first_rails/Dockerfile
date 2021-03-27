FROM centos:centos8

ENV USER uny0102
ENV HOME /${USER}
RUN mkdir /${USER}
RUN touch /${USER}/.zshrc

RUN dnf install -y epel-release

RUN dnf -y install zsh
RUN curl https://gist.githubusercontent.com/mollifier/4979906/raw/43d1c77344dd59fa119ca5b75e7a54e01e668710/zshrc_useful.sh >> ~/.zshrc
SHELL ["/bin/zsh", "-c"]

### ======汎用ここから======

RUN dnf -y install sudo git which vim

# RUN dnf -y gcc

### ======汎用ここまで======

### ======mysql5.7ここから======

RUN dnf localinstall -y http://dev.mysql.com/get/mysql57-community-release-el7-7.noarch.rpm
# 既存のモジュールをOFFにしないとmyql入らない
RUN dnf module disable -y mysql

RUN dnf install -y mysql-community-server
# RUN systemctl start mysqld
RUN systemctl enable mysqld

RUN cat /var/log/mysqld.log

### ======mysql5.7ここまで======

### ======ImageMagickここから======

## ImageMagickで必要
Run dnf install -y 'dnf-command(config-manager)'
RUN dnf config-manager --set-enabled powertools
RUN dnf install -y ImageMagick ImageMagick-devel

### ======ImageMagickここまで======

### ======Rubyここから======

RUN git clone https://github.com/sstephenson/rbenv.git ~/.rbenv
RUN git clone https://github.com/sstephenson/ruby-build.git ~/.rbenv/plugins/ruby-build
RUN echo '# rbenv' >> ~/.zshrc
ENV PATH $HOME/.rbenv/bin:$PATH
RUN echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.zshrc
RUN echo 'eval "$(rbenv init -)"' >> ~/.zshrc
RUN eval "$(rbenv init -)"
RUN echo $PATH

RUN dnf install -y bzip2 gcc make openssl-devel readline-devel zlib-devel

# RUN dnf install -y ruby ruby-devel rpm-build
RUN dnf install -y ruby-devel rpm-build

## 2020/3/27 mimemagic gemのエラー対策に必要
RUN dnf install -y shared-mime-info

RUN  dnf install -y nodejs

RUN rbenv install 2.6.5 -v
RUN rbenv global 2.6.5
RUN rbenv rehash

RUN gem install rails -v '6.0.0'
RUN gem install bundler -v '2.1.4'

RUN bundle config --global build.mysql2 --with-opt-dir="$(brew --prefix openssl)"

### ======Rubyここまで======

CMD ["/sbin/init" ]