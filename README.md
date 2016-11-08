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
PSQL_PASS=INSERT_DB_PASS_HERE```
