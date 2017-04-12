# Ruby 2.3.4 for Heroku
FROM ruby:2.3.4

# Git Variables
ENV USER_NAME 'YOUR NAME'
ENV USER_EMAIL 'YOUR EMAIL'

# Install heroku-cli
RUN wget https://cli-assets.heroku.com/branches/stable/heroku-linux-amd64.tar.gz -O heroku.tar.gz && \
	tar -xvzf heroku.tar.gz -C /usr/local/lib && \
	/usr/local/lib/heroku/install

# Install build-essential and dependencies 
RUN apt-get update -qq && apt-get install -y build-essential libpq-dev nodejs

# Configure workdir and copy Gemfile to container for run bundle.
WORKDIR /app
ADD ./Gemfile /app/Gemfile
ADD ./Gemfile.lock /app/Gemfile.lock
RUN bundle install -j4

# Configure git variables
RUN git config --global user.name ${USER_NAME}
RUN git config --global user.email ${USER_EMAIL}
