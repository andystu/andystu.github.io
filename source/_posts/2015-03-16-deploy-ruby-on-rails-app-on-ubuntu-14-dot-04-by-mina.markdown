---
layout: post
title: "deploy ruby on rails app on ubuntu 14.04 by mina"
date: 2015-03-16 22:44:48 +0800
comments: true
categories: [rails, deploy, ubuntu, passenger, nginx, mina]
---
- Mina is fast and easy deploy tool for ruby on rails app (especially faster than capistrano). This note shows how to deploy ruby on rails app by mina.

- Start up an ubuntu server (here we use Ubuntu 14.04 LTS x64 on vultr cloud server)

- ssh to login your server
```
$ ssh username@123.123.123.123
```

<!-- more -->

- create a new user for later deployment work, better use the same name as your local development user name
```
$ sudo adduser new_user
$ sudo adduser new_user sudo
$ su new_user
```

- We're going to exploit ssh-copy-id to setup SSH connection for saving our time.

```
$ brew install ssh-copy-id # on Mac we use brew
$ ssh-copy-id new_user@123.123.123.123
```

- Next, we're going to install Ruby and its bundler.
```
$ curl -L https://get.rvm.io | bash -s stable
$ source ~/.rvm/scripts/rvm
$ rvm install 2.2.0
$ rvm use 2.2.0 --default
$ echo "gem: --no-ri --no-rdoc" > ~/.gemrc
$ gem install bundler
```

- Installing nginx and passenger [A guide to setting up a Ruby on Rails production environment](https://gorails.com/deploy/ubuntu/14.04)

{% codeblock %}
# Install Phusion's PGP key to verify packages
$ gpg --keyserver keyserver.ubuntu.com --recv-keys 561F9B9CAC40B2F7
$ gpg --armor --export 561F9B9CAC40B2F7 | sudo apt-key add -

# Add HTTPS support to APT
$ sudo apt-get install apt-transport-https

# Add the passenger repository
$ sudo sh -c "echo 'deb https://oss-binaries.phusionpassenger.com/apt/passenger trusty main' >> /etc/apt/sources.list.d/passenger.list"
$ sudo chown root: /etc/apt/sources.list.d/passenger.list
$ sudo chmod 600 /etc/apt/sources.list.d/passenger.list
$ sudo apt-get update

# Install nginx and passenger
$ sudo apt-get install nginx-full passenger

# start service
$ sudo service nginx start
{% endcodeblock %}

- setup nginx
```
$ sudo nano /etc/nginx/nginx.conf
```

- find lines below and uncomment them.
{% codeblock %}
##
# Phusion Passenger
##
# Uncomment it if you installed ruby-passenger or ruby-passenger-enterprise
##

passenger_root /usr/lib/ruby/vendor_ruby/phusion_passenger/locations.ini;

#passenger_ruby /home/new_user/.rbenv/shims/ruby; # If you use rbenv
passenger_ruby /home/new_user/.rvm/wrappers/ruby-2.2.0/ruby; # If use use rvm, be sure to change the version number
# passenger_ruby /usr/bin/ruby; # If you use ruby from source
{% endcodeblock %}

- installing mysql
```
$ sudo apt-get install mysql-server mysql-client libmysqlclient-dev
```

- installing locale and set it up [ref](http://sfs.chc.edu.tw/~chi/blog/index.php?load=read&id=296)
{% codeblock %}
$ sudo nano /var/lib/locales/supported.d/local # add locales you want to use
# zh_TW.UTF-8 UTF-8

$ sudo locale-gen
# regenerate locales

$ sudo nano /etc/default/locale
# set all as your preferal locale
{% endcodeblock %}

-installing nodejs for coffee script engine
```
$ sudo apt-get install nodejs
```

- installing git for pull remote git repo
```
$ sudo apt-get install git
```

- installing nginx
```
$ sudo apt-get install nginx
```

- installing imagemagick for paperclip resize image
```
$ apt-get install imagemagick
```

- installing unicorn
```
$ gem install unicorn
```

- installing [mina](http://nadarei.co/mina/setting_up_a_project.html)

{% codeblock %}
# go to rails app which your want to deploy and inialize your deploy config file

$ mina init

# login and setup your server and create folders for later deployment

$ ssh username@123.123.123.123
$ sudo mkdir -p "/var/www/demo.com" && sudo chown -R new_user "/var/www/demo.com"

$ mina setup # after tweak your mina deploy.rb file, run this.

$ mina deploy # if mina setup is allpass, run this.
{% endcodeblock %}

- `mina init` will created config/deploy.rb. after this you might want to customize your [deploy.rb file.](https://gist.github.com/jbonney/6257372)

- done.