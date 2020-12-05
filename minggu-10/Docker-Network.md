# Docker Networking Hands-on Lab
Pada Praktik ini akan dipelajari tentang konsep Docker Networking. Akan ada beberapa contoh konsep networking, belajar tentang Bridge networking, dan Overlay networking.

## Section #1 - Networking Basics
### Step 1: The Docker Network Command
**docker network** adalah perintah utama untuk konfigurasi dan me-manage container networks. Jalankan perintah **docker network** dari terminal pertama, 
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