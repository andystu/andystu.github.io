---
layout: post
title: "how to use vagrant with virtualbox"
date: 2016-03-28 23:32:34 +0800
comments: true
categories: 
---
```
$ brew install caskroom/cask/brew-cask
$ brew cask install virtualbox
$ brew cask install vagrant
$ brew install ansible
```

```
$ vagrant box add hashicorp/precise64
# automatically download box file from hashicorp and put it into ~/.vagrant.d/ folder
$ vagrant init hashicorp/precise64
$ vagrant up # up your vbox
$ vagrant ssh # login your vbox
$ curl -L https://gist.github.com/gogojimmy/5523985/raw/b9d777bc380ee791c2f4534e9261b4b99289ed9f/bootstrap-chef-solo.sh | sh
```


