#!make

APP_NAME=ansibledind
DOCKER_REPO=maissacrement

env ?= .env
-include $(env)
export $(shell sed 's/=.*//' $(env))

docker:
	@docker rm -f ansibledind;echo 1
	@docker run -d --name ansibledind \
	  -e email=$(email) -e password=$(password) \
	  -v "/var/run/docker.sock:/var/run/docker.sock" \
	  -v "${PWD}/main.yml:/home/main.yml" \
	$(DOCKER_REPO)/$(APP_NAME):latest

deploy: docker
	@docker exec -i ansibledind /bin/sh -c "ansible-playbook /home/main.yml"