# Rails on Docker with Nginx

Skeleton a development environment with Rails, PostgreSQL and Nginx running on Docker.

#### 1. Build image and create a Rails.
```bash
docker-compose build
docker-compose run app bundle install
docker-compose run app bundle exec rails new . --force --database=postgresql --skip-bundle
```

#### 2. Configure PostgreSQL in Rails APP.
Edit ```app/config/database.yml```
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

#### 3. Create DB and start containers

```bash
docker-compose up
docker-compose run app bundle exec rake db:create
```
