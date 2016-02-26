---
published: true
title: Software RAID manipulations
layout: post
---
Creating Software RAID Array:
{% highlight ruby %}
mdadm --create --verbose /dev/md0 --level=linear --raid-devices=2 /dev/sdb6 /dev/sdc5
mdadm --create --verbose /dev/md0 --level=stripe --raid-devices=2 /dev/sdb6 /dev/sdc5

mdadm --create --verbose /dev/md0 --level=raid0 --raid-devices=2 /dev/sdb /dev/sdc
mdadm --create --verbose /dev/md0 --level=raid0 --raid-devices=2 /dev/xvdb /dev/xvdc
mdadm --create --verbose /dev/md0 --level=raid0 --raid-devices=4 /dev/xvdb /dev/xvdc /dev/xvdd /dev/xvde

mdadm --create --verbose /dev/md0 --level=raid0 --raid-devices=4 /dev/xvdf /dev/xvdg /dev/xvdi /dev/xvdj
{% endhighlight %}

Generate A Lost mdadm.conf File:
{% highlight ruby %}
mdadm -Es | grep md > /etc/mdadm/mdadm.conf
mdadm --examine --scan > /etc/mdadm.conf
{% endhighlight %}