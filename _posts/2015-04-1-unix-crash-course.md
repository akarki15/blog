---
title:  "Unix crashcourse"
date:   April 1, 2015
categories: unix shell shellpower
---

Following is a list of basic shell commands for Unix:

**ls**

{% highlight bash %}
ls -l 
{% endhighlight %}

Outputs 

{% highlight bash%}

drwxr-x---   2 akarki15 akarki15       6 Jun  2  2011 bin
-rw-r-----   1 akarki15 akarki15 4194304 Apr 22  2014 block-device.data
drwxrwxr-x  17 akarki15 akarki15    4096 Feb 28  2014 cs111
drwxr-x---  19 akarki15 akarki15    4096 May 28  2014 cs112
drwxr-x---   6 akarki15 akarki15     147 May 10  2014 cs-261
drwxr-x---   3 akarki15 akarki15      18 May  1  2013 CS281

{% endhighlight %}

* First column of the output is showing access rights
	1. rwx: read, write, executable
	2. Three sets of them for user, others in the group, and everyone

**How do you change the access settings?**

- `chmod u+w` will give _write_ rights to _users_ in the group
- `chmod o+x` will give _executable_ rights to _others_ in the group
- `chmod a-r` will take away _read_ rights to _everyone_ in the group


Some switches for ls

| Command	    | Description		 										 |
|---------------|------------------------------------------------------------|
| `ls -a`		    | shows "all" files 										 |
| `ls -d a*`      | Wildcard to display all files whose filename begins with a |
| `ls -d [i-l]*`  | [i-l] is a set containing letters i through l 			 |
 
	
**Cool things you can do with dot dot (..) and tilde (~)** 

- .. represents the parent director. So say you are in `/home/aashish` and `/home` has another file called `a.java`. You can access it from aashish by saying 
	
{% highlight bash %}
	cat ../a.java
{% endhighlight %}


* `~/` refers to the user home directory

**Using History** 

- `history` shows list of previous shell commands used. It gave following output on my computer: 

{% highlight bash %}

 5673  ssh -Y akarki15@romulus.amherst.edu
 5674  cd Desktop/jam/blog/
 5675  jekyll build
 5676  jekyll serve
{% endhighlight %}

- Run a certain numbered command by `!<number of the command>`. For exmaple `!5676` will run `jekyll serve`. 

**.cshrc file**


- `~/.cshrc` contains shell configuration 
- `PATH` contains paths for programs you run on terminal. E.g. more, less etc

**Random cool monitors**

- `vmstat 5` shows the paging history, 5 denotes how fast the list is being refreshed

- `ps uax` shows the processes running right now 

**All about that stream**

- Three I/O streams of unix (Similar to what it is in Java)
	- Say you have a java executable called prog.class
	- stdin 
		- `java prog < inputFile` will use `inputFile` for keyboardinput expected by stdin in java. 
	- stdout		
		- `java prog > outfile` writes whatever `System.out.println("")` into the `outfile` 		
			- Note that `System.err.println("")` is written on the screen instead of file
		- `java prog >& oufile` will write both stdout and stderr into `outfile`
		- `java prog > /dev/tty) >& /path` will write stdout to `/dev/tty` and stderr to `/path`
		- `prog >> outfile` appendas to the `outfile` instead of overwriting it 


**Pipe command**

- Feeds the output of one command to another (prog1 to prog2). e.g. 
{% highlight bash %}
	prog1 < file1 | prog2
{% endhighlight %}



**Suspend/resume jobs aka COOL STUFF**

- `ctrl+z` suspends/pauses the running job
- `bg` puts a job to background
- `jobs` prints the list of jobs
- `fg %1` bring job no. 1 from background to foreground  

**Tar Tricks**

- `tar cf Simplex.tar Simplex`
	- `c`reate a `f`ile `Simplex.tar` from `Simplex`
- `mkdir newDir ; cd newDir ; tar xf ../Simplex.tar`
	- Creates `newDir` and extracts `Simplex` into `newDir`
- Loop: `basename` parses out from every `$i` just its filename. The loop creates a copy of every file but changes the extension to `.save`.

{% highlight bash %}
foreach i (*.txt)
	foreach? cp $i `basename $i .txt`.save
	foreach? end
{% endhighlight %}

