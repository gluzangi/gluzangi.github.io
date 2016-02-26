---
published: true
title: Mirroring with rsync
layout: post
---
{% highlight ruby %}
rsync --progress -havz -e "ssh" root@108.166.xx.xx:/var/www/html ./
rsync --progress -havz -e "ssh -l ssh-user" rsync-user@host:/path/to/files/ /dest
rsync --progress -havz -e "ssh -p $portNumber" /local/path/ user@remoteip:/path/to/files/ 
{% endhighlight %}

{% highlight ruby %}
rsync -Phavz --stats -e "ssh -l geraldl" 50.57.xx.xx:~/aws/ ~/
rsync -Phavz --stats --exclude="*.mp4" ./* gluzangi@192.0.159.178:/media/gsung/
rsync -Phavz -AX --compress-level=9 --bwlimit=0 --stats -e "ssh -c blowfish -i /root/.ssh/id_rsa" admin@host.domain.com:/path/to/source /path/to/dest/folder 
{% endhighlight %}

Synch while excluding folders:
{% highlight ruby %}
rsync -Phavzn --stats --exclude='Blah/' --exclude='Park/' --exclude='Monster/' --exclude='OpsCenter/' --exclude='muze/' --exclude='system/' --exclude='*/snapshots/' -e "ssh -i /root/.ssh/server.pem" ./  ec2-user@ec2-23-22-xxx-xxx.compute-1.amazonaws.com:/home/ec2-user/

rsync -Phavzn --stats --exclude='*/snapshots/' -e "ssh -i /root/.ssh/server.pem" ./*Smiles  ec2-user@ec2-23-22-xxx-xxx.compute-1.amazonaws.com:/home/ec2-user/

rsync -Phavzn --stats -e "ssh -i /root/.ssh/server.pem" ./*Smiles/snapshots/  ec2-user@ec2-23-22-xxx-xxx.compute-1.amazonaws.com:/home/ec2-user/
{% endhighlight %}

Bandwith optimization:
{% highlight ruby %}
rsync -Phavzn -X --compress-level=9 --bwlimit=0 --stats --log-file="/vol/rsync_logs/rsync.log.$(date +%Y%m%d%H%m%S)" -e "ssh -c blowfish -i /root/.ssh/id_rsa" /vol/ admin@host.domain.com:/share/vol/
{% endhighlight %}