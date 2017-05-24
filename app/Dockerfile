FROM ruby:2.3.4

RUN apt-get update -qq && apt-get install -y build-essential libpq-dev nodejs

ENV INSTALL_PATH /app

RUN mkdir -p $INSTALL_PATH

WORKDIR $INSTALL_PATH

ENV BUNDLE_GEMFILE=$INSTALL_PATH/Gemfile \
  BUNDLE_JOBS=2 \
  BUNDLE_PATH=/box

COPY . .
