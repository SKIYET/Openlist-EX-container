# Openlist-EX-container

[Overview](#Overview)

[Deployment](#Deployment)

[First run](#first)

[More usages and precautions](#more)  


## <a id="Overview"></a>Overview

This project integrates Openlist, Aria2, qBittorrent and Caddy reverse proxy in a single container.

Support AMD64/Arm64/Armv7 architecture.


## <a id="Deployment"></a>Deployment

 1. Download [docker-compose file](https://github.com/huancun/Openlist-EX-container/blob/main/docker-compose.yml) and save as `docker-compose.yml`.

 2. Set envs and run container with following command:

        docker-compose up -d


## <a id="first"></a>First run

1. Run `docker logs openlist-ex` , you can get the initial password of openlist.

2. Visit < ip address or domain name >:< CADDY_WEB_PORT > to open openlist.

3. Visit < ip address or domain name >:< CADDY_WEB_PORT >/portalpage to open portal page.

4. Visit < ip address or domain name >:< CADDY_WEB_PORT >/ariang , you can open AriaNg panel. Click `AriaNg Settings` > `RPC`, set `RPC Secret Token` and check whether protocol and port are the same with URL in browser address bar.

5. Visit < ip address or domain name >:< CADDY_WEB_PORT >/qbitweb , you can open qBittorrent WebUI. Open log/qBittorrent/current file under docker volume diretory to get temporary password, Type default username `admin` and temporary password to login. Click `tools` > `options` > `Web UI` to change username and password, recommend strong password. 

6. Visit < ip address or domain name >:< CADDY_WEB_PORT >/qbitvue , you can open VueTorrent qBittorrent WebUI. 

7. Offline download settings:

   Open openlist manage page, `tools` > `Other`.

   Fill Aria2 uri with: http://localhost:61601/jsonrpc , and Aria2 Secret Token.

   Fill Qbittorrent url with: http://< qbit username>:< qbit password >@localhost:61602/


## <a id="more"></a>More usages and precautions

 1. If you migrate from previous openlist installation, you can bind container volume to the previous openlist data directory.

 2. Aria2 settings which changed in AriaNg panel will be reset after Aria2 restarted. You can modify aria2/aria2.conf file in data directory to change Aria2 settings persistently.

 3. Set openlist admin password.

 ```
     # Set random password
     docker exec openlist-ex openlist admin random

     # Set admin password as 'NEW_PASSWORD'
     docker exec openlist-ex openlist admin set NEW_PASSWORD
```

 4. You can check logs of aria2/qBittorrent/caddy from log dir in container volume.
