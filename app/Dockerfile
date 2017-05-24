# Ruby 2.3.4 for Heroku
FROM ruby:2.3.4

# Git Variables
ENV USER_NAME 'YOUR NAME'
ENV USER_EMAIL 'YOUR EMAIL'

# Install heroku-cli
RUN wget https://cli-assets.heroku.com/branches/stable/heroku-linux-amd64.tar.gz -O heroku.tar.gz && \
	tar -xvzf heroku.tar.gz -C /usr/local/lib && \
	/usr/local/lib/heroku/install

RUN apt-get update -qq && apt-get install -y build-essential libpq-dev nodejs

ENV INSTALL_PATH /app

RUN mkdir -p $INSTALL_PATH

WORKDIR $INSTALL_PATH

COPY Gemfile Gemfile.lock ./

ENV BUNDLE_GEMFILE=$INSTALL_PATH/Gemfile \
  BUNDLE_JOBS=2 \
  BUNDLE_PATH=/box

COPY . .

# Configure git variables
RUN git config --global user.name ${USER_NAME}
RUN git config --global user.email ${USER_EMAIL}
