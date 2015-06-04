---
layout: post
title: "Laravel 5 with dockerized Gulp, PHP-FPM, MySQL and nginx"
description: "Laravel 5 with dockerized Gulp, PHP-FPM, MySQL and nginx"
---

## Objective

Setup Laravel 5 with *dockerized* Gulp, PHP-FPM, MySQL and nginx using docker orchestration tool, *docker-compose*.

> This post presumes that `docker` & `docker-compose` are already installed on your system.


## 1. Clone repository

{% highlight bash %}
git clone https://github.com/harshjv/docker-laravel.git
{% endhighlight %}


## 2. Run services

{% highlight bash %}
docker-compose up
{% endhighlight %}


## 3. Download Composer

{% highlight bash %}
docker-compose run --rm phpnginx curl -O https://getcomposer.org/installer
docker-compose run --rm phpnginx php installer
{% endhighlight %}


## 4. Install Laravel 5 using Composer

{% highlight bash %}
docker-compose run --rm phpnginx php composer.phar create-project laravel/laravel src --prefer-dist
{% endhighlight %}


## 5. Permissions

Laravel 5 requires `vendor` and `storage` and directories within them to have write permission by web server.

{% highlight bash %}
chmod -R 777 vendor storage
{% endhighlight %}

> If you are running Docker using boot2docker, check this post to [configure NFS with boot2docker and OS X]({% post_url 2015-03-21-configure-nfs-with-boot2docker-and-os-x %}) in order to fix write permissions.


## 6. Hooray

Visit [http://localhost](http://localhost "http://localhost") to view the project.
