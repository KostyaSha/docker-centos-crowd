### About

Crowd2 docker container that i'm using for https://github.com/jenkinsci/crowd2-plugin testing

### Usage
Not fully automated :atm:

- build image
```
docker build . -t centos-crowd:1
```
- run container
```
docker run -d \
  --name crowd.${your-docker-host-ip}.xip.io \
  -h crowd.${your-docker-host-ip}.xip.io \
  -p 8095:8095 \
  -v /pathat/to/stored/crowd-home:/opt/atlassian-crowd \
  centos-crowd:1
```
- go to `http://crowd.${your-docker-host-ip}.xip.io:8095/crowd` and configure crowd instance (i.e. license on first run)

### Kudos
- DNS resolver http://xip.io/
