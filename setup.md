---
layout: page
title: Setup
root: .
---
## Account on interactive and batch farm nodes at Jefferson Lab

In order to be able to use containers (and in particular singularity) most
productively, you will need a Jefferson Lab user account that can access the
interactive farm environment. This means you must be able to `ssh` into the
node `ifarm` (possibly by going through `login.jlab.org`).
~~~
ssh ifarm
~~~

## Local installation of singularity

You can also install singularity locally or on another linux system. At this
point singularity is only supported on linux, not on Windows or Mac.

To install singularity, execute the following commands:
~~~
cd /tmp
wget
tar -zxvf
./configure --prefix=/usr/local
make
sudo make install
~~~
