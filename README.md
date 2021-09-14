# docker_ai_study
A docker-compose script for studying AI.

## How to use it

* Build
```
$ docker-compose build --build-arg PASSWD=1qazse45
```
* Start & Stop
```
$ docker-compose up -d
$ docker-compose down
```
* Login
```
$ ssh -p 2222 root@localhost
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

* [TO BE DONE, I'm little tired tonight.]

## Tips

* Connect to the GitHub form this AI study environment.

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
