# Introduction to Portainer

Start here 👉🏽[https://www.portainer.io/](https://www.portainer.io/) </br>
Documentation 👉🏽[https://docs.portainer.io/](https://docs.portainer.io/)

## Portainer installation

Let's go ahead with a local docker install: 

```
docker run -d -p 8000:8000 -p 9443:9443 --name portainer 
--restart=always 
-v /var/run/docker.sock:/var/run/docker.sock 
-v portainer_data:/data portainer/portainer-ce:2.22.0
```
