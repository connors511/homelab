# Homelab
This is my little collection of interesting reads, inspirations and services for a homelab.


"Perfect Home Server" [survey responses](https://docs.google.com/spreadsheets/d/1FuXck6l1NSc2eG0kfXLHNj5xo_Yjltra_ia3AxadG1Q/edit#gid=330853588), source: https://www.youtube.com/watch?v=Gv023LpzUwQ&feature=youtu.be&t=14m3s

## To try
* Downloaders
  * Deluge
  * nZEDb
  * Youtube downloader -> plex music + videos ( https://github.com/Rudloff/alltube )
  * Hentrix - crawl websites
  * MusicBrainz
    * ~~lsiodev/musicbrainz~~ This container can't seem to start properly.
* Reverse proxy for subdomain -> vm (SSL termination)
  * Consul
    * With: http://jlordiales.me/2015/02/03/registrator/
  * HAProxy
  * https://github.com/Trikitaum/rancher-proxy ?
* Storage related
  * Owncloud / Seafile
  * Steam proxy cache
    * Ready to go Docker image: https://hub.docker.com/r/miquella/lancache/
    * Alternative, based on Nginx: https://hub.docker.com/r/mpawlowski/lancache/
  * Apt-get mirror / cache
    * https://github.com/sameersbn/docker-apt-cacher-ng
    * https://github.com/sgirones/apt-mirror-docker
  * ISO repo?
  * Backup
  * Crashplan
  * Docker image cache for LAN
    * Reads:
      * http://www.slideshare.net/Docker/https-dldropboxusercontentcomu20637798docker-meetup-freiburg
      * https://blog.docker.com/2015/10/registry-proxy-cache-docker-open-source/
      * http://www.tothenew.com/blog/set-up-docker-registry-proxy-cache-server/
* Network
  * Fail2ban?
  * DNS
  * DHCP
  * Monitoring
    * Observium
    * Zabbix
    * Inciga
    * [ELK](https://www.digitalocean.com/community/tutorials/how-to-install-elasticsearch-logstash-and-kibana-elk-stack-on-ubuntu-14-04) (This is also capable of generic logging)
    * [Sensu](https://sensuapp.org/)
  * AAA
    * LDAP?
* Chat
  * [Let's chat](https://sdelements.github.io/lets-chat/)
  * [Kaiwa](http://getkaiwa.com/)
  * [IRC](http://archive.news.softpedia.com/news/Building-Your-Own-IRC-Server-With-Services-40772.shtml)
    * [UnrealIRCd](https://www.unrealircd.org/)
    * [Anope](http://www.anope.org/)
* IaaS
  * [Docker](https://www.docker.com/)
  * [Mesos](http://mesosphere.com/)
    * [Running on Rancher](http://rancher.com/running-a-mesos-cluster-on-rancheros/)
* CI / CD
  * [comparison](http://www.quora.com/What-is-the-difference-between-Bamboo-CircleCI-CIsimple-Ship-io-Codeship-Jenkins-Hudson-Semaphoreapp-Shippable-Solano-CI-TravisCI-and-Wercker)
  * [Jenkins](http://jenkins-ci.org)
  * [Go](http://www.go.cd/)
  * [Drone.io](https://drone.io/)
    * Rancher has a guide [here](http://rancher.com/building-a-scalable-ci-deployment-with-drone-rancher-and-docker-recorded-august-meetup/).
* Document Management
  * [Paperless](https://github.com/danielquinn/paperless)
  * [Ambar](https://ambar.cloud/)
* Misc
  * [Phabricator](http://phabricator.org/)
  * UniFi
    * Find or create docker images for UniFi and mFi controller. Perhaps using https://github.com/pducharme/UniFi as a base, but splitting the services up, into seperate containers.
  * Synergy?
  * GDocs sync
  * Upside-down-ternet
  * Pastebin alternative?
  * Zoneminder
  * OpenVAS?
  * Transcode downloads til mp4 (plex til telefon streams)
  * VPN
    * [Pritunl](https://pritunl.com/)
  * Wiki?
  * Ghost blog
  * Dashboard
    * http://jpmens.net/2014/11/12/freeboard-a-versatile-dashboard/
    * [Freeboard](https://github.com/Freeboard/freeboard) - see [Jan-Piet Mens](http://jpmens.net/2014/11/12/freeboard-a-versatile-dashboard/)
    * [Dashing-js](https://github.com/fabiocaseri/dashing-js)
  * Email
    * [Zimbra](https://www.zimbra.com/downloads/) with [docker](https://github.com/Zimbra-Community/zimbra-docker).

## Using
* Downloaders
  * Radarr
    * linuxserver/radarr
  * Sonarr
    * linuxserver/sonarr
  * rutorrent
    * Docker: diameter/rtorrent-rutorrent:64
  * Jackett
    * Docker: sdesbure/arch-jackett
  * Headphones
    * Docker: linuxserver/headphones
  * Nzbget
    * Docker: linuxserver/nzbget
  * NZBHydra
    * Docker: linuxserver/hydra
* Network
  * DNS
    * DNS based Ad-blocker
      * Docker: kolyunya/afdns
  * AAA
    * RADIUS
      * [FreeRadius + DaloRADIUS web](http://linuxdrops.com/install-freeradius-with-web-based-management-daloradius-on-centosrhel-debian-ubuntu/)
      * I've created experimental Docker images for [FreeRadius](https://hub.docker.com/r/connors511/radius/) and [DaloRADIUS](https://hub.docker.com/r/connors511/daloradius/) (git repo [here](https://github.com/connors511/docker-freeradius))
    * LDAP?
* IaaS
  * [Docker](https://www.docker.com/)
  * [Rancher](http://rancher.com/)
* CI / CD
  * [Codeship](https://codeship.com/)
* Home automation
  * https://home-assistant.io/
  * Inspiration:
    * http://jpmens.net/2014/02/15/who-phoned-fritzbox-openhab-and-mqtt/
    * http://jpmens.net/2014/01/14/a-story-of-home-automation/
    * http://jpmens.net/2014/01/11/your-location-on-a-web-page-with-mqttitude/
* Chat
  * Discourse

## Tried
* Downloaders
  * Couchpotato
    * Docker: linuxserver/couchpotato
  * Transmission
    * Unable to put finished downloads in different dirs based on rules or labels
  * NzbMegasearch
    * Docker: needo/nzbmegasearch
    * Got slow and integrations randomly stopped working.
* Atlassian
  * _Gonna look into [Phabricator](http://phabricator.org/) instead_
    * It's free, multiple [docker](https://hub.docker.com/r/fredericlb/docker-phabricator/) [images](https://hub.docker.com/r/yesnault/docker-phabricator/) exist and it doesn't run off Java!
  * FishEye
  * Stash
  * Confluence
  * Jira
  * Bamboo
* Configuration Management
  * _Using Rancher, making this undeeded.. Might revisit later for edu purpose_
  * Ansible (Might just go with this, and discard the others..)
  * Cobbler
  * Puppy
  * Chef
* Chat
  * Teamspeak (Voice)
    * ~~Currently running~~ Previously ran with [this docker image](https://hub.docker.com/r/devalx/docker-teamspeak3/)
    * Switched to [Discord](https://discordapp.com/)
 * Network
  * DNS
    * DNS based Ad-blocker
      * https://hub.docker.com/r/arthurkay/sagittarius-a/
        * Didn't block a lot  and using an old lists.
* Home automation
  * OpenHAB
    * Dismissed as having too much complexity for setting up some basic stuff
* Chat
  * Mumble (Voice)
    * Worked fine, but could be easier and more flexible in regards to permissions. Discord does an overall better job and a fraction of the effort.