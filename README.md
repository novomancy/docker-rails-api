# README

# Instructions

To set up a new project based on this docker config:

* Create a new project directory.
* Pull the skeleton `git clone -o "docker-rails-api" https://github.com/novomancy/docker-rails-api.git project_directory`
* Create new remote for the project on github
* Add new origin: `git remote add origin https://github.com/change_me/new_project.git`
* Push the new project: `git push origin master` (You may need to pull from origin first)
* Remove the old remote `git remote rm docker-rails-api`

Add .env:

```SECRET_KEY_BASE=INSERT_KEY_HERE
RAILS_ENV=development

PSQL_NAME=INSERT_DB_HERE
PSQL_PASS=INSERT_DB_PASS_HERE
```

Set local docker paths:
- for persistance of PGSQL data: in docker-compose.yml -> db -> volumes change `../docker-persisted/baton-postgres` to a valid local path
- for the app's root directory in the image: in docker-compose.yml -> web -> volumes -> db change `/baton` to `/your_app_name`
- for the app's root directory in the image: in Dockerfile change all instances of `/baton` to `/your_app_name`

Build docker environment:

- `docker-compose build`

Run the environment:

- `docker-compose up`

...you will get an error. This is because you haven't set up the database user yet. Open a new tab and do so now:

- Open an SQL cli: `docker-compose exec db psql -U postgres`
- Create your new user: `CREATE ROLE INSERT_DB_HERE WITH PASSWORD 'XXXX' LOGIN CREATEDB;`
- Change the password of the default user: `ALTER USER postgres WITH PASSWORD 'XXXX';`
- Exit psql: `\q`

Create your database:
- `docker-compose exec web rake db:create`
- `docker-compose exec web rake db:migrate`

...now you should be able to load localhost:3000 and get a rails spash page.

Controlling your environment:

- Stopping your containers: `docker-compose stop`
- Starting your containers in the background: `docker-compose up -d`
- Rebuilding your containers after changing gemfile or dockerfile: `docker-compose build`
