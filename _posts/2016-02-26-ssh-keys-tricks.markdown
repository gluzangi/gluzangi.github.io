---
published: true
title: SSH Keys Tricks
layout: post
---
SSH With Identity Key:

{% highlight ruby %}
sudo ssh -i /home/geraldl/.ssh/id_rsa user@domain.com
{% endhighlight %}

Appending File Using SSH:

{% highlight ruby %}
cat id_rsa.pub | ssh user@host.domain.com 'cat >> /home/user/.ssh/authorized_keys'
cat ~/.ssh/id_dsa.pub | ssh user@host.domain.com 'mkdir .ssh; cat >> .ssh/authorized_keys'
cat ~/.ssh/id_rsa.pub | ssh user@domain.com 'cat >> .ssh/authorized_keys'
{% endhighlight %}

{% highlight ruby %}
for i in server1 server2 server3 server4; 
do 
    echo "sending file to $i";
    cat localfile | ssh -p portnumber user@$i "cat >> remotefile"; 
done;
{% endhighlight %}

SSHFS With Identity Key:

{% highlight ruby %}
sshfs -o idmap=user -o ssh_command="ssh -i /root/server.pem"  user@domain.com:/media/vol /mnt/partition
{% endhighlight %}