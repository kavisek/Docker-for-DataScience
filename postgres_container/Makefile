docker_build:
	docker pull postgres:11

docker_run:
	# Make a directory to save your local db volume.
	mkdir -p ./cache/data

	# We are exporing our local 5444 port to dockers 5432
	# We saving our postgress passwording as enviroment variable to not password prompt is needed.
	# If the e flag was not present we would hazve to enter our password manually during each docker exec command
	docker run --name pg-docker-11 \
	-e POSTGRES_PASSWORD=docker -d \
	-p 5444:5432 \
	--mount type=bind,source=$(shell pwd)/cache/data,target=/var/lib/postgresql/data \
	postgres:11

docker_inspect:
	# Inspect the container
	docker inspect pg-docker-11 

docker_logs:
	# View the logs of the container is something goes wrong
	docker logs  pg-docker-11 

docker_bash:
	# Connet to the database via bin/bash
	docker exec -it pg-docker-11 /bin/bash

create_adventureworks_db:
	# Create a "adventureworks" database
	docker exec -it pg-docker-11 psql -U postgres -c "CREATE DATABASE \"Adventureworks\";"

load_adventure_works: create_adventureworks_db
	# Load the database into the container from local machine.
	docker exec -i pg-docker-11 psql -U postgres -d Adventureworks < databases/adventure_works.sql

create_dvd_rental:
	# Create a "adventureworks" database
	docker exec -it pg-docker-11 psql -U postgres -c "CREATE DATABASE \"dvdrental\";"

load_dvd_rental:
	# Load the database into the container from local machine.
	docker exec -i pg-docker-11 psql -U postgres -d dvdrental < databases/dvdrental.tar

view_database:
	\d

show_database_version:
	SHOW server_version;

disconnect from postgres:
	# Run the following command
	\q

