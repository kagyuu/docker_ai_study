# docker_ai_study
A docker-compose script for studying AI.

## How to use it

* Prepare
    * This docker build script copies settings of ssh-server and github-client to the container each booting.
    * So you have to setup for ssh access.
    * And setup for accessing GitHub.
    1. Create a key pair. You shold make passphrase empty.
        ```
        $ ssh-keygen -t rsa
        Generating public/private rsa key pair.
        Enter file in which to save the key (/root/.ssh/id_rsa): id_rsa.github
        Enter passphrase (empty for no passphrase): 
        Enter same passphrase again: 
        ```
    2. Upload the public key, id_rsa.github.pub, to the GitHub.
    3. Create ~/.ssh/config
        ```
        Host github github.com
        HostName github.com
        IdentityFile ~/.ssh/id_rsa.github
        User git
        ```
    * You also have to initial bash settings once, because the container mounts /var/keras-work on the host to /home/aichan on the container.
        ```
        $ sudo cp /etc/skel /var/keras-work
        $ chown 5000:5000 -R /var/keras-work
        ```

* Build
    ```
    $ docker-compose build
    ```
* Start & Stop
    ```
    $ docker-compose up -d
    $ docker-compose down
    ```
* Login
    ```
    $ ssh -p 2222 aichan@localhost
    ````
* So, we can also use remote VS-Code envionment which connect to this container by SSH connection.

## Contains

* Original Image that is based on nvidia/cuda:11.4.1-devel-ubuntu20.04
    * https://hub.docker.com/r/nvidia/cuda
    * sshd
    * git
    * python3 + pip3 + pipenv3
* postgres:13.4
    * https://hub.docker.com/_/postgres
* dpage/pgadmin4:latest
    * https://hub.docker.com/r/dpage/pgadmin4

## Local Volumes

|Host                |Container |          |
|--------------------|--------|------------|
|/var/keras-data     |keras   |/home/aichan|
|/var/pgsql-data/data|pgsql   |/var/lib/postgresql/data|
|/var/pgadmin-data   |pgadmin4|/var/lib/pgadmin|
|~/.ssh/id_rsa.pub   |keras   |/home/aichan/.ssh/authorized_keys|
|~/.ssh/id_rsa.github|keras   |/home/aichan/.ssh/id_rsa.github|
|~/.ssh/config       |keras   |/home/aichan/.ssh/config|
