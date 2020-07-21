# Multi-Tenant LaravelApp

This is a sample app to run the multi-tenant Laravel app project.

This source code for the multi-tenant app is hosted in a separate repo while this is the Docker-compose project to run the app

## Containers Present

- PHP 7.3 running on Apache
- MySQL 8.0 (can be downgraded to 5.7 if needed)
- PHPMyAdmin (Only for administering the DB)
- Redis (For session data storage)

## Running the App

- Run `docker-compose build`
- Run `docker-compose up -d`
- Use `docker-compose ps` to ensure all 4 containers are running  
- Pull the Laravel project source code into `www/atom_app` dir
- Run `mv www/sample_laravel.env www/atom_app/.env`
- Restart the `web` container and Browse the app

## App URLs

- App1: http://localhost:8001/public/app1/login
- App2: http://localhost:8001/public/app2/login
- App3: http://localhost:8001/public/app3/login

## Ports used by the Containers

- **8001** - Apache
- **8002** - PhpMyAdmin
- **3307** - MySQL
- **6389** - Redis

## Some useful tips


Docker example with Apache, MySql 8.0, PhpMyAdmin and Php

- You can use MariaDB 10.1 if you checkout to the tag `mariadb-10.1` - contribution made by [luca-vercelli](https://github.com/luca-vercelli)
- You can use MySql 5.7 if you checkout to the tag `mysql5.7`

I use docker-compose as an orchestrator. To run these containers:

```
docker-compose up -d
```

Open phpmyadmin at [http://localhost:8000](http://localhost:8000)
Open web browser to look at a simple php example at [http://localhost:8001](http://localhost:8001)

Run mysql client:

- `docker-compose exec db mysql -u root -p` 

Enjoy !
