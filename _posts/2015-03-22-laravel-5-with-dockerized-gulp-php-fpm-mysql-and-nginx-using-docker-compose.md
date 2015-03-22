---
published: false
title: "Laravel 5 with Dockerized Gulp, PHP-FPM, MySQL and nginx using docker-compose"
description: "Laravel 5 with Dockerized Gulp, PHP-FPM, MySQL and nginx using docker-compose"
layout: post
---

## Objective

Setup Laravel 5 with Dockerized Gulp, PHP-FPM, MySQL and nginx using *docker-compose*

> This post presumes that docker & docker-compose are already installed on your system.

## Steps

### Clone repository

{% highlight bash %}
git clone https://github.com/harshjv/docker-laravel.git
{% endhighlight %}

### Run services

{% highlight bash %}
docker-composer up
{% endhighlight %}

### Download Composer

{% highlight bash %}
docker-compose run --rm phpnginx curl -O https://getcomposer.org/installer
docker-compose run --rm phpnginx php installer
{% endhighlight %}

### Install Laravel 5 using Composer

{% highlight bash %} 
docker-compose run --rm phpnginx php composer.phar create-project laravel/laravel src --prefer-dist
{% endhighlight %}

### Hooray

Visit [http://localhost](http://localhost "http://localhost") to view the project.