## Starter Symfony 4.4.* with Docker

Clone repo
````shell
git clone https://github.com/thewasta/symfony4-4.git
````

Copy `.env.local` into `.env`

```shell
cp .env.local .env
```

You **must** to edit APP_SECRET, source: [Symfony Secret](https://symfony.com/doc/current/reference/configuration/framework.html#secret)
. You can use [APP_SECRET Generator](http://nux.net/secret), but you can just type a random string with length 32.

Edit arguments for php service in `docker-compose.yml`

```text
args:
GIT_MAIL: "mail@mail.com"
GIT_NAME: "Name Random"
```

Start project using docker-compose

````shell
docker-compose up
````