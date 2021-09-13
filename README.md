# homelab
a place to document my homelab stuff

## Infrastructure
* 10 Intel NUCS (Pentium N3700, 8GB RAM, 500GB SSD)
* 5 NVIDIA TK1 Jetsons 
* Supermicro Server (NAS)
* Dell Optiplex Desktop (i5-3470, 16GB RAM, 1TB SSD)

Here's a [blog post](https://blog.fosketts.net/2020/09/22/tortoise-or-hare-nvidia-jetson-tk1/) from someone that bought the same thing from ebay...

To provisoin the NUCS, I [forked](https://github.com/stephenl03/matchbox) [matchbox](https://github.com/poseidon/matchbox) as I wanted it to exit the iPXE process if a config wasn't present and installed Fedora Server.

After installing Fedora Server, I deployed k3s using [ansible](https://github.com/k3s-io/k3s-ansible). I opted to disable the built-in servicelb and traefik.

## k3s
I am running the below services, or in the process of migrating them from docker to k3s

* metallb (Installed via helm)
* traefik (Installed via helm)
* radarr
* sonarr
* nzbget
* deluge
* home assistant
* mdnsrepeater
* mosquitto
* node-red
* zwavejs2mqtt
* nginx server
* unifi
