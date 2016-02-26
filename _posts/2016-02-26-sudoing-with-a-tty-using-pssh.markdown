---
published: true
title: sudoing with a tty using pssh 
layout: post
---
ENABLE sudo COMMAND WITH A tty USING pssh

{% highlight ruby %}
pssh -h /usr/local/etc/group/cassadb -i -l ec2-user -x '-t -t -c blowfish' 'sudo service cassandra status'
{% endhighlight %}