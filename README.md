# Get up and running with Laravel in Docker

## Includes Postgres and other tools.

Laravel and Docker simplified

### How To Setup

1. Append the .env.docker.example to your .env file in your Laravel Project
2. Copy all other files and the docker-files folder contents to the root of your Laravel project
3. Change to your laravel project
4. Run `./dock build:dev` to create the containers (This may take awhile ☕️)
5. Run `./dock watch:dev` to start the containers (Also try `./dock start:dev` to start it in the background)
6. Go to `http://localhost`
7. Build your empire

### Other interesting commands

### Batteries included

- PHP 7.4 (w/ XDebug support soon)
- Composer (Dependency Manager for PHP)
- NPM (Node package manager)
- Headless Chrome Browser (For running Laravel Dusk tests)
- Nginx (Web server)
- PostgreSql (Database Server)
- Mailhog (Emulate and read emails sent)
- Adminer (Web interface to manage your database)

### Dock shell script list of commands

Usage: `dock <command> <option>`

Examples:
`./dock build`

`./dock build php`

`./dock ssh php`

`./dock artisan route:list`

`./dock composer require wisecompany/anvil-project`

`./dock npm install`

| Command      | Description                                                                                 |
| ------------ | ------------------------------------------------------------------------------------------- |
| build        | Build containers for production e.g. `./dock build`                                         |
| build:dev    | Build containers for development e.g. `./dock build:dev`                                    |
| rebuild      | Build containers for production without using cache e.g. `./dock rebuild`                   |
| rebuild:dev  | Build containers for development without using cache e.g. `./dock rebuild:dev php`          |
| watch        | Bring production up and attached e.g. `./dock watch`                                        |
| watch:dev    | Bring development up and attached e.g. `./dock watch:dev`                                   |
| start        | Bring container for production up and detached e.g. `./dock start`                          |
| start:dev    | Bring container for development up and detached e.g. `./dock start:dev`                     |
| stop         | Stop containers e.g `./dock stop <container>`, `./dock stop web`                            |
| halt         | Force stop all containers e.g. `./dock halt`                                                |
| kill-all     | Terminate all containers e.g. `./dock kill-all`                                             |
| restart      | Restart containers for production e.g. `./dock restart`                                     |
| restart:dev  | Restart containers for development e.g. `./dock restart:dev`                                |
| status       | Container status e.g. `./dock status`                                                       |
| ssh          | Start a bash shell e.g. `./dock ssh <container>`, `./dock ssh web`                          |
| exec         | Executes a command in the php container e.g. `./dock exec <command> `, `./dock exec ls -l ` |
| clean        | Prune containers, images, cache etc. e.g. `./dock clean`                                    |
| clean:images | Erase all images e.g. `./dock clean:images`                                                 |
| artisan      | Run php artisan command e.g. `./dock artisan migrate:fresh --seed`                          |
| composer     | Run composer command e.g. `./dock composer dump-autoload`                                   |
| phpunit      | Run phpunit command e.g. `./dock phpunit -v --stop-on-failure --filter=ExampleTest`         |
| npm          | Run npm command e.g. `./dock npm install`                                                   |
