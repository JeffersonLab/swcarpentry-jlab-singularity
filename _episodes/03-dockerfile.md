---
title: "Creating your own containers"
teaching: 10
exercises: 5
questions:
- "How can I create my own containers?"
- "Why should I build docker containers even if I am using singularity?"
objectives:
- "Understand how container layering allows for portability and reusability."
- "Map the ecosystem of services that can take advantage of docker containers."
keypoints:
- "Docker containers can be used on the widest array of platforms."
- "Dockerfiles are recipes for docker containers."
- "By storing Dockerfiles in a GitHub repository we gain version both tracking and cloud building."
---

Up to this point we have exclusively talked about singularity as our interface
to containers. However, you will likely be faced with blank stares if you talk
about singularity containers with our friends at Amazon Web Services, GitHub, or
literally any other large software organization that is investing in
containerization and virtualization.

They will talk to you have about *docker*.

## Singularity, Docker: What's all that about?

The most common container format currently in use is not singularity, but rather
docker. Why do we not use docker on the interactive farm nodes at Jefferson Lab?

Unfortunately running docker in a scientific computing environment requires too
many trade-offs on security to the point where it is not a workable solution.
Effectively one would need to give superuser privileges to all docker users at
Jefferson Lab...

This is where singularity comes in! At no point in the past episode did you need
superuser privileges to run a guest operating system on the Jefferson Lab
interactive farm node.

But wait, there's more!

Singularity can natively load docker containers, directly from docker hub.
~~~
singularity pull docker://electronioncollider/jleic:1.0.0
singularity run jleic-1.0.0.simg
~~~

~~~
Docker image path: index.docker.io/electronioncollider/jleic:1.0.0
Cache folder set to /lustre/expphy/volatile/hallc/qweak/wdconinc/singularity/docker
[34/34] |===================================| 100.0%
Importing: base Singularity environment
Exploding layer: sha256:18b8eb7e7f013bd0e585c8c88c6f24599a5db1cbbe72e54246004dad662582c1.tar.gz
WARNING: Warning reading tar header: Ignoring malformed pax extended attribute
WARNING: Warning reading tar header: Ignoring malformed pax extended attribute
WARNING: Warning reading tar header: Ignoring malformed pax extended attribute
Exploding layer: sha256:32ed41d700a68921e01c0f5b2d74ed9da073915d4c61a90dbc32a1fe00d2f3b7.tar.gz
Exploding layer: sha256:4d9ef36483ec64d1f4946d48fab0924034fc0bfc6b8ab73f9cd6bef9cabb88b2.tar.gz
Exploding layer: sha256:1ad7107ca7f526f0e2e159abdbed52425d9293ed52cb4df70cc408d76f044e09.tar.gz
Exploding layer: sha256:b797f44ab34afa949131769bddb320eaaaaf8e842336fbb30d01ac6e7b3bb3e9.tar.gz
Exploding layer: sha256:3b5d341419e73f8a9c0a94b5bc5d906b1a323ddf7d7dcedadd76b8344614c87c.tar.gz
Exploding layer: sha256:5148a839749525ff0c5657be56b6e91dfb8003e9d42d440e5b8918e6fe8265ef.tar.gz
Exploding layer: sha256:e41c39d2b6564e331fee260dd81160bdd1e773d7a8293d2ed6167bcebd700b3f.tar.gz
Exploding layer: sha256:5c0f99e3009917f25a8f6708fbdca0bee3879e944be2262ddbb1a5ab8a4af310.tar.gz
Exploding layer: sha256:25264bd8b04602a313f9baa2114989c76c248ceae6aaf033ac841225d58a0f7a.tar.gz
Exploding layer: sha256:2443a4be215d747e26d15f88354b82c846bbc375f45b2d736a1b90538dd40f3e.tar.gz
Exploding layer: sha256:f1aa5ed6052f22ac06197d54111c066776cd542282338b7f8d9797cd001ec9a2.tar.gz
Exploding layer: sha256:193e022ed0a144e749d50a7ef7f5c6ddf41213d48413edc022f962d9f9400719.tar.gz
Exploding layer: sha256:e823a724a54d941ff6d493b752f2d643f21a3ced81c91917da7dc6a3ab3d22c1.tar.gz
Exploding layer: sha256:63d6eb91c67de97f262b67531f7f8356ad8c8b0cf8abb85ff8098c5a9b4c4bb2.tar.gz
Exploding layer: sha256:4138be3481bf259aeea3e822770a308f099fbbd2a7b9fac72375bc44d6ec9fc3.tar.gz
Exploding layer: sha256:710b5d0684c704a03e65039309c87c97b597bfff838c9cf6331e453d3dbf2156.tar.gz
Exploding layer: sha256:17e316c8b786816e6cde7dc89fc4ed5f6490255971409c47d956304055f13903.tar.gz
Exploding layer: sha256:870f7026f0c43fbd4e756c93eb11afcea4238ac8496b00c7becb3e9b41428753.tar.gz
Exploding layer: sha256:2137eb6f06c8ea4a29617ddb8687015e6c01441467f2371c3fa288a5855eda81.tar.gz
Exploding layer: sha256:da02753573941a8d93ddda5beee102e237cf824b368105918279297d71820fa1.tar.gz
Exploding layer: sha256:2c0eeadeed40d40a433bad23813f722c52db3411375051f8fd04774f850e025f.tar.gz
Exploding layer: sha256:7306c40f87c57c56961be669806a72b0ceabd102b1c925ceab80c9e583d6b38a.tar.gz
Exploding layer: sha256:d8e5179e920cf53d32f3c7daf17c2fe6126ce095306b1e6c11f799bd7387a513.tar.gz
Exploding layer: sha256:4267bfc935fc24474201dfabb55f62f8dbc70c77ae7393d53d50df9d779447eb.tar.gz
Exploding layer: sha256:38fa6296dff800141d875a8dda184587e28a96bdd1296a78929eb60e6a54a00a.tar.gz
Exploding layer: sha256:f502ae11b23c47393c676256482a7a7a8e78d6ac3e2681aa9bb31fa01fb8c9b5.tar.gz
Exploding layer: sha256:edee6c963a7e3c7ab34ce0087acc93398741f786650a09192dc3eab800d33f7e.tar.gz
Exploding layer: sha256:b8402a6ed84bcedb1b5cf80fc398bd9ac8332f4ccf3fb9e731c2c3233064ecc4.tar.gz
Exploding layer: sha256:9775bd270fe81119bb45f727ee4541fbc52822046e5244e60bc0d5631499043e.tar.gz
Exploding layer: sha256:4b13ad2b8addaabfda501730f317bc7a3eae6b977120d8f76318e622a1b28ea7.tar.gz
Exploding layer: sha256:613568e39dd437312400133b34d945f8fefafe2356e0b3b502925aa78a530025.tar.gz
Exploding layer: sha256:cdb2aeb7a7b7430a913e5d5b96e1771902c2d64d9c8099ba660786e63e987f7c.tar.gz
Exploding layer: sha256:607f73f0682151591642f261b5cb93ec3d33a046a7722fbf97ef86ddc04ee63f.tar.gz
Exploding layer: sha256:09647ecf0caa778f76c087ea031eaf103fa9802b5749f117f6a4d9e396c81a4b.tar.gz
WARNING: Building container as an unprivileged user. If you run this container as root
WARNING: it may be missing some functionality.
Building Singularity image...
Singularity container built: ./jleic-1.0.0.simg
Cleaning up...
Done. Container is at: ./jleic-1.0.0.simg
~~~


~~~
unset OSRELEASE
source /jlab/2.1/ce/jlab.sh
~~~

## Creating docker containers
