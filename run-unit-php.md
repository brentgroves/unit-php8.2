https://unit.nginx.org/installation/#docker-images
https://unit.nginx.org/installation/#installation-docker
https://hub.docker.com/_/php
https://unit.nginx.org/howto/docker/
http://unit.nginx.org/howto/samples/#php

docker pull unit:php8.2
docker run -d unit:php8.2

docker cp "nginx-php:/usr/local/etc/php" "`pwd`/config"


# run with custom nginx config and your own code
docker run --name nginx-php -p 80:8080 -v "`pwd`/config/nginx/conf.d/:/etc/nginx/conf.d/" -v "`pwd`/webroot/:/var/www/html/" trafex/php-nginx

docker run --name unit-php -p 8080:8000 -v "`pwd`/www/:/www/" unit:php8.2

Upload the app config to Unit and test it:

# curl -X PUT --data-binary '{
  "listeners": {
      "*:8080": {
          "pass": "applications/php"
      }
  },
  "applications": {
      "php": {
          "type": "php",
          "root": "/www/"
      }
  }
  }' --unix-socket /path/to/control.unit.sock http://localhost/config/
https://stackoverflow.com/questions/55585586/how-to-access-control-unit-sock-with-nginx-for-securely-proxying-unit-api
--control 127.0.0.1:8080
$ curl http://localhost:8080

    Hello, PHP on Unit!

export UNIT=$(                                             \
      docker run -d --mount type=bind,src="$(pwd)",dst=/www  \
      -p 8080:8000 brentgroves/unit:php8.2                 \
  )


The command mounts the host’s current directory where your app files are stored to the container’s /www/ directory and publishes the container’s port 8000 that the listener will use as port 8080 on the host, saving the container’s ID in the UNIT environment variable.

# stop and remove container
docker rm $(docker stop $(docker ps -a -q --filter ancestor=trafex/php-nginx --format="{{.ID}}"))

## run interactive terminal
docker exec -it some-nginx /bin/bash
docker exec -it tmp-nginx-container sh

docker rm $(docker stop $(docker ps -a -q --filter ancestor=unit:php8.2 --format="{{.ID}}"))

