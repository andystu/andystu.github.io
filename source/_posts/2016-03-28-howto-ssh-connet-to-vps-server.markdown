---
layout: post
title: "how to setup for ssh connet to vps server"
date: 2016-03-28 22:03:12 +0800
comments: true
categories: ssh vps
---
- use ssh-keygen to generate keys (public/private)
```
$ ssh-keygen -t rsa # -t refers to key type, here we use rsa
```
- The keys were generated under ~./ssh folder
- copy public key to vps server
```
$ cd ~/.ssh
$ cat id_rsa.pub
```
- Sign in vps server
- Before we use ssh to connect vps, we have to activate ssh service for ssh connection.
```
$ sudo apt-get install openssh-server # make sure your server install openssh service (here we use ubuntu)
$ sudo pico /etc/ssh/sshd_config # edit sshd setting
# Port 12141 # do not forget to change port for security reason
# PermitRootLogin yes --> PermitRootLogin no # for disable root ssh login 
$ sudo /etc/init.d/ssh restart # restart sshd
# or use service tool
$ service ssh restart
```
- put your public key to vps
```
$ mkdir .ssh
$ touch authorized_keys
# then copy your local ~/.ssh/id_rsa.pub to authorized_keys by any text editor (vi,pico...etc)
```
- On Mac, we can use 'ssh-copy-id' to install our identity.pub in a remote machine's authorized_keys.
- Now, you can ssh to connect your vps directly without typing any password.
- enjoy.