---
published: true
title: Dealing with netfilter and IPTables
layout: post
---
Check the status of the Firewall:
{% highlight ruby %}
iptables -L -n -v
{% endhighlight %}

Create a Two Way Firewall:
{% highlight ruby %}
iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
{% endhighlight %}

Allow Outgoing SSH:
{% highlight ruby %}
iptables -A OUTPUT -o eth0 -p tcp --dport 22 -m state --state NEW,ESTABLISHED -j ACCEPT
iptables -A INPUT -i eth0 -p tcp --sport 22 -m state --state ESTABLISHED -j ACCEPT
{% endhighlight %}

Allow Outgoing SSH + HTTP + HTTPS:
{% highlight ruby %}
iptables -A INPUT -i eth0 -p tcp -m multiport --dports 22,80,443 -m state --state NEW,ESTABLISHED -j ACCEPT
iptables -A OUTPUT -o eth0 -p tcp -m multiport --sports 22,80,443 -m state --state ESTABLISHED -j ACCEPT
{% endhighlight %}

Simple NAT:
{% highlight ruby %}
iptables -t nat -A PREROUTING -d 10.10.20.99 -j DNAT --to-destination 10.10.14.2
iptables -t nat -A PREROUTING -p tcp -d 10.10.20.99 --dport 80 -j DNAT --to-destination 10.10.14.2
{% endhighlight %}

SNAT
{% highlight ruby %}
iptables -t nat -A POSTROUTING -s 216.13.105.98 --dport 80 -j SNAT --to-destination 54.224.49.87
iptables -t nat -A POSTROUTING -p tcp -s 209.146.166.158 --dport 80 -j SNAT --to-destination 54.224.49.87
{% endhighlight %}

DNAT
{% highlight ruby %}
iptables -t nat -A PREROUTING -d 184.106.196.252 --dport 80 -j DNAT --to-destination 54.224.49.87
iptables -t nat -A PREROUTING -p tcp -d 184.106.196.252 --dport 80 -j DNAT --to-destination 54.224.49.87
{% endhighlight %}

SAMPLE /etc/sysconfig/iptables
{% highlight ruby %}
*filter
:INPUT DROP [0:0]
:FORWARD ACCEPT [0:0]
:OUTPUT ACCEPT [0:0]

## Create a Two Way Firewall ##
-A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT

## Allow Ping Requests And UNIX loopback interface
-A INPUT -p icmp -j ACCEPT
-A INPUT -i lo -j ACCEPT

## open ssh tcp protocol on port 22 ##
-A INPUT -m state --state NEW -m tcp -p tcp --dport 22 -j ACCEPT

## open http(s) tcp protocol on port 80 ##
-A INPUT -m state --state NEW -m tcp -p tcp --dport 80 -j DROP
-A INPUT -m state --state NEW -m tcp -p tcp --dport 443 -j DROP

## open dns tcp/udp protocol on port 53 ##
-A INPUT -m state --state NEW -m udp -p udp --dport 53 -j ACCEPT
-A INPUT -m state --state NEW -m tcp -p tcp --dport 53 -j ACCEPT

## open ntp tcp/udp protocol on port 123 ##
-A INPUT -m state --state NEW -m udp -p udp --dport 123 -j ACCEPT
-A INPUT -m state --state NEW -m tcp -p tcp --dport 123 -j ACCEPT

## open snmp service tcp/udp protocol on port 161 ##
-A INPUT -m state --state NEW -m udp -p udp --dport 161 -j ACCEPT
-A INPUT -m state --state NEW -m tcp -p tcp --dport 161 -j ACCEPT

## open mysql tcp protocol on port 3306  ##
-A INPUT -m state --state NEW -m tcp -p tcp --dport 3306 -j DROP

## open gmond tcp protocol on port 8649 ##
-A INPUT -m state --state NEW -m tcp -p tcp --dport 8649 -j ACCEPT

## open cassandra tcp protocol on port 7000,7001,7199,9160 ##
-A INPUT -m state --state NEW -m tcp -p tcp -m multiport --dports 7000,7001,7199,9160 -j ACCEPT

-A INPUT -j REJECT --reject-with icmp-host-prohibited
-A FORWARD -j REJECT --reject-with icmp-host-prohibited
COMMIT

*nat
:OUTPUT ACCEPT [0:0]
:PREROUTING ACCEPT [0:0]
:POSTROUTING ACCEPT [0:0]
COMMIT

*mangle
:FORWARD ACCEPT [0:0]
:INPUT ACCEPT [0:0]
:OUTPUT ACCEPT [0:0]
:PREROUTING ACCEPT [0:0]
:POSTROUTING ACCEPT [0:0]
COMMIT
# Completed on Thu Mar 12 13:22:17 2015
{% endhighlight %}