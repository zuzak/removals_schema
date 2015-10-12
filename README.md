# Removals schema
Schema files for removal project

###To use the generator
```shell
npm install
```

###To output 10 events to stdout
```shell
node generate.js event.json 10
```

###To output 10 heartbeats to stdin

```shell
node generate.js heartbeat.json 10
```


##Guidelines

### event.json
This is triggered on an event and should be sent in realtime.
Clients are responsible for:
* setting a transaction ID that is auto incrementing and unique to the centre its referring.
* also for resetting this after it reaches ```1000000000``` before it reaches ```2000000000```
* queueing these for submission should a ```4xx``` or ```5xx``` be received or a ```5 second``` timeout be reached and retry at regular intervals
* raise alerts to relevant parties should errors occur
* if a ```3xx``` is received follow the redirection

### heartbeat.json
This is sent at regular intervals (as agreed) with the provider which provides fundamental 
Clients are responsible for:
* not queuing if failure occurs
