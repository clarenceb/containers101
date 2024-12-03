# Containers 101

## Create a Dockerfile

```sh
cat <<EOF> Dockerfile
FROM debian:12
LABEL maintainer="Contoso, Inc."
RUN apt-get update && \\
  apt-get install -y nginx
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
EOF
```

## Build the image

```sh
docker build -t nginx-demo:v1.0.0 .
```

## List the images

```sh
docker images
```

## View the build history

```sh
docker history nginx-demo:v1.0.0
```

## Generate a Dockerfile for an app with Draft

Install `draft` from https://github.com/Azure/draft

Create a new web app and generate a Dockerfile

```sh
# dotnet new webapp --name demoapp
cd demoapp
draft create --dockerfile-only
# Choose "8.0" as the SDK version

# Build the image
docker build -t demoapp .
docker images

# Run the image
docker run -d -p 8080:80 demoapp

# Test the app
curl http://localhost:8080

# Remove the container
docker rm -f $(docker ps -q)

# Remove the image
docker rmi demoapp

# Remove the Dockerfile
rm Dockerfile
```

## Docker Compose Demo 1 (Wordpress)

```sh
docker compose up
# CTRL+C to stop
docker compose down
docker volume prune
```

## Docker Compose Demo 2 (Voting App)

```sh
docker compose -f voting-app-compose.yaml up
# CTRL+C to stop
docker compose -f voting-app-compose.yaml down
docker volume prune
```

## Explore

- Networks
- Volumes
- Images
- Builds
- Containers
- Docker Compose files (e.g. healthcheck scripts)
- Pruning resources

## Credits

* [Example Voting App](https://github.com/dockersamples/example-voting-app) - from Docker samples, used some of the code files

  * healthchecks/postgres.sh
  * healthchecks/redis.sh
  * voting-app-compose.yaml
  * See license `LICENSE-voting-app.txt` for those files
