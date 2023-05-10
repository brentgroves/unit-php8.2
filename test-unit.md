http://unit.nginx.org/howto/docker/
http://unit.nginx.org/howto/samples/#php

export UNIT=$(                                             \
      docker run -d --mount type=bind,src="$(pwd)",dst=/www  \
      -p 8080:8000 unit:1.30.0-python3.11                 \
  )
export UNIT=$(                                             \
      docker run -d --mount type=bind,src="$(pwd)",dst=/www  \
      -p 8080:8000 brentgroves/unit:php8.2                 \
  )

export UNIT=$(                                             \
      docker run -d --mount type=bind,src="$(pwd)",dst=/www  \
      -p 8080:8000 unit::php8.2                 \
  )

docker run -d --mount type=bind,src="$(pwd)",dst=/www -p 8080:8000 unit::php8.2

docker run --name some-nginx -v /home/brent/src/linux-utils/nginx/docker/nginx/test/conf.d/:/etc/nginx/conf.d/:ro -v /home/brent/src/linux-utils/nginx/docker/webroot:/usr/share/nginx/html:ro -d -p 8080:80 nginx
