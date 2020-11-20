mvn clean install "-Dremote=true" "-DseleniumGridURL=http://USERNAME:KEY@ondemand.saucelabs.com:80/wd/hub" "-Dplatform=Windows" "-Dbrowser=Chrome" "-Dbrowserversion=51" "-Doverwrite.binaries=true"
##


## Install selenium grid 

1. Install docker 
2. Install docker-compose. https://docs.docker.com/compose/install/
3. Create a following file

```yaml
# To execute this docker-compose yml file use `docker-compose -f <file_name> up`
# Add the `-d` flag at the end for detached execution
version: "3"
services:
  selenium-hub:
    image: selenium/hub:3.141.59-lithium
    container_name: selenium-hub
    restart: always
    ports:
      - "4444:4444"
  chrome:
    image: selenium/node-chrome:3.141.59-lithium
    restart: always
    volumes:
      - /dev/shm:/dev/shm
    depends_on:
      - selenium-hub
    environment:
      - HUB_HOST=selenium-hub
      - HUB_PORT=4444
  firefox:
    image: selenium/node-firefox:3.141.59-lithium
    restart: always
    volumes:
      - /dev/shm:/dev/shm
    depends_on:
      - selenium-hub
    environment:
      - HUB_HOST=selenium-hub
      - HUB_PORT=4444
```


4. Run the following command.

```shell
$ docker-compose up -d 
```