# Docker Laravel and Postgres Quick Start Kit

🚀 Add to your Laravel project and Profit

## How To Setup

1. Append the .env.example to your .env file in your Laravel Project
2. Copy all other files and the docker-files folder contents to the root of your Laravel project
3. Run `./dock build:dev` to create the containers (This may take awhile ☕️)
4. Run `./dock start:dev` to start the containers (Also try `./dock watch:dev` to see logs)
5. Go to `http://localhost`
6. Build your empire

## Other interesting commands

`./dock ssh php`

`./dock artisan route:list`

`./dock composer require wisecompany/anvil-project`

`./dock npm install`

## Batteries included

- PHP 7.4 (w/ XDebug support soon)
- Composer
- NPM
- Headless Chrome Browser (For running Laravel Dusk tests)
- Nginx
- PostgreSql
- Mailhog to view emails sent
- Adminer to manage your database

## Dock shell script list of commands

Usage: `dock <command>`

build .................. Build containers for production

build:dev .............. Build containers for development

rebuild ................ Build containers for production without using cache

rebuild:dev ............ Build containers for development without using cache

watch .................. Bring production up and attached

watch:dev .............. Bring development up and attached

start .................. Bring container up and detached

stop ................... Stop containers

halt ................... Force stop all containers

kill-all ............... Terminate all containers

restart ................ Restart containers

status ................. Container status

ssh .................... Start a bash shell

exec ................... Executes a command in the shell

clean .................. Prune containers, images, cache etc.

clean:images ........... Erase all images

artisan ................ Run php artisan command

composer ............... Run composer command

phpunit ................ Run phpunit command

npm .................... Run npm command
