#!make
include .env
export $(shell sed 's/=.*//' .env)

RED=\033[0;31m        #  ${RED}
GREEN=\033[0;32m      #  ${GREEN}
BOLD=\033[1;m   #  ${BOLD}
WARNING=\033[37;1;41m #  ${WARNING}
END_COLOR=\033[0m  #  ${END_COLOR}

RUN = docker-compose -f docker-compose.yml run --rm --no-deps
START = docker-compose -f docker-compose.yml up -d
STOP = docker-compose -f docker-compose.yml stop
LOGS = docker-compose -f docker-compose.yml logs --tail=100 -f
EXEC = docker-compose -f docker-compose.yml exec
STATUS = docker-compose -f docker-compose.yml ps
CLEAN = docker-compose -f docker-compose.yml down --rmi all 2> /dev/null
BUILD = docker-compose -f docker-compose.yml build --no-cache

.PHONY: up stop restart status

up:
	@echo "\n\033[1;m Spinning up containers for environment... \033[0m"
	@$(START)
	@$(MAKE) --no-print-directory status

down:
	@echo "\n\033[1;m Removing containers for environment... \033[0m"
	@docker-compose down
	@$(MAKE) --no-print-directory status

stop:
	@echo "\n\033[1;m Halting containers... \033[0m"
	@$(STOP)
	@$(MAKE) --no-print-directory status

restart:
	@echo "\n\033[1;m Restarting containers... \033[0m"
	@$(MAKE) --no-print-directory stop
	@$(START)
	@$(MAKE) --no-print-directory status

status:
	@echo "\n\033[1;m Containers statuses \033[0m"
	@$(STATUS)

console-web:
console-php:
console-mysqldb:
console-%:
	$(EXEC) $* bash

logs-web:
logs-php:
logs-mysqldb:
logs-%:
	$(LOGS) $*