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