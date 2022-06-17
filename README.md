# compose
> docker-compose configuration to run openspaceteam

## Instructions

```
$ git clone git@github.com:openspaceteam/compose.git
$ cd compose
# Clone submodules (frontend and backend code)
$ git submodule update --init --recursive
$ docker-compose up -d --build
```

## Reverse proxy
You should add an additional reverse proxy (e.g.: nginx) in front of the containers.

This should run on port 80/443. It is recommended to use SSL (e.g.: Let's Encrypt).

You can use the following nginx config on your host (you'll have to add the SSL directives, for example, through Certbot)

```
server {
        server_name your.domain.com;	# change this

        location ~* \.io {
                proxy_http_version 1.1;
                proxy_set_header Upgrade $http_upgrade;
                proxy_set_header Connection "upgrade";
                proxy_set_header Origin "";
                proxy_pass http://127.0.0.1:3388;
        }
        location / {
                proxy_pass http://127.0.0.1:3387;
        }
}
```

## LICENCE

MIT
