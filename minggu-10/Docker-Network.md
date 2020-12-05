# Praktik Docker Networking
Pada Praktik ini akan dipelajari tentang konsep Docker Networking. Akan ada beberapa contoh konsep networking, belajar tentang Bridge networking, dan Overlay networking.

## Bagian #1 - Basic Networking 
### Step 1: The Docker Network Command
**docker network** adalah perintah utama untuk konfigurasi dan me-manage container networks. Jalankan perintah **docker network** dari terminal pertama.
```terminal
$ docker network

Usage:  docker network COMMAND

Manage networks

Commands:
  connect     Connect a container to a network
  create      Create a network
  disconnect  Disconnect a container from a network
  inspect     Display detailed information on one or more networks
  ls          List networks
  prune       Remove all unused networks
  rm          Remove one or more networks

Run 'docker network COMMAND --help' for more information on a command.
```
Output menunjukkan cara menggunakan perintah serta semua sub-perintah *docker network*.

### Step 2: List network
Jalankan perintah **docker network ls** untuk melihat *container networks* yang tersedia saat ini di dalam Docker host.
```terminal
docker network ls
NETWORK ID          NAME                DRIVER              SCOPE
c31fcfcd6e1f        bridge              bridge              local
3020ad9d96a4        host                host                local
51d28444a7b9        none                null                local
```

### Step 3: Inspect sebuah network
Perintah **docker network inspect** digunakan untuk melihat konfigurasi network secara detail. Detail yang dapat dilihat adalah name, ID, driver, IPAM driver, subnet info, connected containers, dan banyak lagi.

Gunakan perintah **docker network inspect <network>** untuk melihat konfigurasi detail dari *container network* di dalam host. Perintah dibawah ini menunjukkan detail network bernawa **bridge**
```terminal
$ docker network inspect bridge
[
    {
        "Name": "bridge",
        "Id": "c31fcfcd6e1ff5192f1c6f2e2250f0182ca1af4eb122e3c5a09c7c34f0ffc94f",
        "Created": "2020-12-03T07:45:48.151542364Z",
        "Scope": "local",
        "Driver": "bridge",
        "EnableIPv6": false,
        "IPAM": {
            "Driver": "default",
            "Options": null,
            "Config": [
                {
                    "Subnet": "172.17.0.0/16"
                }
            ]
        },
        "Internal": false,
        "Attachable": false,
        "Ingress": false,
        "ConfigFrom": {
            "Network": ""
        },
        "ConfigOnly": false,
        "Containers": {},
        "Options": {
            "com.docker.network.bridge.default_bridge": "true",
            "com.docker.network.bridge.enable_icc": "true",
            "com.docker.network.bridge.enable_ip_masquerade": "true",
            "com.docker.network.bridge.host_binding_ipv4": "0.0.0.0",
            "com.docker.network.bridge.name": "docker0",
            "com.docker.network.driver.mtu": "1500"
        },
        "Labels": {}
    }
]
```

### Step 4: List dari network driver plugin
Perintah **docker info** menunjukkan informasi menarik tentang instalasi Docker.
Jalankan perintah **docker info** dan melihat info list dari *network plugins*
```terminal
$  docker info
Client:
 Debug Mode: false
 Plugins:
  app: Docker App (Docker Inc., v0.9.1-beta3)

Server:
 Containers: 0
  Running: 0
  Paused: 0
  Stopped: 0
 Images: 0
 Server Version: 19.03.11
 Storage Driver: overlay2
  Backing Filesystem: xfs
  Supports d_type: true
  Native Overlay Diff: true
 Logging Driver: json-file
 Cgroup Driver: cgroupfs
 Plugins:
  Volume: local
  Network: bridge host ipvlan macvlan null overlay
  Log: awslogs fluentd gcplogs gelf journald json-file local logentries splunk syslog
 Swarm: inactive
 Runtimes: runc
 Default Runtime: runc
 Init Binary: docker-init
 containerd version: 7ad184331fa3e55e52b890ea95e65ba581ae3429
 runc version: dc9208a3303feef5b3839f4323d9beb36df0a9dd
 init version: fec3683
 Security Options:
  apparmor
  seccomp
   Profile: default
 Kernel Version: 4.4.0-194-generic
 Operating System: Alpine Linux v3.12 (containerized)
 OSType: linux
 Architecture: x86_64
 CPUs: 8
 Total Memory: 31.42GiB
 Name: node1
 ID: 67P6:XJM5:5YAG:ATWW:DRQU:DQVH:IN5S:S4BC:QCGA:BPUC:LAAM:YRMO
 Docker Root Dir: /var/lib/docker
 Debug Mode: true
  File Descriptors: 24
  Goroutines: 43
  System Time: 2020-12-03T07:52:53.009011551Z
  EventsListeners: 0
 Registry: https://index.docker.io/v1/
 Labels:
 Experimental: true
 Insecure Registries:
  127.0.0.1
  127.0.0.0/8
 Live Restore Enabled: false
 Product License: Community Engine

WARNING: API is accessible on http://0.0.0.0:2375 without encryption.
         Access to the remote API is equivalent to root access on the host. Refer
         to the 'Docker daemon attack surface' section in the documentation for
         more information: https://docs.docker.com/engine/security/security/#docker-daemon-attack-surface
WARNING: No swap limit support
WARNING: bridge-nf-call-iptables is disabled
WARNING: bridge-nf-call-ip6tables is disabled
```

## Bagian #2 - Bridge Networking
### Step 1: Basics
Setiap instalasi baru dari Docker sudah terdapat *pre-build* network bernama ***bridge***. Verifikasi ini dengan **docker network ls**.
```terminal
$ docker network ls
NETWORK ID          NAME                DRIVER              SCOPE
c31fcfcd6e1f        bridge              bridge              local
3020ad9d96a4        host                host                local
51d28444a7b9        none                null                local
```
>The output above shows that the bridge network is associated with the bridge driver. It’s important to note that the network and the driver are connected, but they are not the same. In this example the network and the driver have the same name - but they are not the same thing!
>
>The output above also shows that the bridge network is scoped locally. >This means that the network only exists on this Docker host. This is true >of all networks using the bridge driver - the bridge driver provides >single-host networking.
>
>All networks created with the bridge driver are based on a Linux bridge (a.k.a. a virtual switch).

Install perintah **brctl** dan gunakan itu untuk melihat list dari Linux Bridge yang ada di Docker host. Dapat diinstal menggunakan perintah **sudo apt-get install bridge-utils**.
```terminal
$ apk update
fetch http://dl-cdn.alpinelinux.org/alpine/v3.12/main/x86_64/APKINDEX.tar.gz
fetch http://dl-cdn.alpinelinux.org/alpine/v3.12/community/x86_64/APKINDEX.tar.gz
v3.12.1-69-gbdfcc49399 [http://dl-cdn.alpinelinux.org/alpine/v3.12/main]
v3.12.1-71-gfc587ffaa2 [http://dl-cdn.alpinelinux.org/alpine/v3.12/community]
OK: 12763 distinct packages available
[node1] (local) root@192.168.0.8 ~
$ apk add bridge
(1/1) Installing bridge (1.5-r4)
OK: 404 MiB in 151 packages
```

Lalu, lihat list bridge dengan meenjalankan perintah **brctl show**
```terminal
$ brctl show
bridge name     bridge id               STP enabled     interfaces
docker0         8000.02425209e75d       no
```
>The output above shows a single Linux bridge called docker0. This is the bridge that was automatically created for the bridge network. You can see that it has no interfaces currently connected to it.

Jalankan perintah **ip a** untuk melihat detail dari ***docker0 bridge***
```terminal
$ ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN qlen 1
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
2: docker0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc noqueuestate DOWN
    link/ether 02:42:52:09:e7:5d brd ff:ff:ff:ff:ff:ff
    inet 172.17.0.1/16 brd 172.17.255.255 scope global docker0
       valid_lft forever preferred_lft forever
8470: eth0@if8471: <BROADCAST,MULTICAST,UP,LOWER_UP,M-DOWN> mtu 1500 qdisc noqueue state UP
    link/ether 5a:e3:3b:ef:e3:3e brd ff:ff:ff:ff:ff:ff
    inet 192.168.0.8/23 scope global eth0
       valid_lft forever preferred_lft forever
8476: eth1@if8477: <BROADCAST,MULTICAST,UP,LOWER_UP,M-DOWN> mtu 1500 qdisc noqueue state UP
    link/ether 02:42:ac:12:00:3f brd ff:ff:ff:ff:ff:ff
    inet 172.18.0.63/16 scope global eth1
       valid_lft forever preferred_lft forever
```

### Step 2: Menghubugkan container
***bridge*** network adalah network default dari sebuah container baru. Ini berarti tanpa menyertakan network lain secara spesifik, maka semua container baru akan terkoneksi dengan ***bridge*** network.

Buat container baru dengan menjalankan **docker run -dt ubuntu sleep infinity**.
```terminal
$ docker run -dt ubuntu sleep infinity
Unable to find image 'ubuntu:latest' locally
latest: Pulling from library/ubuntu
da7391352a9b: Pull complete
14428a6d4bcd: Pull complete
2c2d948710f2: Pull complete
Digest: sha256:c95a8e48bf88e9849f3e0f723d9f49fa12c5a00cfc6e60d2bc99d87555295e4c
Status: Downloaded newer image for ubuntu:latest
873b48766380dc323190d64c959e92bf87f017102377764b5ed3245e27d46408
```
Perintah tersebut akan membuat container baru based **ubuntu:latest** image dan akan menjalankan **sleep** agar container berjalan di background. Dapat verifikasi contoh container dengan menjalankan **docker ps**
```terminal
$ docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED         STATUS              PORTS               NAMES
873b48766380        ubuntu              "sleep infinity"    21 minutesago      Up 21 minutes                           optimistic_leakey
```

Dengan tidak menyertakan network secara spesifik dalam perintah **docker run**, maka container akan ditambahkan ke ***bridge*** network.

Jalankan perintah **brctl show** lagi.
```terminal
$ brctl show
bridge name	bridge id		STP enabled	interfaces
docker0		8000.02425209e75d	no		vethd630437
```
Notice ***docker0*** bridge saat ini sudah memiliki interface yang terkoneksi. Interface ini terkoneksi dengan ***docker0*** bridge ke container baru yang baru dibuat.

Dapat dilakukan *inspect* ***bridge*** network lagi dengan menjalankan **docker network inspect bridge**.
```terminal
$ docker network inspect bridge
[
    {
        "Name": "bridge",
        "Id": "c31fcfcd6e1ff5192f1c6f2e2250f0182ca1af4eb122e3c5a09c7c34f0ffc94f",
        "Created": "2020-12-03T07:45:48.151542364Z",
        "Scope": "local",
        "Driver": "bridge",
        "EnableIPv6": false,
        "IPAM": {
            "Driver": "default",
            "Options": null,
            "Config": [
                {
                    "Subnet": "172.17.0.0/16"
                }
            ]
        },
        "Internal": false,
        "Attachable": false,
        "Ingress": false,
        "ConfigFrom": {
            "Network": ""
        },
        "ConfigOnly": false,
        "Containers": {
            "873b48766380dc323190d64c959e92bf87f017102377764b5ed3245e27d46408": {
                "Name": "optimistic_leakey",
                "EndpointID": "d7b52dc479b2d03d767bb99ff819a40ba68db064514243f2aa1f3e4c95e86dca",
                "MacAddress": "02:42:ac:11:00:02",
                "IPv4Address": "172.17.0.2/16",
                "IPv6Address": ""
            }
        },
        "Options": {
            "com.docker.network.bridge.default_bridge": "true",
            "com.docker.network.bridge.enable_icc": "true",
            "com.docker.network.bridge.enable_ip_masquerade": "true",
            "com.docker.network.bridge.host_binding_ipv4": "0.0.0.0",
            "com.docker.network.bridge.name": "docker0",
            "com.docker.network.driver.mtu": "1500"
        },
        "Labels": {}
    }
]
```

### Step 3: Uji konektivitas network
Pada output sebelumnya, perintah **docker network inspect** menampilkan IP address daro container baru.
Ping IP address dari container dari shell prompt dalam Docker host dengan menjalankan perintah ping **-c5 <IPv4 Address>**.
```terminal
$ ping -c5 172.17.0.2
PING 172.17.0.2 (172.17.0.2): 56 data bytes
64 bytes from 172.17.0.2: seq=0 ttl=64 time=0.169 ms
64 bytes from 172.17.0.2: seq=1 ttl=64 time=0.097 ms
64 bytes from 172.17.0.2: seq=2 ttl=64 time=0.130 ms
64 bytes from 172.17.0.2: seq=3 ttl=64 time=0.140 ms
64 bytes from 172.17.0.2: seq=4 ttl=64 time=0.074 ms

--- 172.17.0.2 ping statistics ---
5 packets transmitted, 5 packets received, 0% packet loss
round-trip min/avg/max = 0.074/0.122/0.169 ms
```
Reply diatas menunjukkan bahwa Docker host dapat ping container melewati ***bridge*** network. Tapi dapat verify container dapat terkoneksi ke luar juga. Mari coba install ping prigram, kemudian ping **www.github.con**.

Pertama, kita perlu mengambil ID dari container dari langkah sebelumnya. Dapat menjalankan perintah **docker ps** untuk mengambilnya.
```terminal
$ docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED         STATUS              PORTS               NAMES
873b48766380        ubuntu              "sleep infinity"    32 minutesago      Up 32 minutes                           optimistic_leakey
```

Berikutnya, mari menjalankan shell dalam ubuntu container, dengan menjalankan perintah **docker exec -it <CONTAINER ID> /bin/bash**.
```terminal
$ docker exec -it 873b48766380 /bin/bash
root@873b48766380:/#
```

Berikutnya, perlu install program ping. Mari jalankan perintah **apt-get update && apt-get install -y iputils-ping**.
```terminal
root@873b48766380:/# apt-get update && apt-get install -y iputils-ping
Get:1 http://security.ubuntu.com/ubuntu focal-security InRelease [109 kB]
Get:2 http://archive.ubuntu.com/ubuntu focal InRelease [265 kB]
Get:3 http://security.ubuntu.com/ubuntu focal-security/multiverse amd64 Packages [1165 B]
Get:4 http://security.ubuntu.com/ubuntu focal-security/restricted amd64 Packages [103 kB]
<Snip>
debconf: falling back to frontend: Teletype
Setting up iputils-ping (3:20190709-3) ...
Processing triggers for libc-bin (2.31-0ubuntu9.1) ...
root@873b48766380:/#
```

Mari ping www.github.com dengan menjalankan **ping -c5 www.github.com**
```terminal
root@873b48766380:/#   ping -c5 www.github.com
PING github.com (140.82.112.3) 56(84) bytes of data.
64 bytes from lb-140-82-112-3-iad.github.com (140.82.112.3): icmp_seq=1 ttl=51 time=0.925 ms
64 bytes from lb-140-82-112-3-iad.github.com (140.82.112.3): icmp_seq=2 ttl=51 time=1.01 ms
64 bytes from lb-140-82-112-3-iad.github.com (140.82.112.3): icmp_seq=3 ttl=51 time=2.20 ms
64 bytes from lb-140-82-112-3-iad.github.com (140.82.112.3): icmp_seq=4 ttl=51 time=1.13 ms
64 bytes from lb-140-82-112-3-iad.github.com (140.82.112.3): icmp_seq=5 ttl=51 time=0.995 ms

--- github.com ping statistics ---
5 packets transmitted, 5 received, 0% packet loss, time 4004ms
rtt min/avg/max/mdev = 0.925/1.251/2.201/0.479 ms
root@873b48766380:/#
```

Akhirnya, mari disconnect sheel dari container, dengan menjalankan **exit**
```terminal
exit
[node1] (local) root@192.168.0.8 ~
$
```

Juga perlu stop container ini, jadi dapat bersih dari test yang sudah dijalankan, dengan menjalankan perintah **docker stop <CONTAINER ID>**.
```terminal
$ docker stop 873b48766380
873b48766380
```
>This shows that the new container can ping the internet and therefore has a valid and working network configuration.

## Step 4: Konfigurasi NAT untuk konektivitas external
Pada step ini, akan mulai dengan container ***NGINX*** baru dan map port 8080 di Docker host ke port 80 dalam container. Ini berarti traffic yang mengenai Docker host dengan port 8080 akan melewati port 80 dalam container. 
Mulai container baru berdasar NGINGX image original, dengan menjalankan perintah **$ docker run --name web1 -d -p 8080:80 nginx**.
```terminal
$ docker run --name web1 -d -p 8080:80 nginx
Unable to find image 'nginx:latest' locally
latest: Pulling from library/nginx
852e50cd189d: Pull complete
571d7e852307: Pull complete
addb10abd9cb: Pull complete
d20aa7ccdb77: Pull complete
8b03f1e11359: Pull complete
Digest: sha256:6b1daa9462046581ac15be20277a7c75476283f969cb3a61c8725ec38d3b01c3
Status: Downloaded newer image for nginx:latest
bae5af290920988925916f4d44a9019443a232a39ff06974cb806c1e6a665f8b
```

Review container status dan port mappings dengan menjalankan **docker ps**.
```terminal
docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED          STATUS              PORTS                  NAMES
bae5af290920        nginx               "/docker-entrypoint.…"   23 seconds ago      Up 21 seconds       0.0.0.0:8080->80/tcp   web1
```
>The top line shows the new web1 container running NGINX. Take note of the command the container is running as well as the port mapping - 0.0.0.0:8080->80/tcp maps port 8080 on all host interfaces to port 80 inside the web1 container. This port mapping is what effectively makes the containers web service accessible from external sources (via the Docker hosts IP address on port 8080).
>
>Now that the container is running and mapped to a port on a host interface you can test connectivity to the NGINX web server.
>
>To complete the following task you will need the IP address of your Docker host. This will need to be an IP address that you can reach (e.g. your lab is hosted in Azure so this will be the instance’s Public IP - the one you SSH’d into). Just point your web browser to the IP and port 8080 of your Docker host. Also, if you try connecting to the same IP address on a different port number it will fail.

Dalam beberapa kasus, tidak dapat membuka sebuah session dari web browser, dapat mengoneksikan Docker host menggunakan perintah **curl 127.0.0.1:8080**.
```terminal
$ curl 127.0.0.1:8080
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
    body {
        width: 35em;
        margin: 0 auto;
        font-family: Tahoma, Verdana, Arial, sans-serif;
    }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
```

## Bagian #3 - Overlay Networking
### Step 1: Basics
Dalam langkah ini, akan diinstalasi Swarm baru, join sebuah single worker node, dan verify operasinya berjalan.
Jalankan **docker swarm init --advertise-addr $(hostname -i)**.
```terminal
$ docker swarm init --advertise-addr $(hostname -i)
Swarm initialized: current node (yumm2034th5aayirw4zwi1c2o) is now a manager.

To add a worker to this swarm, run the following command:

    docker swarm join --token SWMTKN-1-42zoc6neu7gc0y0v0zeul2i5ztty1325zxbfqfcpx1p9i2dz2x-d3a11jdd2bbnk8qp0hxrow5zd 192.168.0.18:2377

To add a manager to this swarm, run 'docker swarm join-token manager' and follow the instructions.
```

Dalam terminal pertama copy seluruh perintah ***docker swarm join ...***. kemudian paste ke terminal kedua.
```terminal
$ docker swarm join --token SWMTKN-1-42zoc6neu7gc0y0v0zeul2i5ztty1325zxbfqfcpx1p9i2dz2x-d3a11jdd2bbnk8qp0hxrow5zd 192.168.0.18:2377
This node joined a swarm as a worker.
```

Jalankan perintah **docker node ls** untuk verify bahwa kedua nodes adalah bagian dari Swarm.
```terminal
$ docker node ls
ID                            HOSTNAME            STATUS              AVAILABILITY        MANAGER STATUS      ENGINE VERSION
yumm2034th5aayirw4zwi1c2o *   node1               Ready               Active              Leader              19.03.11
korxqwsc8qua0zoqley0zy7ap     node2               Ready               Active                                  19.03.11
```

### Step 2: Membuat sebuah overlay network
Saat ini sudah terinstall Swarm, maka dari itu saatnya membuat ***overlay*** network.
Buat sebuah overlay network baru bernama "overnet" dengan menjalankan **docker network create -d overlay overnet**.
```terminal
$ docker network create -d overlay overnet
394gqdttkvozndr0s3dpn82j1
```

Gunakan perintah **docker network ls** untuk verify network sudah berhasil dibuat.
```terminal
$ docker network ls
NETWORK ID          NAME                DRIVER              SCOPE
ceba66be8c2a        bridge              bridge              local
3b932b2debfa        docker_gwbridge     bridge              local
c36704107bc0        host                host                local
x5uphn6xp9t2        ingress             overlay             swarm
0f75ca36d8fe        none                null                local
394gqdttkvoz        overnet             overlay             swarm
```

"overnet" network baru sudah terlihat dibagian terkahir dari output.

Jalankan perintah **docker network ls** di terminal kedua.
```terminal
$ docker network ls
NETWORK ID          NAME                DRIVER              SCOPE
4fa25627e0ee        bridge              bridge              local
98c476dea44e        docker_gwbridge     bridge              local
8c96595b9904        host                host                local
x5uphn6xp9t2        ingress             overlay             swarm
ea057c1d928f        none                null                local
```

Notice bahwa "overnet" network tidak muncul dari output. Ini dikarenakan Docker hanya memperluas overlay network ke host jika mereka membutuhkan.
Gunakan perintah **docker network inspect <network>** untuk melihat lebih detail mengenai informasi tentang "overnet" network. jalankan di terminal pertama.
```terminal
$ docker network inspect overnet
[
    {
        "Name": "overnet",
        "Id": "394gqdttkvozndr0s3dpn82j1",
        "Created": "2020-12-03T09:36:52.056980164Z",
        "Scope": "swarm",
        "Driver": "overlay",
        "EnableIPv6": false,
        "IPAM": {
            "Driver": "default",
            "Options": null,
            "Config": [
                {
                    "Subnet": "10.0.1.0/24",
                    "Gateway": "10.0.1.1"
                }
            ]
        },
        "Internal": false,
        "Attachable": false,
        "Ingress": false,
        "ConfigFrom": {
            "Network": ""
        },
        "ConfigOnly": false,
        "Containers": null,
        "Options": {
            "com.docker.network.driver.overlay.vxlanid_list": "4097"
        },
        "Labels": null
    }
]
```

### Step 3: Membuat sebuah service
Saat ini sudah terinstall Swarm dan overlay network, saatnya membuat sebuah service yang memakai network.
Jalankan program berikut di terminal pertama untuk membuat service baru dengan nama *myservice* di *overnet* network dengan dua tasks/replika.
```terminal
$ docker service create --name myservice \
> --network overnet \
> --replicas 2 \
> ubuntu sleep infinity
ur4ztz67jtmqzqqyspus3ua4k
overall progress: 2 out of 2 tasks
1/2: running
2/2: running
verify: Service converged
```

Verify bahwa service dan kedua replika sudah up dengan menjalankan **docker service ls**.
```terminal
$ docker service ls
ID                  NAME                MODE                REPLICAS     IMAGE               PORTS
ur4ztz67jtmq        myservice           replicated          2/2     ubuntu:latest
```
**2/2** di dalam kolom **REPLICAS** menunjukkan bawa kedua task sudah up dan running.

Verifi bawa single task (replika) sudah running di keuda nodes dalam swarm dengan menjalankan **docker service ps myservice**.
```terminal
$ docker service ps myservice
ID                  NAME                IMAGE               NODE     DESIRED STATE       CURRENT STATE                ERROR               PORTS
663wqdkux5w7        myservice.1         ubuntu:latest       node2     Running             Running about a minute ago
si2ine2hcuoj        myservice.2         ubuntu:latest       node1     Running             Running about a minute ago
```
Sekarang, bahwa node kedua sudah running task di "overnet" network, ini akan dapat ditampilkan. Jalankan perintah **docker network ls** di terminal kedua.
```terminal
$ docker network ls
NETWORK ID          NAME                DRIVER              SCOPE
4fa25627e0ee        bridge              bridge              local
98c476dea44e        docker_gwbridge     bridge              local
8c96595b9904        host                host                local
x5uphn6xp9t2        ingress             overlay             swarm
ea057c1d928f        none                null                local
394gqdttkvoz        overnet             overlay             swarm
```

Jika ingin melihat informasi lebih detail dari "overnet", dapat menjalankan perintah **docker network inspect overnet** dari terminal kedua.
```terminal
$ docker network inspect overnet
[
    {
        "Name": "overnet",
        "Id": "394gqdttkvozndr0s3dpn82j1",
        "Created": "2020-12-03T09:39:39.321971352Z",
        "Scope": "swarm",
        "Driver": "overlay",
        "EnableIPv6": false,
        "IPAM": {
            "Driver": "default",
            "Options": null,
            "Config": [
                {
                    "Subnet": "10.0.1.0/24",
                    "Gateway": "10.0.1.1"
                }
            ]
        },
        "Internal": false,
        "Attachable": false,
        "Ingress": false,
        "ConfigFrom": {
            "Network": ""
        },
        "ConfigOnly": false,
        "Containers": {
            "537653ec128dd54020be4e4f817a857578a30ffb1c1fc57bf93779c366f729b9": {
                "Name": "myservice.1.663wqdkux5w7q9h9gl1kndve8",
                "EndpointID": "49f750e170d3552a2d0c09335e89ba2739e6561c939bf49558f21adfb91dc24e",
                "MacAddress": "02:42:0a:00:01:03",
                "IPv4Address": "10.0.1.3/24",
                "IPv6Address": ""
            },
            "lb-overnet": {
                "Name": "overnet-endpoint",
                "EndpointID": "134cf3865ba91192c358eee66f68c199f268b34442749d6a62647d997fc0139b",
                "MacAddress": "02:42:0a:00:01:05",
                "IPv4Address": "10.0.1.5/24",
                "IPv6Address": ""
            }
        },
        "Options": {
            "com.docker.network.driver.overlay.vxlanid_list": "4097"
        },
        "Labels": {},
        "Peers": [
            {
                "Name": "415ce069ce6a",
                "IP": "192.168.0.17"
            },
            {
                "Name": "aed335f96081",
                "IP": "192.168.0.18"
            }
        ]
    }
]
```

## Step 4: Uji network
Untuk melengkapi step ini, dibutuhkan IP address dari service yang running di ***node2*** (*10.0.1.3*).
Jalankan perintah berikut diterminal pertama.
```terminal
$ docker network inspect overnet
```

Jalankan perintah **docker ps** untuk mendapatkan ID dari service task, jadi dapat melanjutkan ke step berikutnya.
```terminal
$ docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED          STATUS              PORTS                  NAMES
b1ef2b5df7ff        ubuntu:latest       "sleep infinity"         9 minutesago       Up 9 minutes                               myservice.2.si2ine2hcuoj4qxalh9x83opd
bae5af290920        nginx               "/docker-entrypoint.…"   17 minutes ago      Up 17 minutes       0.0.0.0:8080->80/tcp   web1
```

Masuk ke serive task, dengan perintah **docker exec -it <CONTAINER ID> /bin/bash.**
```terminal
$ docker exec -it b1ef2b5df7ff /bin/bash
root@b1ef2b5df7ff:/#
```

Install program ping dan ping service task yang running di node ke dua, yang memiliki IP address *10.0.1.3*.
```terminal
root@b1ef2b5df7ff:/# apt-get update && apt-get install -y iputils-ping
Get:1 http://security.ubuntu.com/ubuntu focal-security InRelease [109 kB]
Get:2 http://archive.ubuntu.com/ubuntu focal InRelease [265 kB]
Get:3 http://archive.ubuntu.com/ubuntu focal-updates InRelease [114 kB]
Get:4 http://security.ubuntu.com/ubuntu focal-security/main amd64 Packages[489 kB]
<Snip>	
```

Sekarang, ping *10.0.1.3*
```terminal
root@b1ef2b5df7ff:/# ping -c5 10.0.1.3
PING 10.0.1.3 (10.0.1.3) 56(84) bytes of data.
64 bytes from 10.0.1.3: icmp_seq=1 ttl=64 time=0.350 ms
64 bytes from 10.0.1.3: icmp_seq=2 ttl=64 time=0.187 ms
64 bytes from 10.0.1.3: icmp_seq=3 ttl=64 time=0.135 ms
64 bytes from 10.0.1.3: icmp_seq=4 ttl=64 time=0.179 ms
64 bytes from 10.0.1.3: icmp_seq=5 ttl=64 time=0.182 ms

--- 10.0.1.3 ping statistics ---
5 packets transmitted, 5 received, 0% packet loss, time 4000ms
rtt min/avg/max/mdev = 0.135/0.206/0.350/0.074 ms
root@b1ef2b5df7ff:/#
```

Output diatas menampilkan bahwa kedua task dari service **myservice** berada di overlay network yang sama dengan memutar kedua node dan mereka dapat menggunakan network untuk komunikasi.

## Step 5: Uji service discovery
Sekarang, kita sudah memiliki service yang berjalan menggunakan overlay network, saatnya mempelajari service.
Pastikan masih berada di dalam container, kemudian jalankan perintah **cat /etc/resolv.conf**
```terminal
root@b1ef2b5df7ff:/# cat /etc/resolv.conf
search 51ur3jppi0eupdptvsj42kdvgc.bx.internal.cloudapp.net
nameserver 127.0.0.11
options ndots:0
root@b1ef2b5df7ff:/#
```
>The value that we are interested in is the nameserver 127.0.0.11. This value sends all DNS queries from the container to an embedded DNS resolver running inside the container listening on 127.0.0.11:53. All Docker container run an embedded DNS server at this address.

Coba ping nama "myservice"  dari container dengan menjalankan **ping -c5 myservice**.
```terminal
root@b1ef2b5df7ff:/# ping -c5 myservice
PING myservice (10.0.1.2) 56(84) bytes of data.
64 bytes from 10.0.1.2 (10.0.1.2): icmp_seq=1 ttl=64 time=0.114 ms
64 bytes from 10.0.1.2 (10.0.1.2): icmp_seq=2 ttl=64 time=0.063 ms
64 bytes from 10.0.1.2 (10.0.1.2): icmp_seq=3 ttl=64 time=0.073 ms
64 bytes from 10.0.1.2 (10.0.1.2): icmp_seq=4 ttl=64 time=0.076 ms
64 bytes from 10.0.1.2 (10.0.1.2): icmp_seq=5 ttl=64 time=0.073 ms

--- myservice ping statistics ---
5 packets transmitted, 5 received, 0% packet loss, time 4005ms
rtt min/avg/max/mdev = 0.063/0.079/0.114/0.017 ms
root@b1ef2b5df7ff:/#
```

Outputnya sudah jelas menampilkan bahwa container dapat ping service ***myservice*** by nama. Notice IP addressnya adalah *10.0.1.2*. Di step step berikutnya, akan mem-verify bahwa address tersebut adalah virtual IP (VIP) yang ditugaskan ke service ***myservice***.

Jalankan **exit** untuk keluar dari **exec**. Kembali ke shell prompt Docker host.
```terminal
root@b1ef2b5df7ff:/# exit
exit
```

Inspect konfigurasi dari "myservice" dengan menjalankan **docker service inspect myservice**. Mari verify bahwa VIP sama dengan IP address pada perintah sebelumnya.
```terminal
$ docker service inspect myservice
[
    {
        "ID": "ur4ztz67jtmqzqqyspus3ua4k",
        "Version": {
            "Index": 20
        },
        "CreatedAt": "2020-12-03T09:39:39.15283517Z",
        "UpdatedAt": "2020-12-03T09:39:39.155145272Z",
        "Spec": {
            "Name": "myservice",
            "Labels": {},
            "TaskTemplate": {
                "ContainerSpec": {
                    "Image": "ubuntu:latest@sha256:c95a8e48bf88e9849f3e0f723d9f49fa12c5a00cfc6e60d2bc99d87555295e4c",
                    "Args": [
                        "sleep",
                        "infinity"
                    ],
                    "Init": false,
                    "StopGracePeriod": 10000000000,
                    "DNSConfig": {},
                    "Isolation": "default"
                },
                "Resources": {
                    "Limits": {},
                    "Reservations": {}
                },
                "RestartPolicy": {
                    "Condition": "any",
                    "Delay": 5000000000,
                    "MaxAttempts": 0
                },
                "Placement": {
                    "Platforms": [
                        {
                            "Architecture": "amd64",
                            "OS": "linux"
                        },
                        {
                            "OS": "linux"
                        },
                        {
                            "Architecture": "arm64",
                            "OS": "linux"
                        },
                        {
                            "Architecture": "ppc64le",
                            "OS": "linux"
                        },
                        {
                            "Architecture": "s390x",
                            "OS": "linux"
                        }
                    ]
                },
                "Networks": [
                    {
                        "Target": "394gqdttkvozndr0s3dpn82j1"
                    }
                ],
                "ForceUpdate": 0,
                "Runtime": "container"
            },
            "Mode": {
                "Replicated": {
                    "Replicas": 2
                }
            },
            "UpdateConfig": {
                "Parallelism": 1,
                "FailureAction": "pause",
                "Monitor": 5000000000,
                "MaxFailureRatio": 0,
                "Order": "stop-first"
            },
            "RollbackConfig": {
                "Parallelism": 1,
                "FailureAction": "pause",
                "Monitor": 5000000000,
                "MaxFailureRatio": 0,
                "Order": "stop-first"
            },
            "EndpointSpec": {
                "Mode": "vip"
            }
        },
        "Endpoint": {
            "Spec": {
                "Mode": "vip"
            },
            "VirtualIPs": [
                {
                    "NetworkID": "394gqdttkvozndr0s3dpn82j1",
                    "Addr": "10.0.1.2/24"
                }
            ]
        }
    }
]
```

Lihat pada bagian bawah output, terdapat VIP yang sama dengan "myservice".

Jalankan sesi **docker exec** di container yang berada di node2, kemudian jalankan perintah **ping -c5 service** maka akan mendapat respon VIP yang sama.
```terminal
root@537653ec128d:/# ping -c5 myservice
PING myservice (10.0.1.2) 56(84) bytes of data.
64 bytes from 10.0.1.2 (10.0.1.2): icmp_seq=1 ttl=64 time=0.144 ms
64 bytes from 10.0.1.2 (10.0.1.2): icmp_seq=2 ttl=64 time=0.067 ms
64 bytes from 10.0.1.2 (10.0.1.2): icmp_seq=3 ttl=64 time=0.074 ms
64 bytes from 10.0.1.2 (10.0.1.2): icmp_seq=4 ttl=64 time=0.097 ms
64 bytes from 10.0.1.2 (10.0.1.2): icmp_seq=5 ttl=64 time=0.088 ms

--- myservice ping statistics ---
5 packets transmitted, 5 received, 0% packet loss, time 4003ms
rtt min/avg/max/mdev = 0.067/0.094/0.144/0.027 ms
root@537653ec128d:/#
```

## Membersihkan
Praktik dasar bagaimana Docker network bekerja sudah selesai. Mari bersihkan service yang sudah dibuat, container dan kemudian disable Swarm.

jalankan perintah **docker service rm myservice** untuk menghapus service bernama *myservice*
```terminal
$ docker service rm myservice
myservice
```

Jalankan perintah **docker ps** untuk melihat daftar container yang running.
```terminal
$ docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED          STATUS              PORTS                  NAMES
b1ef2b5df7ff        ubuntu:latest       "sleep infinity"         29 minutes ago      Up 29 minutes                              myservice.2.si2ine2hcuoj4qxalh9x83opd
bae5af290920        nginx               "/docker-entrypoint.…"   37 minutes ago      Up 37 minutes       0.0.0.0:8080->80/tcp   web1
```
Jalankan perintah **docker kill <CONTAINER ID ...>** untuk menghentikan container ubuntu dan nginx.
```terminal
$ docker kill b1ef2b5df7ff bae5af290920
b1ef2b5df7ff bae5af290920

```

Akhirnya, mari hapus node1 dan node2 dari Swarm. Dapat menjalankan perintah **docker swarm leave --force** 
Jalankan perintah tersebut di node1
```terminal
$ docker swarm leave --force
Node left the swarm.
```

Jalankan perintah tersebut di node2
```terminal
$ docker swarm leave --force
Node left the swarm.
```

#### PRAKTIK SUDAH SELESAI