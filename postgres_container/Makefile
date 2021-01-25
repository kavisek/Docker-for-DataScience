mkdir_volume_store:
	mkdir -p $HOME/workspaces/docker/volumes/postgres11

docker_build:
	docker pull postgres:11

docker_run:
	# We are exporing our local 5431 port to dockers 5432
	# We saving our postgress passwording as enviroment variable to not password prompt is needed.
	# If the e flag was not present we would have to enter our password manually during each docker exec command
	docker run --rm --name pg-docker \
	-e POSTGRES_PASSWORD=docker -d \
	-p 5432:5432 \
	-v $HOME/docker/volumes/postgres:/var/lib/postgresql11/data \
	postgres


docker_exec:
	docker exec -it pg-docker psql -U postgres


view_database:
	\d

show_database_version:
	SHOW server_version;

disconnect from postgres:
	# Run the following command
	\q
