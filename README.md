# Test pgbouncer with django and postgres 15

## TL;DR

For scram, use `rmccaffrey/pgbouncer:latest` image.
In production with kubernetes for example, make sure to use `127.0.0.1` instead of `localhost` as the database host.

### Build django docker image

```shell
$> docker build -f docker/app/Dockerfile -t djangoapp/server:latest .
```

### Launch docker-compose + migrations

```shell
$> # with md5
$> docker-compose -f docker-compose-md5.yml up -d && DATABASE_URL=postgres://db:password@localhost:5532/db python manage.py migrate
$> # with scram
$> docker-compose -f docker-compose-scram.yml up -d && DATABASE_URL=postgres://db:password@localhost:5532/db python manage.py migrate
```

### Run migrations alone

```shell
$> DATABASE_URL=postgres://db:password@localhost:5532/db python manage.py migrate
```

### Test

Go to localhost:8001/admin and try to authenticate, it should **NOT** hang, and you should get an error message as superuser was not yet created.

### Clean

```shell
$> docker-compose down && sudo rm -rf postgres-data
```
