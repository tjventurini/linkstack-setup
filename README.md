# Linkstack Setup

This is my Linkstack 🔗 Setup based on Docker 🐳

## Setup

```
git clone git@github.com/tjventurini/linkstack-setup.git
make init
```

## Commands

```Makefile
init:
	@cp .env.example .env
	@echo "Is this a production environment? [y/N]" && read ans && if [ "$$ans" = "y" ]; then ln -s docker-compose.prod.yml docker-compose.yml; else ln -s docker-compose.local.yml docker-compose.yml; fi

up:
	@docker compose up -d
start: up

down:
	@docker compose down --remove-orphans
stop: down

restart: down up

logs:
	@docker compose logs
tail:
	@docker compose logs -f

ps:
	@docker compose ps

clear:
	@docker compose down --remove-orphans --volumes
	@rm docker-compose.yml
	@rm .env

login:
	@docker compose exec linkstack bash
```

## HTTPS

In order to force linkstack to use HTTPS, you need to set the `FORCE_HTTPS` environment variable to `true` in the `.env` file IN THE PERSISTANT STORAGE of your container.

```
sudo vim /var/lib/docker/volumes/<project_name>_linkstack/_data/.env

# change the following line from false to true
FORCE_HTTPS=true
```