# Setting up Ruby on Rails with PostgreSQL

+ Installing Postgres

    $ sudo apt-get update
    $ sudo apt install postgresql postgresql-contrib libpq-dev

+ Creating a user

    $ sudo -i -u postgres
    $ psql
    $ CREATE ROLE root LOGIN SUPERUSER PASSWORD 'root';
    $ exit

+ Creating our Rails app

    $ rails new postegresql_rails7 -d postgresql
    $ cd app
    $ bundle

+ Store the secrets

    $ EDITOR=nano rails credentials:edit

    Add database username and password:

    database:
        username: root
        password: root

+ Database configuration

```Yaml
    default: &default
    adapter: postgresql
    encoding: unicode
    pool: <%= ENV.fetch("RAILS_MAX_THREADS") { 5 } %>
    username: <%= Rails.application.credentials.database[:username] %>
    password: <%= Rails.application.credentials.database[:password] %>
    host: localhost
    development:
    <<: *default
    database: postgresql_rails7_development
    username: <%= Rails.application.credentials.database[:username] %>
    password: <%= Rails.application.credentials.database[:password] %>
    host: localhost

    test:
    <<: *default
    database: postgresql_rails7_test
    username: <%= Rails.application.credentials.database[:username] %>
    password: <%= Rails.application.credentials.database[:password] %>
    host: localhost

    production:
    <<: *default
    database: postgresql_rails7_production
    username: postgresql_rails7
    password: <%= ENV["POSTGRESQL_RAILS7_DATABASE_PASSWORD"] %>
```

+ Create and migrate the database

    $ rails db:create db:migrate

+ Run server

    $ rails s




