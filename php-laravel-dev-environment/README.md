# PHP Laravel dev environment

### Usage

Run image with interactive mode and expose Code server on :8080

```docker
docker run -it -v ${PWD}:/var/www/html -p 8080:8080 --name php-laravel-container php-laravel-dev
```