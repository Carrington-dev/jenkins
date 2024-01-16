# Docker Lessons/Tutorial

## Run commands inside a docker container
```
docker exec <container_name> <command>
```
examples are
1. With docker compose
```
docker exec jenkins/jenkins cat /var/jenkins_home/secrets/initialAdminPassword
```
2. With docker
```
docker exec vroomy cat python3 manage.py makemigrations
docker exec vroomy cat python3 manage.py migrate
docker exec vroomy cat python3 manage.py runserver
```

## Preserve the state of jenkins in docker image

In order to preserve the state of jenkins running as a docker container we use

```
docker run -d -p 80:8080 -v /root/jenkins_data/jenkins_home:/var/jenkins_home jenkins/jenkins:lts
```
the above will or may give errors
```
docker run -d -p 80:8080 -v /root/jenkins_data/jenkins_home:/var/jenkins_home -u root jenkins/jenkins:lts
```

This is will save docker data in our ubuntu instance directly hence data on jenkins docker image won't be lost each time we restart docker images or docker itself

## To restart a contianer

```bash
docker restart <continer-id>
```

## To stop a contianer

```bash
docker stop <continer-id>
```

## To delete a contianer

```bash
docker rm <continer-id>
```

## To see all contianers

```bash
docker ps -a 
```

## To see images

```bash
docker images
```

