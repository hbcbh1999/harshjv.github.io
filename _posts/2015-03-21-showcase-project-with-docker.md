---
layout: post
title: Showcase project with Docker
description: Quick steps to run Showcase project using Docker
keywords: "showcase, showcase project, laravel, laravel 5, docker, phpfpm, php-fpm, mysql, nginx, lemp, lemp stack, installation, linux, ubuntu, osx, os x, mac, windows"
---

## Objective

Run [Showcase](https://github.com/harshjv/Showcase "Showcase") project using [Docker](http://www.docker.com "Docker").

> This post presumes that **docker** & **docker-compose** are already installed on your system.


## 1. Clone repository

{% highlight bash %}
git clone https://github.com/harshjv/Showcase.git
{% endhighlight %}


## 2. Run containers

{% highlight bash %}
cd Showcase && docker-compose up -d
{% endhighlight %}


## 3. Install project dependencies using Composer

{% highlight bash %}
docker-compose run --rm phpnginx curl -O https://getcomposer.org/installer
docker-compose run --rm phpnginx php installer
docker-compose run --rm phpnginx php composer.phar install
{% endhighlight %}


## 4. Setup database

{% highlight bash %}
docker-compose run --rm mysql mysql -hmysql --password=root -e "create database showcase;"
docker-compose run --rm phpnginx php artisan migrate --seed
{% endhighlight %}


## 5. Get departmental tokens

{% highlight bash %}
docker-compose run --rm mysql mysql -hmysql --password=root -e "use showcase; select * from departments;"
{% endhighlight %}


## 6. Hooray

Visit [http://localhost](http://localhost "http://localhost") to view the project.


## 7. Or try all-in-one script

{% highlight bash %}
curl https://gist.githubusercontent.com/harshjv/875db02e8f8d3a09090f/raw/f535ca306c2279f8f06ca2b4a6a7a64f39805bef/install.sh | bash
{% endhighlight %}
