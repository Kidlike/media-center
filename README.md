# media-center
Docker based integration for media center related [companion tools](https://www.reddit.com/r/radarr/comments/hbwnb2/a_list_of_all_companion_tools_and_software/)

#### Basics / Prerequisites:

- [x] torrent ([Transmission](https://github.com/transmission/transmission))
- [x] vpn ([NordVPN](https://nordvpn.com/))


#### Companion Tools _(in order of TODO priority)_:
- [ ] [Radarr](https://github.com/Radarr/Radarr)
- [ ] [Sonarr](https://github.com/Sonarr/Sonarr)
- [ ] [Traktarr](https://github.com/l3uddz/traktarr)
- [ ] [Bazarr](https://github.com/morpheus65535/bazarr)


### Configure

Use a local `.env` file with all required configurations:
```
HOSTNAME='tardis'
LOCAL_NETWORK='192.168.1.0/24'
DNS_LIST='1.1.1.1,1.0.0.1'
TIMEZONE='Europe/Zurich'

NORDVPN_USER='...'
NORDVPN_PASS='...'
NORDVPN_CONNECT_TO='Switzerland'
NORDVPN_TECHNOLOGY='NordLynx'

TRANSMISSION_USER='...'
TRANSMISSION_PASS='...'
TRANSMISSION_DIR_CONFIG='./data/transmission/config'
TRANSMISSION_DIR_DOWNLOADS='./data/transmission/downloads'
TRANSMISSION_DIR_WATCH='./data/transmission/watch'

SYNCTHING_DIR_CONFIG='./data/syncthing/config'
SYNCTHING_DIR_DATA1='./data/syncthing/data1'
```


### Run

```shell
mkdir -p ./data/config ./data/downloads ./data/watch
docker-compose up -d
```

- `-d` to persist between host restarts (will automatically start containers after restart)


### Docker Swarm vs Docker Compose

Initially the plan was to implement this with docker swarm (i.e. `docker stack deploy`), but unfortunately it's not yet possible.

This is the runtime error: https://github.com/bubuntux/nordvpn/issues/50

This error is basically a feature that's not yet implemented in docker swarm: https://github.com/moby/moby/issues/25885  

This can be reproduced by running `docker stack deploy -c docker-stack.yaml media-center-test`
