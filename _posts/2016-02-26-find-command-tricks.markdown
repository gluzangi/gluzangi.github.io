---
published: true
title: find command tricks
layout: post
---
Finding Empty Directories:

{% highlight ruby %}
find ./ -type d -empty -print0 | xargs -0 rmdir
{% endhighlight %}

Find and bulk move files:

{% highlight ruby %}
find ./ -type f -name "*.db" -print | while read line; do (mv $line ./DreamPunsDBData/$line) done;
find ./DreamPunsDB/ -type f -name *Data.db | sort -n > ./DreamPunsDBSST.list

find /tmp -name core -type f -print0 | xargs -0 /bin/rm -f
find /path/to/files -name *.tsv -type f -print0 | xargs -0 -I {} /bin/mv {} /path/to/destination
{% endhighlight %}

Find and delete:

- Delete all logs which are older than 461 days ago

{% highlight ruby %}
find  /media/ephemeral0/data/logs/ -type f -mtime +461 -print0 | xargs -0 /bin/rm -f
{% endhighlight %}

- Delete all logs which are younger than 90 days ago

{% highlight ruby %}
find  /media/ephemeral0/data/logs/ -type f -mtime -90 -print0 | xargs -0 /bin/rm -f
{% endhighlight %}

- Delete all files containing "failed_core" which are older than 720 days ago

{% highlight ruby %}
find /var/log/hoover/v6 -iname *failed_core* -daystart -mtime +720 -print0 | xargs -0 /bin/rm -f
find / -type f -size +10000000k -exec ls -lh --sort=size {} \; | awk '{ print $9 ": " $5 }'
{% endhighlight %}

Using 'grep' as a 'find' command

{% highlight ruby %}
grep -R -aiH "iSSD" /var /etc /home
{% endhighlight %}

Finding Difference Between Directories:

- List all files that are different from dir_1 and dir_2

{% highlight ruby %}
diff -rq dir_1 dir_2 | sort > dir_1_diff.txt
{% endhighlight %}

Sort Files:

- To arrange the 3rd and 4th column in numerical with using ":" field separator

{% highlight ruby %}
sort -t : -k 3,4 -n /etc/passwd | more
{% endhighlight %}