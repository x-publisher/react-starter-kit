### Docker build
```
$ docker build -t starter-kit .

$ docker run -it \
  -v ${PWD}:/usr/src/app \
  -v /usr/src/app/node_modules \
  -p 3000:3000 \
  --rm \
  starter-kit
```

### Docker Compose
```
$ docker-compose up -d --build

$ docker-compose stop
```

### Docker Machine
```
docker-machine create -d virtualbox sample-kit
$ docker-machine env sample-kit
$ eval $(docker-machine env sample-kit)

$ docker-machine ip sample-kit

$ docker build -t starter-kit .

$ docker run -it \
  -v ${PWD}:/usr/src/app \
  -v /usr/src/app/node_modules \
  -p 3000:3000 \
  --rm starter-kit
```

##### Test the app again in the browser at http://DOCKER_MACHINE_IP:3000/[http://DOCKER_MACHINE_IP:3000/]

##### To get hot-reload working, we need to add an environment variable:
```
$ docker run -it \
  -v ${PWD}:/usr/src/app \
  -v /usr/src/app/node_modules \
  -p 3000:3000 \
  -e CHOKIDAR_USEPOLLING=true \
  --rm starter-kit
```

##### Using the production Dockerfile, build and tag the Docker image:
```
$ docker build -f Dockerfile-prod -t starter-kit-prod .
```
##### Spin up the container:
```
$ docker run -it -p 80:80 --rm starter-kit-prod
```

Assuming you are still using the same Docker Machine, navigate to http://DOCKER_MACHINE_IP in your browser.

##### Fire up the container:
```
$ docker-compose -f docker-compose-prod.yml up -d --build
```

##### Test it out once more in your browser. Then, if you’re done, go ahead and destroy the Machine:
```
$ eval $(docker-machine env -u)
$ docker-machine rm sample
````
