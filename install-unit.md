To install and run Unit from official builds at Docker Hub:

docker pull unit:TAG
docker run -d unit:TAG

docker pull unit:php8.2
docker pull unit
# build your image
docker build -t brentgroves/1.30.0-php8.2:1 

docker run --name unit -d unit:php8.2 -p 8080:8000