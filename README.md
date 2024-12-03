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

```
# dotnet new webapp --name demoapp
cd demoapp
draft create --dockerfile-only
```
