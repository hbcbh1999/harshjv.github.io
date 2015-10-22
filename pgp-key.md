---
layout: page
title: PGP Key
permalink: /pgp-key/
nav_index: 4
---

Email: [{{ site.author.email.htmlencode }}]({{ site.author.email.id | prepend:"mailto:" }})

Download: [key.asc](/key.asc)

{% highlight text %}
{% include_relative key.asc %}
{% endhighlight %}
