# Laravel simple sample (Dev)

## Ubuntu 20.04

### composer.json
````
{
    "name": "laravel/laravel",
    "type": "project",
    "description": "The Laravel Framework.",
    "keywords": ["framework", "laravel"],
    "license": "MIT",
    "require": {
        "php": "^7.3|^8.0",
        "fideloper/proxy": "^4.4",
        "fruitcake/laravel-cors": "^2.0",
        "guzzlehttp/guzzle": "^7.0.1",
        "laravel/framework": "^8.40",
        "laravel/tinker": "^2.5"
    },
    "require-dev": {
        "facade/ignition": "^2.5",
        "fakerphp/faker": "^1.9.1",
        "laravel/sail": "^1.0.1",
        "mockery/mockery": "^1.4.2",
        "nunomaduro/collision": "^5.0",
        "phpunit/phpunit": "^9.3.3"
    },
````
### How to use

##### Build image
```
docker build -t laravel:0.0 .
```
 ##### Run container to first time
```
 docker run --name laravel -p 8088:80 laravel:0.0 /bin/bash
```
 ##### Start container after run and exit
```
 docker start  laravel
```
 ##### Access the container
```
docker exec -ti laravel /bin/bash
```
 ##### Stop the container
```
docker stop laravel
```
##### Ready!
```
localhost:8088
```