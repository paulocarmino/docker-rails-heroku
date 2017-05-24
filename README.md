# Rails on Docker with Heroku

Skeleton a development environment with Rails, PostgreSQL and Heroku CLI ning on Docker.

#### 1. Configure git credential variables.
Edit ```app/Dockerfile```
```yaml
[...]
# Git Variables
ENV USER_NAME 'YOUR NAME'
ENV USER_EMAIL 'YOUR EMAIL'
[...]
```

#### 2. Create a Rails APP and build image.
```bash
docker-compose  app bundle install
docker-compose  app bundle run rails new . --force --database=postgresql --skip-bundle
docker-compose build
```

#### 3. Configure PostgreSQL in Rails APP.
Edit ```config/database.yml```
```yaml
default: &default
  adapter: postgresql
  encoding: unicode
  pool: <%= ENV.fetch("RAILS_MAX_THREADS") { 5 } %>
  username: postgres
  password:
  host: db
development:
  <<: *default
  database: app_development
test:
  <<: *default
  database: app_test
```

#### 4. Start containers and create DB

```bash
docker-compose up
docker-compose run app bundle exec rake db:create
```

#### 5. Deploying in Heroku
```bash
docker-compose run app git init
docker-compose run app git add .
docker-compose run app git commit -m 'Inital Commit'
docker-compose run app heroku create
docker-compose run app git push heroku master
```
