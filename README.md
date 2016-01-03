# docker-registry-auth

This image is based on the odaniait/docker-nginx-basic-auth-proxy image.

In my setup there is already an ssl termination in front of the registry. Cause of that i had problems using the build in
authentication mechanisms. I am using this proxy in between to do the basic auth for the registry. Cause the ssl termination
is done in front, the forwarded scheme is set to https by default.

An example for docker compose looks like this:

```
nginx:
  image: odaniait/docker-registry-auth
  links:
    - registry:app
  volumes:
    - /etc/htpasswd:/auth
  restart: always
  tty: true
  stdin_open: true
registry:
  image: registry:2
  volumes:
    - /media/volumes/docker-registry:/var/lib/registry
  restart: always
  tty: true
  stdin_open: true
```

Under /etc/htpasswd is a file called docker.htpasswd which is used for authentication.
