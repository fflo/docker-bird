# BIRD Routing Daemon on Docker

BIRD Routing Daemon Docker container based on Ubuntu 20.04 LTS.

### Usage

To start a bird2 instance running the latest version:

```
$ docker run fflo/bird -v /YourPathTo/bird.conf:/bird/bird.conf:ro
```

### Hint

Do not forget to expose your BIRD Routing Daemon port(s) needed for communitcation with peers.
For example Border Gateway Protocol (BGP) requires TCP port 179.

```
$ docker run fflo/bird -e 179:179 -v /YourPathTo/bird.conf:/bird/bird.conf:ro
```
