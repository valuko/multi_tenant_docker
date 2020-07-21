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

The project is implemented to highlight using one Laravel project to run multiple apps, which have different routes and domain but share some common parts of the source codes.

For simplicity, I implemented the project to use common Eloquent Models, common Repositories and common auth DB.
The differences come in the Controllers, the routes and the database configurations.
Rather than loading the DB configurations for each app from the main_db, I opted to have them configured in the app so that Laravel can open connections easily to the DBs as needed.
In more complex use cases, you may want to keep the DB configurations in the `main_db` and load them when the user is authenticated. I can also implement that.

The `main_db` is used to authenticate users and determine the app the user is using.
Although the apps currently use different login URLs, as requested, I added the app in the `users` table so that we can move to a single login URL for all apps.
I also played around with different concepts in this.
For instance, I ensured app2 and app3 have the same `members` table, so that they can use the same Eloquent model but change DB connection as necessary.
I also moved the `CompanyController` into a separate namespace to show how we would separate the controllers unique to each app while keeping the `MemberController` in the common namespace.

The main authenticatin and access check is performed in the middlewares, which perform the following functions:
- Check the session of the user in the current app
- Set the app for the request lifetime 
- Set the DB for the request lifetime 

I tried to use a Scope for setting the DB connection to use but I ran into some errors doing that. 
I intend to fix this errors later.
 
