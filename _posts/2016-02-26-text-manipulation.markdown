---
published: true
title: Text Manipulation
layout: post
---
WHILE loop:

{% highlight ruby %}
while read line; do (echo $line); done
{% endhighlight %}

FOR loop:

{% highlight ruby %}
for name in {1..10}.txt; do touch $name; done
{% endhighlight %}

Read A Line On A File:

{% highlight ruby %}
$ cat file.txt | while read line; do (echo $line); done
{% endhighlight %}


{% highlight ruby %}
cut -d":" -f1 -s /etc/group | (while read line; do sudo chown -R $line.$line ./$line; done)
cut -d":" -f1 -s /home/ec2-user/passwd | while read line; do sudo chown -R $line.$line /home/$line ; done
cut -d"/" -f3 DreamPunsDBSST.list | while read line; do mv ./DreamParkDB/$line ./DreamPunsDBSST/$line; done
{% endhighlight %}

Read the mailboxes lines and copy to archive directory 

{% highlight ruby %}
cat mailboxes.txt | while read line; do cp ./mail/$line ./mail_archives/ ; done
{% endhighlight %}

Substitution:

replace 'cat' by 'dog' in file in.txt and output it to file out.txt the 'g' means replace all matches, not just the first on a given line

{% highlight ruby %}
sed -e 's/cat/dog/g' in.txt > out.txt
{% endhighlight %}

Batch File Rename:

{% highlight ruby %}
for file in *.* ; do mv [SOURCE_NAME] [DEST_NAME]; done
{% endhighlight %}

Batch File Rename Ext:

{% highlight ruby %}
for file in *.bkp
do
mv $file `basename $filename .bkp`;
done
{% endhighlight %}