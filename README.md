# glonass - Geo Tracking System
![Demo-1](https://github.com/glonass-project/glonass/blob/master/demo-desktop.png)
![Demo-2](https://github.com/glonass-project/glonass/blob/master/demo-desktop-2.png)
![Demo-3](https://github.com/glonass-project/glonass/blob/master/demo-mobile-1.png)
![Demo-4](https://github.com/glonass-project/glonass/blob/master/demo-mobile-2.png)
![Demo-5](https://github.com/glonass-project/glonass/blob/master/demo-mobile-3.png)
![Demo-6](https://github.com/glonass-project/glonass/blob/master/demo-mobile-4.png)

Project contains 4 repos (as many as containers) and 1 more container for redis. There are:

### [glonass-node-geoapi-polling-server](https://github.com/glonass-project/glonass-node-geoapi-polling-server)
[![Build Status](https://travis-ci.org/glonass-project/glonass-node-geoapi-polling-server.svg?branch=master)](https://travis-ci.org/glonass-project/glonass-node-geoapi-polling-server)

This micro service provide poll requests to fire-group api to gain list of devices and coordinates of them. This service subscribes for HAS_USERS channel of redis and if message delivered it starts polling data from api and pushing it to the redis on GEO_STATE channel, if false message recieved it will stops and start waiting for new events.

### [glonass-node-cluster](https://github.com/glonass-project/glonass-node-cluster)
[![Build Status](https://travis-ci.org/glonass-project/glonass-node-cluster.svg?branch=master)](https://travis-ci.org/glonass-project/glonass-node-cluster)

This micro service provide support for client side socket.io events. When first client connected this service push notification to the redis node to HAS_USERS channel, and waiting for GEO_STATE events, when this event comming node-cluster push notification to client application with array of devices with locations of them.

### [glonass-client](https://github.com/glonass-project/glonass-client)
Client side application written using React and socket.io with leaflet.

### [glonass-nginx-front-end](https://github.com/glonass-project/glonass-nginx-front-end)
Reverse proxy for glonass-node-cluster application. Also serves client side application and static files.

### redis.db
Used as MQ service and storage of active users count.

## Development
If you want to contribute to this project you should first build this app by yourself in few simple steps:

1. Before that you should already have python, pip, docker, docker-compose.

2. Run this script: 

```sh
  git clone https://github.com/glonass-project/glonass.git
  cd glonass
  git clone https://github.com/glonass-project/glonass-node-geoapi-polling-server.git
  git clone https://github.com/glonass-project/glonass-node-cluster.git
  git clone https://github.com/glonass-project/glonass-client.git
  git cloen https://github.com/glonass-project/glonass-nginx-front-end.git
  docker-compose up --build
```

That's it!

## Production
In production build you don't need all repose from previous step, you just should:
```sh
  docker-compose -f docker-compose.prod.yml up
```
That's all.

## Credits
[@mikefaraponov](https://github.com/mikefaraponov)
