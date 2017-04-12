# Rails on Docker with Heroku

Skeleton a development environment with Rails, PostgreSQL and Heroku CLI running on Docker.

#### 1. Edit `USER_NAME` and `USER_EMAIL` variables in `app/Dockerfile` with git credentials. 

#### 2. Create a Rails APP and build image.
```bash
docker-compose run app rails new . --force --database=postgresql --skip-bundle
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
docker-compose exec app rails db:create
```

#### 5. Deploying in Heroku
```bash
docker-compose exec app git init
docker-compose exec app git add .
docker-compose exec app git commit -m 'Inital Commit'
docker-compose exec app heroku create
docker-compose exec app git push heroku master
```
