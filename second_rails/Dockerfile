FROM ruby:3.0.0

RUN gem install rails -v '6.1.3'

RUN bundle config --global build.mysql2 --with-opt-dir="$(brew --prefix openssl)"

CMD ["/bin/bash"]