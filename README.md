# Dockerfile for Meross smartplugs script

Dockerfile that creates a docker image that will run this script:
- https://github.com/luisgs/read_expose_dht_sensors.git

Dockerizing this script allows us to spin several instances without maintainance.

## Docker

Dockerfile will expose data via port 8000 by default, but it can be changed within the
Dockerfile if necessary or during executition of the docker itself (compose). When ready, simply use the Dockerfile to
build the image.

```sh
sudo docker build -t dockerfile_meross .
```

Example of running this docker image for a meross sensor:
```sh
[sudo] docker run --rm -e EMAIL=email.com -e PASSWORD=password 0.0.0.0:8040:8000 meross
```

Docker compose can look like this:
```yaml
services:
  meross:
    image: paneraccoon/meross_stat:latest
    container_name: meross_smartplug1
    restart: unless-stopped
    environment:
      - MEROSS_EMAIL=${EMAIL}
      - MEROSS_PASSWORD=${MEROSS_PASSWORD}
      - DEVICE_NAME=smartplug
      - READ_INTERVAL=60
    ports:
     - 8040:8000
  ```
