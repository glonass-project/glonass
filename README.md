# glonass
Project contains 4 repos (as many as containers) and 1 more container for redis. There are:

## glonass-node-geoapi-polling-server
[![Build Status](https://travis-ci.org/glonass-project/glonass-node-geoapi-polling-server.svg?branch=master)](https://travis-ci.org/glonass-project/glonass-node-geoapi-polling-server)

This micro service provide poll requests to fire-group api to gain list of devices and coordinates of them. This service subscribes for HAS_USERS channel of redis and if message delivered it starts polling data from api and pushing it to the redis on GEO_STATE channel, if false message recieved it will stops and start waiting for new events.

## glonass-node-cluster
[![Build Status](https://travis-ci.org/glonass-project/glonass-node-cluster.svg?branch=master)](https://travis-ci.org/glonass-project/glonass-node-cluster)

This micro service provide support for client side socket.io events. When first client connected this service push notification to the redis node to HAS_USERS channel, and waiting for GEO_STATE events, when this event comming node-cluster push notification to client application with array of devices with locations of them.

## glonass-client
Client side application written using React and socket.io with leaflet.

## glonass-nginx-front-end
Reverse proxy for glonass-node-cluster application. Also serves client side application and static files.

## redis.db
Used as MQ service and storage of active users count.
