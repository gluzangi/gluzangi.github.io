---
published: true
title: Network Services Connection And Ports
layout: post
---
NETCAT:

- Test a listening port

{% highlight ruby %}
nc -vz mail.capcomcanada.com 587
{% endhighlight %}


NETSTAT:

- List all active TCP and UDP port

{% highlight ruby %}
netstat -tupanc
{% endhighlight %}

- List all TCP ports in listening state

{% highlight ruby %}
netstat -tl
{% endhighlight %}

- List all UDP ports in listening state

{% highlight ruby %}
netstat -ul
{% endhighlight %}

- List all UNIX domain sockets in listening state

{% highlight ruby %}
 netstat -xl
{% endhighlight %}

TRACEROUTE:
{% highlight ruby %}
traceroute -T mail.capcomcanada.com -p 25
{% endhighlight %}

NMAP:

- Network Fast Discovery With Nmap

{% highlight ruby %}
nmap -A -F -T5 192.168.1.200-250
{% endhighlight %}