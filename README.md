# homelab
a place to document my homelab stuff

## Infrastructure
* 10 Intel NUCS (Pentium N3700, 8GB RAM, 500GB SSD)
* 5 NVIDIA TK1 Jetsons 
* Supermicro Server (NAS)
* Dell Optiplex Desktop (i5-3470, 16GB RAM, 1TB SSD)

Here's a [blog post](https://blog.fosketts.net/2020/09/22/tortoise-or-hare-nvidia-jetson-tk1/) from someone that bought the same thing from ebay...

To provisoin the NUCS, I [forked](https://github.com/stephenl03/matchbox) [matchbox](https://github.com/poseidon/matchbox) as I wanted it to exit the iPXE process if a config wasn't present and installed Fedora Server.

After installing Fedora Server, I deployed k3s using [k3s-ansible](https://github.com/k3s-io/k3s-ansible). I opted to disable the built-in servicelb, traefik and metrics-server.

## k3s
I am running the below services, or in the process of migrating them from docker to k3s

* metallb
* traefik
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
* longhorn
* metrics-server

## metrics-server
I disabled the bundled metric-server in k3s because it was crashing and was a number of versions behind. I installed the latest version, which as of this time is v0.5.2 via the [components.yaml](https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml) file.
```
kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml
```

## Longhorn
For storage I used longhorn. I first attempted rook-ceph, but that was a dumpster fire, so I gave up. I initially installed longhorn via the helm chart, but ran into issues and resorted to just deploying with kubectl. I will probably revisit the helm chart as I would rather deploy that instead.
```
kubectl apply -f https://raw.githubusercontent.com/longhorn/longhorn/master/deploy/longhorn.yaml
```

## MetalLB
MetalLB is awesome and I used it in the past.
```
helm repo add metallb https://metallb.github.io/metallb
helm repo update
helm upgrade --install metallb metallb/metallb -n kube-system --values helm/metallb/values.yaml
```

