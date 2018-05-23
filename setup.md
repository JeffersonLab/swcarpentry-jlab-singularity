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

## Optionally, install singularity on a local linux system

You can also install singularity locally or on another linux system. At this
point singularity is only supported on linux, not on Windows or Mac.

To install singularity 2.5.1, execute the following commands:
~~~
VERSION=2.5.1
cd /tmp
wget https://github.com/singularityware/singularity/releases/download/$VERSION/singularity-$VERSION.tar.gz
tar xvf singularity-$VERSION.tar.gz
cd singularity-$VERSION
./configure --prefix=/usr/local
make
sudo make install
~~~
You can find what the latest version is on the [Singularity GitHub repository](https://github.com/singularityware/singularity/releases).
