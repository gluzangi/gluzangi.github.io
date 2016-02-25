---
published: true
title: SSH Keys at work
layout: post
---
SSH with identity key:

sudo ssh -i /home/unixuser/.ssh/id_rsa ec2-user@ec2-xx-xxx-81-46.compute-1.amazonaws.com

Appending new keys using SSH:

cat id_rsa.pub | ssh ec2-user@access.domain.com 'cat >> /home/ec2-user/.ssh/authorized_keys'
cat ~/.ssh/id_dsa.pub | ssh ec2-user@access.domain.com 'mkdir .ssh; cat >> .ssh/authorized_keys'
cat ~/.ssh/id_rsa.pub | ssh user@hostname 'cat >> .ssh/authorized_keys'

Sending a key multiple server:
for i in server1 server2 server3 server4; 
do 
    echo "sending file to $i";
    cat localfile | ssh -p portnumber user@$i "cat >> remotefile"; 
done;

SSHFS with identity key:
sshfs -o idmap=user -o ssh_command="ssh -i /root/accesspoint.pem -l ec2-user"  ec2-xx-xxx-182-37.compute-1.amazonaws.com:/media/ext/