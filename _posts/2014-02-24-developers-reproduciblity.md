---
layout: post
title: 'Developer's Reproduciblity'
date: 2014-02-24 13:30
comments: true
categories: 
---
#1 Project
For a small two year old project with 4+ people from back to front, used by 10K users everyday with 

1. CMS and
2. Sophiscate membership managment,
3. And some banking exchange

```
-------------------------------------------------------------------------------
Language                     files          blank        comment           code
-------------------------------------------------------------------------------
Python                          34           2232            485          18758
HTML                           160            771            246          10384
Javascript                      26            859           1161           8553
CSS                             15            996           1395           6436
SASS                             7            320             71           1313
YAML                             6             17             17            902
SQL                             33            116              0            577
Bourne Shell                     1              6              4             21
Ruby                             1              6             13              5
-------------------------------------------------------------------------------
SUM:                           283           5323           3392          46949
-------------------------------------------------------------------------------
```

#2 experinced
When there was 2 people, 1 from G, 1 from  Y, things was easy. One used MacPort and One uses Homebrew, everything was fine. A simple document is fine.

#3 is a warning
Then the third came, yet another senior, things still fine. But I started moving to `virtualenv` and `Fabric` as I have my hygenie standard on enviroment. Managing a constant changing database is a pain in the ass.

#n(n-1)/2
Here comes the fresh blood/brains. They spent hours to keep up the environment. Things went south immediately. My time was consumed by the newbies.

# For 2 hours
Finally, I decide to try Virtual Box. For 2 hours, I could setup a complete new environment.

# For 6 hours
I setup a completely reproducible enviroment using Vagrant. Don't aske me why I took so long. I recorded it in my calendar is that how long it takes.

# For 4 hours
I migrate my development environment to `Ansible`. Simply because I saw it in `Vagrant` 's document and love the [name](https://en.wikipedia.org/wiki/Ansible) and the [pholosophy](http://www.coloandcloud.com/editorial/an-interview-with-ansible-author-michael-dehaan/) behind.

# In 8 hours
I tried `docker` and give up. XD becuase I want not ready for it.

# In review
It's all about scale. For 20 hours, I've came to the level of reproducible I need and I am pleasant about it. The best thing is that the juniors can get up and coding (sort of) within 20 minutes.

In short, If there's only one, bare metal is enough. Stay focused on your pet project.

For 2+, `vagrant` should be there. Otherwise [Frederick Brooks](https://en.wikipedia.org/wiki/The_Mythical_Man-Month) will be laughing at you.

But `docker` is the blue meth, purist thing I've ever seen so far. Definitely the holy grail.
