---
layout: post
title: Setup LaTeX PDF build using Travis CI
description: Setup LaTeX PDF build using Travis CI
---

## Objective

Setup [Travis CI](https://travis-ci.org) continuous integration and deployment service to build PDF from LaTeX document.

> This post presumes that, `git`, `ruby` and `gem` are already installed.

## 1. Clone `harshjv/travis-ci-latex-pdf`

{% highlight bash %}
git clone https://github.com/harshjv/travis-ci-latex-pdf.git
{% endhighlight %}


## 2. Add tex files

Add your **tex** files to `tex` folder of your repository.


## 3. Configure Travis-CI


### 3.1. Setup Github repo

* If you have forked this repo, then directly go to **Settings** option, otherwise, first create a new repository on Github and then, then go to **Settings** option of your repository.

* Click on **Webhooks & Services** and then **Add service**

* Select **Travis CI**

* Add your **Travis CI** username and **Token**

* Add service


### 3.2. Setup Travis CI

* Go to [Travis CI](https://travis-ci.org)

* Toggle on your repository


### 3.3. Install Travis Command-line Tool


To configure Travis build to deploy generated PDF to Github releases, we have to get Github OAuth Token. To get it and securely embed it into `.travis.yml` file, we have to install **Travis Command-line Tool**

{% highlight bash %}
gem install travis -v 1.7.5 --no-rdoc --no-ri
travis setup releases
{% endhighlight %}

Provide your Github username and password, to generate token and encrypt it on the go. This will also add it to your `.travis.yml` file.


### 3.4. Configure `.travis.yml`

To deploy our file before get removed by Travis on `clean`, we have to disable it. Modify `.travis.yml` content according to following code.

{% highlight yaml %}
script:
- mkdir _build
- pdflatex -output-directory _build tex/your_file_1.tex
- pdflatex -output-directory _build tex/your_file_2.tex
deploy:
  provider: releases
  api_key:
    secure: [YOUR KEY]
  file:
  - _build/your_file_1.pdf
  - _build/your_file_2.pdf
  skip_cleanup: true
  on:
    tags: true
{% endhighlight %}

## 4. Git commit, push and tag

In order to build PDF, we must commit changes and tag it to a version/release. Then push it to remote Github repository.

{% highlight bash %}
git add . --all
git commit -m "Message"
git tag draft-1
git push -u origin master --tags
{% endhighlight %}

## 5. Hooray

After a successful build, you can see your PDF files available at `releases` under your Github repository.
