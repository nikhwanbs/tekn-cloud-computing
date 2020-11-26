# Docker for Beginners - Linux
## Task 0: Prerequisites

Clone the Lab’s GitHub Repo

```console
[node1] (local) root@192.168.0.28 ~
$     git clone https://github.com/dockersamples/linux_tweet_app
Cloning into 'linux_tweet_app'...
remote: Enumerating objects: 14, done.
remote: Total 14 (delta 0), reused 0 (delta 0), pack-reused 14
Receiving objects: 100% (14/14), 10.76 KiB | 10.76 MiB/s, done.
Resolving deltas: 100% (5/5), done.
```

## Task 1: Run some simple Docker containers
### Run a single task in an Alpine Linux container
In this step we’re going to start a new container and tell it to run the hostname command. The container will start, execute the hostname command, then exit.

1. Run the following command in your Linux console.

    ```console
    $  docker container run alpine hostname
    Unable to find image 'alpine:latest' locally
    latest: Pulling from library/alpine
    188c0c94c7c5: Pull complete
    Digest: sha256:c0e9560cda118f9ec63ddefb4a173a2b2a0347082d7dff7dc14272e7841a5b5a
    Status: Downloaded newer image for alpine:latest
    c523ee190124
    ```

2. Docker keeps a container running as long as the process it started inside the container is still running. In this case the hostname process exits as soon as the output is written. This means the container stops. However, Docker doesn’t delete resources by default, so the container still exists in the Exited state.

List all containers.
    ```console
    $  docker container ls --all
    CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                     PORTS               NAMES
    c523ee190124        alpine              "hostname"          2 minutes ago       Exited (0) 2 minutes ago                       cool_goodall
    ```
### Run an interactive Ubuntu container
You can run a container based on a different version of Linux than is running on your Docker host.

In the next example, we are going to run an Ubuntu Linux container on top of an Alpine Linux Docker host (Play With Docker uses Alpine Linux for its nodes).
1. Run a Docker container and access its shell.
    ```console
    $  docker container run --interactive --tty --rm ubuntu bash
    Unable to find image 'ubuntu:latest' locally
    latest: Pulling from library/ubuntu
    da7391352a9b: Pull complete
    14428a6d4bcd: Pull complete
    2c2d948710f2: Pull complete
    Digest: sha256:c95a8e48bf88e9849f3e0f723d9f49fa12c5a00cfc6e60d2bc99d87555295e4c
    Status: Downloaded newer image for ubuntu:latest
    root@8e7e8f6ab89f:/#
    ```

2. Run the following commands in the container.
    ls / will list the contents of the root director in the container, ps aux will show running processes in the container, cat /etc/issue will show which Linux distro the container is running.
    ```console
    root@8e7e8f6ab89f:/# ls /
    bin   dev  home  lib32  libx32  mnt  proc  run   srv  tmp  var
    boot  etc  lib   lib64  media   opt  root  sbin  sys  usr
    root@8e7e8f6ab89f:/# ps aux
    USER        PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
    root          1  0.3  0.0   4108  2252 pts/0    Ss   13:11   0:00 bash
    root          9  0.0  0.0   5896  2804 pts/0    R+   13:13   0:00 ps aux
    root@8e7e8f6ab89f:/# cat /etc/issue
    Ubuntu 20.04.1 LTS \n \l
    ```

3. Type exit to leave the shell session. This will terminate the bash process, causing the container to exit.
    ```console
    root@8e7e8f6ab89f:/#  exit
    exit
    ```

4. For fun, let’s check the version of our host VM.
    ```console
    $  cat /etc/issue
    Welcome to Alpine Linux 3.12
    Kernel \r on an \m (\l)
    ```

### Run a background MySQL container
Background containers are how you’ll run most applications. Here’s a simple example using MySQL.

1. Run a new MySQL container with the following command.
    ```console
    $  docker container run \
    >  --detach \
    >  --name mydb \
    >  -e MYSQL_ROOT_PASSWORD=my-secret-pw \
    >  mysql:latest
    Unable to find image 'mysql:latest' locally
    latest: Pulling from library/mysql
    852e50cd189d: Pull complete
    29969ddb0ffb: Pull complete
    a43f41a44c48: Pull complete
    5cdd802543a3: Pull complete
    b79b040de953: Pull complete
    938c64119969: Pull complete
    7689ec51a0d9: Pull complete
    a880ba7c411f: Pull complete
    984f656ec6ca: Pull complete
    9f497bce458a: Pull complete
    b9940f97694b: Pull complete
    2f069358dc96: Pull complete
    Digest: sha256:4bb2e81a40e9d0d59bd8e3dc2ba5e1f2197696f6de39a91e90798dd27299b093
    Status: Downloaded newer image for mysql:latest
    93660354a88d82e0f28c3e50e945d9fc239343b2b1d9cd2a9a39a91add16212c
    ```
    As long as the MySQL process is running, Docker will keep the container running in the background.

2. List the running containers.
    ```console
    $  docker container ls
    CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS        PORTS                 NAMES
    93660354a88d        mysql:latest        "docker-entrypoint.s…"   2 minutes ago       Up 2 minutes        3306/tcp, 33060/tcp   mydb
    ```

3. You can check what’s happening in your containers by using a couple of built-in Docker commands: docker container logs and docker container top.
    ```console
    <output truncated>
   2017-09-29T16:02:58.605004Z 0 [Note] Executing 'SELECT * FROM INFORMATION_SCHEMA.TABLES;' to get a list of tables using the deprecated partition engine. You may use the startup option '--disable-partition-engine-check' to skip this check.
   2017-09-29T16:02:58.605026Z 0 [Note] Beginning of list of non-natively partitioned tables
   2017-09-29T16:02:58.616575Z 0 [Note] End of list of non-natively partitioned tables
    ```

    Let’s look at the processes running inside the container.
    ```console
    $    docker container top mydb
    PID                 USER                TIME                COMMAND
    2023                999                 0:00                {docker-entrypoi} /bin/bash/usr/local/bin/docker-entrypoint.sh mysqld
    2235                999                 0:05                mysqld --daemonize --skip-networking --socket=/var/run/mysqld/mysqld.sock
    2339                999                 0:00                mysql_tzinfo_to_sql /usr/share/zoneinfo
    2340                999                 0:00                sed s/Local time zone must be set--see zic manual page/FCTY/
    2351                999                 0:00                {docker-entrypoi} /bin/bash/usr/local/bin/docker-entrypoint.sh mysqld
    2353                999                 0:00                mysql --defaults-extra-file=/dev/fd/63 --protocol=socket -uroot -hlocalhost --socket=/var/run/mysqld/mysqld.sock --database=mysql
    ```

4. List the MySQL version using docker container exec
    docker container exec allows you to run a command inside a container. In this example, we’ll use docker container exec to run the command-line equivalent of mysql --user=root --password=$MYSQL_ROOT_PASSWORD --version inside our MySQL container.
    ```console
    docker exec -it mydb \
    mysql --user=root --password=$MYSQL_ROOT_PASSWORD --version
    mysql: [Warning] Using a password on the command line interface can be insecure.
    mysql  Ver 14.14 Distrib 5.7.19, for Linux (x86_64) using  EditLine wrapper
    ```

5. You can also use docker container exec to connect to a new shell process inside an already-running container. Executing the command below will give you an interactive shell (sh) inside your MySQL container.
    ```console
    $  docker exec -it mydb sh
    #
    ```

6. Let’s check the version number by running the same command again, only this time from within the new shell session in the container.
    ```console
    #  mysql --user=root --password=$MYSQL_ROOT_PASSWORD --version
    mysql: [Warning] Using a password on the command line interface can be insecure.
    mysql  Ver 8.0.22 for Linux on x86_64 (MySQL Community Server - GPL)
    ```

7. Type exit to leave the interactive shell session.
    ```console
    #  exit
    ```

## Task 2: Package and run a custom app using Docker