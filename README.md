# S'nce Group basic PHP/Symfony Docker setup

Basic Docker setup to enable a quick start for Symfony based projects

## TODOs

- [x] Basic setup
- [x] Expose servie
- [x] Sequel PRO shortcut
- [ ] MySQL proper volume mount
- [ ] Symfony test
- [ ] eZ Publish test
- [ ] Sulu test
 
## How to run

Dependencies:

  * [Docker for Mac](https://www.docker.com/community-edition#/download) > 17.04 must installed to use this setup

## Services exposed

| Service | Port | Notes |
| --- | --- | --- |
| NGINX | 8080 | --- |
| MySQL | 3306 | --- |
| Redis | 6379 | --- |

  * Nginx to port 8080
  * MySQL to port 3306
  * Redis to port 6379 

## Hosts within your environment

You'll need to configure your application to use any services you enabled:

| Service | Port | Notes |
| --- | --- | --- |
| php-fpm | 9000 | --- |
| MySQL | 3306 | --- |
| Redis | 6379 | --- |

## Sequel PRO connection script

`./open-db` directly opens Sequel PRO, options available using `-h`

## Symfony environment

You can set an env variable in your host machine to decide which application env will be used by the application: `set SYMFONY_ENV=dev` or for `fish` shell `set SYMFONY_ENV dev`

## Docker compose cheatsheet

  * Start containers in the background: `docker-compose up -d`
  * Start containers on the foreground: `docker-compose up`. You will see a stream of logs for every container running.
  * Stop containers: `docker-compose stop`
  * Kill containers: `docker-compose kill`
  * View container logs: `docker-compose logs`
  * Execute command inside of container: `docker-compose exec SERVICE_NAME COMMAND` where `COMMAND` is whatever you want to run. Examples:
        * Shell into the PHP container, `docker-compose exec php-fpm bash`
        * Run symfony console, `docker-compose exec php-fpm bin/console`
        * Open a mysql shell, `docker-compose exec mysql mysql -uroot -pCHOSEN_ROOT_PASSWORD`

## Recommendations

  * Run composer outside of the php container, as doing so would install all your dependencies owned by `root` within your vendor folder.
  * Run commands (ie Symfony's console) straight inside of your container. You can easily open a shell as described above and do your thing from there.

## Credits
[PHPDocker](https://phpdocker.io/generator)

## License
[MIT](/LICENSE)