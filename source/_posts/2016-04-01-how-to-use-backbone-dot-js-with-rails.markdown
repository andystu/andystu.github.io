---
layout: post
title: "how to use backbone.js with rails"
date: 2016-04-01 14:43:33 +0800
comments: true
categories: 
---
- Here I create a simple rails project (todo-list) for demostrate how to use backbon.js with rails.

- preparation.
```
$ rails new backbone-todo -T
# add backbone.js gem to Gemfile
$ echo "gem 'backbone-on-rails'" >> Gemfile
$ bundle
# generate scaffold for todo tasks
$ rails g scaffold task name complete:boolean
$ rake db:migrate
$ rm -rf app/views/tasks
$ touch app/views/tasks/index.html.erb
```

- install backbone.js into project
```
$ rails g backbone:install
```

- generate backbone scaffold for tasks
```
$ rails g backbone:scaffold task
```

- done.
