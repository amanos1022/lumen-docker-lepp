# Lumen, Docker Development Environment
This repo is an example of how you can setup a development environment for Lumen using docker-compose.

**DO NOT USE THIS IN PRODUCTION!!**

1. Clone Lumen Git Repo into app directory
```
git clone git@github.com:laravel/lumen.git app
```

2. Create Containers:
```
docker-compose up -d
```

3. Create .env file in `app`:
```
APP_ENV=dev
APP_DEBUG=true
APP_KEY=
APP_TIMEZONE=UTC

DB_CONNECTION=pgsql
DB_HOST=psql
DB_PORT=5432
DB_DATABASE=myapi
DB_USERNAME=postgres
DB_PASSWORD=123

CACHE_DRIVER=file
QUEUE_DRIVER=sync
```

4. Run composer install:
```
docker exec -it my-api-php sh -c "cd /app && composer install"
```

5. Enable Nginx Conf (disabled initially so container creation succeeds):
Move `nginx/conf.d/my-api.conf.disabled` to `nginx/conf.d/my-api.conf`
reload nginx in container
```
docker exec -it my-api-nginx bash -c "service nginx reload"
```
6. Set entry in `/etc/hosts` file (on host):

```
#add to /etc/hosts
127.0.0.1 my-api.com
```

Visit http://my-api.com in your browser and you should see the Lumen Version number.