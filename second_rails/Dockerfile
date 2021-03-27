FROM ruby:3.0.0

## updateしないとinstallできない
## imagemagickは最初から入ってる
RUN apt update
RUN apt-get install -y nodejs
RUN apt-get install -y yarn

RUN gem install rails -v '6.1.3'

RUN bundle config --global build.mysql2 --with-opt-dir="$(brew --prefix openssl)"

RUN rails new test-app -d mysql
RUN rm -rf test-app

CMD ["/bin/bash"]