---
layout: post
title: Document Building & Versioning with TeX Document, Git, Continuous Integration & Dropbox
description: Document Building & Versioning with TeX Document, Git, Continuous Integration & Dropbox
keywords: "latex, pdf, build, travis, travis ci, continuous integration, continuous deployment, git, linux, ubuntu, osx, os x, mac, windows"
---

## Objective

Use Git, Continuous Integration & Dropbox to build tex documents and upload with proper branch structure & version to Dropbox.


## Workflow

![Workflow](/assets/images/posts/document-building-versioning-with-tex-document-git-continuous-integration-dropbox/workflow.png "Workflow")


## 1. Requirements

We need;

1. Git service
  - Bitbucket
  - Github

2. Continuous Integration and Deployment service
  - Semaphore
  - Travis

3. Dropbox account


## 1.1. Dropbox Uploader

> Use of **App Folder only** as access level is recommended.

To upload generated PDF to [Dropbox](https://www.dropbox.com), we will use [Dropbox Uploader](https://github.com/andreafabrizi/Dropbox-Uploader).

1. Follow Dropbox-Uploader's [README.md](https://github.com/andreafabrizi/Dropbox-Uploader/blob/master/README.md) and configure it on your local machine.
2. Verify that you have `~/.dropbox_uploader` file on your local machine. We will use this file later.


## 2. Prepare Git repository

> See [best practices for writing Dockerfiles](https://docs.docker.com/articles/dockerfile_best-practices/).

Initialise **Git** `git init` and use following directory structure for your git repository.

{% highlight dockerfile %}
.
├── docker
|   ├── Dockerfile
├── document.tex
{% endhighlight %}

Now for `docker/Dockerfile`, we will use [harshjv/texlive-2015](https://hub.docker.com/r/harshjv/texlive-2015) docker image. This image contains [Tex Live 2015](https://www.tug.org/texlive/).


### 2.1. Dockerfile

{% highlight dockerfile %}
FROM harshjv/texlive-2015
RUN tlmgr update --all
{% endhighlight %}

This will build docker image with latest packages for building tex documents.


## 3. Add your tex documents

Add some **tex** files to your repository.


## 4. Configure Git service

For Webhooks/Services, we need to configure Git services as follows;

### 4.1. For Bitbucket

No configuration needed as of now.

### 4.2. For Github

1. Go to Settings -> Webhooks & services -> Services
2. Select **Travis CI**


## 5. Configure Continuous Integration service

### 5.1. For Semaphore

1. Do an initial commit and push to remote branch (if empty remote repository), because it requires at least one remote branch
2. Go to [SemaphoreCI](https://semaphoreci.com/)
3. Add new project
4. Select your Git service
5. Select your repository
6. Select branch (e.g. master)
7. Select your account

After these initial steps, it's time to configure build and deployment.


#### 5.1.1. Setup Thread

{% highlight bash %}
sudo docker build -t texlive docker
curl "https://raw.githubusercontent.com/andreafabrizi/Dropbox-Uploader/master/dropbox_uploader.sh" -o dropbox_uploader.sh
chmod +x dropbox_uploader.sh
{% endhighlight %}

This setup script builds `docker/Dockerfile` with latest tex packages and fetches Dropbox Uploader script.

#### 5.1.2. Build Thread

{% highlight bash %}
sudo docker run -it -v ${SEMAPHORE_PROJECT_DIR}:/var/texlive texlive sh -c "pdflatex document.lex"
./dropbox_uploader.sh upload document.pdf ${BRANCH_NAME}/document-latest.pdf
./dropbox_uploader.sh upload document.pdf ${BRANCH_NAME}/document-v${SEMAPHORE_BUILD_NUMBER}.pdf
{% endhighlight %}

This build script compiles `document.lex` LeX document and builds `document.pdf` PDF. Then, using Dropbox Uploader, versioned PDF files are stored in branch's individual folder.

> For `document.lex` in `master` branch, `document.pdf` will be uploaded as;
>
> * `Dropbox/[YOUR_APP_FOLDER]/master/document-latest.pdf`
> * `Dropbox/[YOUR_APP_FOLDER]/master/document-v[BUILD_NUMBER].pdf`

Any successive commit will overwrite `document-latest.pdf` and will create a new `document-v[BUILD_NUMBER].pdf` file.

#### 5.1.3. Configuration Files

1. Visit Project Settings -> Configuration Files
2. Add configuration file
3. Add `.dropbox_uploader` to File path
4. (Optional) Check encryption
5. Paste content of `~/.dropbox_uploader`
   * `pbcopy ~/.dropbox_uploader` (OSX)


### 5.2. For Travis

Script for setup and building remains same. Put these script into individual files and create a `.travis.yml` file. This isn't covered here for now. Refer [this post](/blog/setup-latex-pdf-build-using-travis-ci/) for relevant instructions.

## 4. Git commit and push

It's time to

{% highlight bash %}
git add .
git commit -m "Add some details"
git push origin master
{% endhighlight %}

## 5. Hooray

> **Tip**
>
> If you want to share only the latest PDF after changes,
> use URL shortener service like [Bit.ly](http://bit.ly) to point to this latest document
> after getting sharing link from Dropbox.
>
> Why? Because, for each branch folder, `[DOCUMENT_NAME]-latest.pdf` will always contains latest PDF.

After a successful build, generated PDF files will be available at `Dropbox/[YOUR_APP_FOLDER]/master` folder.
