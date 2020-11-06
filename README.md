# README

1 スケルトンアプリ作成
#mysqlの場合
docker-compose run web rails new . --force --no-deps --database=mysql --skip-test --webpacker
#postgresql
docker-compose run web rails new . --force --no-deps --database=postgresql --skip-test --webpacker
#sqlite3
docker-compose run web rails new . --force --no-deps --skip-test --webpacker

2 イメージのビルド
docker-compose build

3 database.yml の設定と DB 接続
/***** mysqlの場合 *****/
default: &default
  adapter: mysql2
  encoding: utf8mb4
  pool: <%= ENV.fetch("RAILS_MAX_THREADS") { 5 } %>
  username: <%= ENV.fetch("MYSQL_USERNAME", "root") %>
  password: <%= ENV.fetch("MYSQL_PASSWORD", "password") %>
  host: <%= ENV.fetch("MYSQL_HOST", "db") %>

development:
  <<: *default
  database: myapp_development

test:
  <<: *default
  database: myapp_test

production:
  <<: *default
  database: myapp_production
  username: myapp
  password: <%= ENV['MYAPP_DATABASE_PASSWORD'] %>
/***** mysqlの場合 *****/

/***** postgresqlの場合 *****/
default: &default
  adapter: postgresql
  encoding: unicode
  host: db
  username: postgres
  password: password
  pool: 5

development:
  <<: *default
  database: myapp_development

test:
  <<: *default
  database: myapp_test
/***** postgresqlの場合 *****/


4 データベース作成
docker-compose run web rake db:create

5 コンテナ起動
docker-compose up