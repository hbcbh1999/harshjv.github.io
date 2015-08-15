---
layout: post
title: Yes, source executes script differently, I mean, in a different shell
description: source command executes script in a different shell
keywords: "shell, linux, command, unix, script execution, script"
---

## Objective

See how differently shell script is executed using `source`.


## 1. Basic

`source` command executes the provided script *(executable permission is **not mandatory**)* in the **current** shell environment, while `./` executes the provided **executable** script in a **new** shell.

> `source` command do have a synonym `. filename`.

To make it more clear, have a look at the following script, which sets the alias, using a shell script file named, `make_alias`.


## 2. `make_alias` file

{% highlight bash %}
#! /bin/bash
alias myproject='cd ~/Documents/Projects/2015/NewProject'
{% endhighlight %}


## 3. Two options

Now we have two choices to execute this script. But with *only* one option, the  desired alias for your ***current*** shell can be created among these two options.


### 3.1. Option 1 `./make_alias`

Make script executable first.

{% highlight bash %}
chmod +x make_alias
{% endhighlight %}


#### 3.1.1. Execute

{% highlight bash %}
./make_alias
{% endhighlight %}


#### 3.1.2. Verify

{% highlight bash %}
alias
{% endhighlight %}


#### 3.1.3. Output

***no alias for myproject***

**Whoops!**, alias is gone with the new shell.


Now, let's go with the second option.


## 3.2. Option 2 `source make_alias`

> No need to make script executable while using `source`.


#### 3.2.1. Execute

{% highlight bash %}
source make_alias
{% endhighlight %}

*or*

{% highlight bash %}
. make_alias
{% endhighlight %}


#### 3.2.2. Verify

{% highlight bash %}
alias
{% endhighlight %}


#### 3.2.3. Output

{% highlight bash %}
alias myproject='cd ~/Documents/Projects/2015/NewProject'
{% endhighlight %}


**Yeah**, alias is set now.


## 4. Reference

* [My answer on SU](http://superuser.com/a/894748/432100)
