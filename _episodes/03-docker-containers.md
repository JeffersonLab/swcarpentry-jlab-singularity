---
title: "Using docker containers"
teaching: 10
exercises: 10
questions:
- "Why should I know about docker containers if I am using singularity?"
objectives:
- "Understand how container layering allows for portability and reusability."
- "Map the ecosystem of services that can take advantage of docker containers."
keypoints:
- "Docker containers can be used on the widest array of platforms."
---

Up to this point we have exclusively talked about singularity as our interface
to containers. However, you will likely be faced with blank stares if you talk
about singularity containers with our friends at Amazon Web Services, GitHub, or
literally any other large software organization that is investing in
containerization and virtualization.

They will talk to you about *docker*.

## Singularity, Docker: What's all that about?

The most common container format currently in use is not singularity, but rather
docker. Why do we not use docker on the interactive farm nodes at Jefferson Lab?

Unfortunately running docker in a scientific computing environment requires too
many trade-offs on security to the point where it is not a workable solution.
Effectively one would need to give superuser privileges to all docker users at
Jefferson Lab...

This is where singularity comes in! At no point in this lesson did you need
superuser privileges to run a guest operating system on the Jefferson Lab
interactive farm node.

But wait, there's more!

Singularity can natively load docker containers, directly from Docker Hub (where
docker containers are typically housed). Instead of specifying `shub` we merely
have to specify `docker` in the 'protocol' section of the URL.

## Retrieving the Jefferson Lab Common Environment container directly from Docker Hub

We can now retrieve the Jefferson Lab Common Environment container:
~~~
singularity pull docker://jeffersonlab/jlabce:2.2
~~~
Instead of loading a full singularity container, docker uses a multitude of
layers, one for each operation that was performed on the container. This allows
docker to be more efficient with disk space (no need to store the same base
layer more than once, after all).

By using singularity we are giving up some of the benefits of docker, but
gaining the ability to run without superuser privileges. Let's try this on the
Jefferson Lab Common Environment container.

> ## Retrieve the Jefferson Lab Common Environment container, tag 2.2, directly from Docker Hub
>
> 1. Take a look at the [Docker Hub page for the jlabce container](https://hub.docker.com/r/jeffersonlab/jlabce/)
> 2. Note the capitalization of 'jeffersonlab' (we've all made some bad choices
>    in the past that we now regret)
> 3. Pull the Docker Hub container using singularity pull
> 4. Start a shell in the container from Docker Hub (which will have by default
>    a different filename from the container from Singularity Hub)
> 5. Unset OSRELEASE and load the Jefferson Lab Common Environment, version 2.2.
>
> > ## Solution
> > ~~~
> > singularity pull docker://jeffersonlab/jlabce:2.2
> > singularity shell jlabce-2.2.simg
> > unset OSRELEASE
> > source /jlab/2.2/ce/jlab.sh
> > ~~~
> >
> > The downloading should have produced the following output:
> > ~~~
> > WARNING: pull for Docker Hub is not guaranteed to produce the
> > WARNING: same image on repeated pull. Use Singularity Registry
> > WARNING: (shub://) to pull exactly equivalent images.
> > Docker image path: index.docker.io/jeffersonlab/jlabce:2.2
> > Cache folder set to /lustre/expphy/volatile/hallc/qweak/wdconinc/singularity/docker
> > [5/5] |===================================| 100.0%
> > Importing: base Singularity environment
> > Exploding layer: sha256:0f819de0d331ea8dd8dc8db153b7e771f78b2cbd768d2fbf832ff9ef8a64c79c.tar.gz
> > WARNING: Warning reading tar header: Ignoring malformed pax extended attribute
> > WARNING: Warning reading tar header: Ignoring malformed pax extended attribute
> > WARNING: Warning reading tar header: Ignoring malformed pax extended attribute
> > Exploding layer: sha256:a91d0ef0aae19bff29469898d18af3c1d00991542adc74accfb179a09bf267b6.tar.gz
> > Exploding layer: sha256:5c0288a20319269e863c35c6967301f9715eede03d35916996a0708004eec515.tar.gz
> > Exploding layer: sha256:b730691c3d74e3c267dfa9d088751454b881bfc8a1f90d229c7ef5c8a25ddaf0.tar.gz
> > Exploding layer: sha256:de09139c64733b25e3114b11f7cad17fe83366fb906ef6542e2edebd8acf3858.tar.gz
> > Exploding layer: sha256:990f3b3acb0de543fa7b18bf630815880e0a9f8f73570a8de26b907e5856728d.tar.gz
> > Exploding layer: sha256:fa9de769675a19a6aa24d39dbae8f5244e62840f8d45fbb2bd42b459dc6b3eab.tar.gz
> > Exploding layer: sha256:e5518714ec0ee63cbf3b4008513ebab1a08964e90f79d3a8074724b4bc8b8d85.tar.gz
> > Exploding layer: sha256:ee335588045368fab72da68cf50056c189a44e54d6e1b3f45e5e3add4595b068.tar.gz
> > Exploding layer: sha256:2d601d9486b3d5ef5a51e3e3a3ccca5f6a0d7bedb669ed2ca5f70c6fa733df24.tar.gz
> > Exploding layer: sha256:1091d963997ca3c760bb7432795dca0283ac4f59708290f0d3b242cdae94e58a.tar.gz
> > Exploding layer: sha256:a21fcb9376a7db6ff0d7dd63306bae44bddb6403a05825e1b082ceb1c126ae88.tar.gz
> > WARNING: Building container as an unprivileged user. If you run this container as root
> > WARNING: it may be missing some functionality.
> > Building Singularity image...
> > Singularity container built: ./jlabce-2.2.simg
> > Cleaning up...
> > Done. Container is at: ./jlabce-2.2.simg
> > ~~~
> > You can see that 11 layers went into this container. If you were to now
> > download the container with tag 2.1, which is based on the same underlying
> > CentOS 7.3 layer, you would not need to download nearly as much.
> > Nevertheless, the final singularity image (`.simg`) would again be about
> > 2 GB large.
> {: .solution}
{: .challenge}

## Retrieve Electron Ion Collider containers directly from Docker Hub

But, of course, now that we have gotten the hang of this, why stop here?

We can pull the environment for the Jefferson Lab EIC (JLEIC) simulation
studies, tag 1.0.3.

> ## Retrieve the Jefferson Lab Electron Ion Collider (JLEIC) container
>
> The location on Docker Hub is `electronioncollider/jleic:1.0.3`
>
> > ## Solution
> > ~~~
> > Docker image path: index.docker.io/electronioncollider/jleic:1.0.3
> > Cache folder set to /lustre/expphy/volatile/hallc/qweak/wdconinc/singularity/docker
> > [34/34] |===================================| 100.0%
> > Importing: base Singularity environment
> > Exploding layer: sha256:18b8eb7e7f013bd0e585c8c88c6f24599a5db1cbbe72e54246004dad662582c1.tar.gz
> > WARNING: Warning reading tar header: Ignoring malformed pax extended attribute
> > WARNING: Warning reading tar header: Ignoring malformed pax extended attribute
> > WARNING: Warning reading tar header: Ignoring malformed pax extended attribute
> > Exploding layer: sha256:32ed41d700a68921e01c0f5b2d74ed9da073915d4c61a90dbc32a1fe00d2f3b7.tar.gz
> > Exploding layer: sha256:4d9ef36483ec64d1f4946d48fab0924034fc0bfc6b8ab73f9cd6bef9cabb88b2.tar.gz
> > Exploding layer: sha256:1ad7107ca7f526f0e2e159abdbed52425d9293ed52cb4df70cc408d76f044e09.tar.gz
> > Exploding layer: sha256:b797f44ab34afa949131769bddb320eaaaaf8e842336fbb30d01ac6e7b3bb3e9.tar.gz
> > Exploding layer: sha256:3b5d341419e73f8a9c0a94b5bc5d906b1a323ddf7d7dcedadd76b8344614c87c.tar.gz
> > Exploding layer: sha256:5148a839749525ff0c5657be56b6e91dfb8003e9d42d440e5b8918e6fe8265ef.tar.gz
> > Exploding layer: sha256:e41c39d2b6564e331fee260dd81160bdd1e773d7a8293d2ed6167bcebd700b3f.tar.gz
> > Exploding layer: sha256:5c0f99e3009917f25a8f6708fbdca0bee3879e944be2262ddbb1a5ab8a4af310.tar.gz
> > Exploding layer: sha256:25264bd8b04602a313f9baa2114989c76c248ceae6aaf033ac841225d58a0f7a.tar.gz
> > Exploding layer: sha256:2443a4be215d747e26d15f88354b82c846bbc375f45b2d736a1b90538dd40f3e.tar.gz
> > Exploding layer: sha256:f1aa5ed6052f22ac06197d54111c066776cd542282338b7f8d9797cd001ec9a2.tar.gz
> > Exploding layer: sha256:193e022ed0a144e749d50a7ef7f5c6ddf41213d48413edc022f962d9f9400719.tar.gz
> > Exploding layer: sha256:e823a724a54d941ff6d493b752f2d643f21a3ced81c91917da7dc6a3ab3d22c1.tar.gz
> > Exploding layer: sha256:63d6eb91c67de97f262b67531f7f8356ad8c8b0cf8abb85ff8098c5a9b4c4bb2.tar.gz
> > Exploding layer: sha256:4138be3481bf259aeea3e822770a308f099fbbd2a7b9fac72375bc44d6ec9fc3.tar.gz
> > Exploding layer: sha256:710b5d0684c704a03e65039309c87c97b597bfff838c9cf6331e453d3dbf2156.tar.gz
> > Exploding layer: sha256:17e316c8b786816e6cde7dc89fc4ed5f6490255971409c47d956304055f13903.tar.gz
> > Exploding layer: sha256:870f7026f0c43fbd4e756c93eb11afcea4238ac8496b00c7becb3e9b41428753.tar.gz
> > Exploding layer: sha256:2137eb6f06c8ea4a29617ddb8687015e6c01441467f2371c3fa288a5855eda81.tar.gz
> > Exploding layer: sha256:da02753573941a8d93ddda5beee102e237cf824b368105918279297d71820fa1.tar.gz
> > Exploding layer: sha256:2c0eeadeed40d40a433bad23813f722c52db3411375051f8fd04774f850e025f.tar.gz
> > Exploding layer: sha256:7306c40f87c57c56961be669806a72b0ceabd102b1c925ceab80c9e583d6b38a.tar.gz
> > Exploding layer: sha256:d8e5179e920cf53d32f3c7daf17c2fe6126ce095306b1e6c11f799bd7387a513.tar.gz
> > Exploding layer: sha256:4267bfc935fc24474201dfabb55f62f8dbc70c77ae7393d53d50df9d779447eb.tar.gz
> > Exploding layer: sha256:38fa6296dff800141d875a8dda184587e28a96bdd1296a78929eb60e6a54a00a.tar.gz
> > Exploding layer: sha256:f502ae11b23c47393c676256482a7a7a8e78d6ac3e2681aa9bb31fa01fb8c9b5.tar.gz
> > Exploding layer: sha256:edee6c963a7e3c7ab34ce0087acc93398741f786650a09192dc3eab800d33f7e.tar.gz
> > Exploding layer: sha256:b8402a6ed84bcedb1b5cf80fc398bd9ac8332f4ccf3fb9e731c2c3233064ecc4.tar.gz
> > Exploding layer: sha256:9775bd270fe81119bb45f727ee4541fbc52822046e5244e60bc0d5631499043e.tar.gz
> > Exploding layer: sha256:4b13ad2b8addaabfda501730f317bc7a3eae6b977120d8f76318e622a1b28ea7.tar.gz
> > Exploding layer: sha256:613568e39dd437312400133b34d945f8fefafe2356e0b3b502925aa78a530025.tar.gz
> > Exploding layer: sha256:cdb2aeb7a7b7430a913e5d5b96e1771902c2d64d9c8099ba660786e63e987f7c.tar.gz
> > Exploding layer: sha256:607f73f0682151591642f261b5cb93ec3d33a046a7722fbf97ef86ddc04ee63f.tar.gz
> > Exploding layer: sha256:09647ecf0caa778f76c087ea031eaf103fa9802b5749f117f6a4d9e396c81a4b.tar.gz
> > WARNING: Building container as an unprivileged user. If you run this container as root
> > WARNING: it may be missing some functionality.
> > Building Singularity image...
> > Singularity container built: ./jleic-1.0.3.simg
> > Cleaning up...
> > Done. Container is at: ./jleic-1.0.3.simg
> > ~~~
> {: .solution}
{: .challenge}

We can even pull the equivalent environment for the Brookhaven National Lab EIC
simulation studies, tag r964.

> ## Retrieve the Brookhaven National Lab Electron Ion Collider container
>
> The location on Docker Hub is `ayk1964/eicroot:r964`
{: .challenge}

It would be unthinkable to run two disparate frameworks from different national
labs based on different operating systems next to each other with minimal
effort.

## Retrieve MOLLER simulation and analysis containers directly from Docker Hub

We can pull the environment for the Jefferson Lab MOLLER simulation and analysis
software, `remoll` and `japan`.

> ## Retrieve the Jefferson Lab MOLLER simulation container
>
> The location on Docker Hub is `jeffersonlab/remoll:develop`
> 
> Once you pulled the `remoll:develop` container, run the command `remoll` inside it, either using shell or using run.
>
> > ## Solution
> > ~~~
> > $ singularity pull docker://jeffersonlab/remoll:develop
> > Docker image path: index.docker.io/jeffersonlab/remoll:develop
> > Cache folder set to /lustre/expphy/volatile/halla/parity/wdconinc/docker
> > [25/25] |===================================| 100.0% 
> > Importing: base Singularity environment
> > Exploding layer: sha256:7dc0dca2b1516961d6b3200564049db0a6e0410b370bb2189e2efae0d368616f.tar.gz
> > Exploding layer: sha256:a1805b8a2cb454859fe58c2629d54391acc35b3897b21c6622a5b9e18e8f1035.tar.gz
> > Exploding layer: sha256:c44ab5e312a776234f3cce9797555cc0a15bfbef2dfcf2b0edf70d942b8f6839.tar.gz
> > Exploding layer: sha256:d6d5f6b64ea5caa25725976e184adcd27fe8345da027015ec22533784a31b67b.tar.gz
> > Exploding layer: sha256:9f6f42344cbd24b2fea45cce050c015feb68d6c9ad237edc803ea1339a5c5e0b.tar.gz
> > Exploding layer: sha256:3fc272a7392ba96f3314599a9b060f6d8ef97c4f4687f219ae016084cd73c888.tar.gz
> > Exploding layer: sha256:fbe93b2fa49adc652c5e90029c7de970c019c3e72eafb007ec300ba31fbb4e95.tar.gz
> > Exploding layer: sha256:89e48c9012b758f506073a30968bd8ed2253948de4f0b312e6a1af8788ff01b2.tar.gz
> > Exploding layer: sha256:19f41eb751344f2164b52a6dffc03de8a79537480099bb23b07d6e2f8d7c09f1.tar.gz
> > Exploding layer: sha256:12a8a540c425c851f11c00b9d99ca3ba61c7bfbe5ce921355299b43d088e254f.tar.gz
> > Exploding layer: sha256:9756d4106cff436eb75be0d4ab964e1ae6bc7f54630501c58ccd2c1d1794ccae.tar.gz
> > Exploding layer: sha256:e6f8fbba5727edf354f2a5768e82e5676105ee50ecced1f84fca02e5c0432d81.tar.gz
> > Exploding layer: sha256:01c6cec2a8f19d0ef4633e7b7751fc6e910a729dd50ec707e7accaddce0009b4.tar.gz
> > Exploding layer: sha256:17cde3210398472fc61002b4250995967fbd49575ece4fb8c6d5a509c15a002d.tar.gz
> > Exploding layer: sha256:4b0c633e1dc00b124bb8bad32d329501b947b23304a3b8dad99cd730dba3b47f.tar.gz
> > Exploding layer: sha256:f53066f618cf176a90ff4a77e2b5f2d059ad4274712c2176ae193f8646ba37ba.tar.gz
> > Exploding layer: sha256:1b4cb466aff0c35994f55135b0b220118c061869836350b2bb51cf078f1f031d.tar.gz
> > Exploding layer: sha256:735b1285bcfe7d3c09287ffdb16fb12c485da74c1e59660f8eea1a6b52216e2d.tar.gz
> > Exploding layer: sha256:4a77e8db35067d6b2b45e9df148e7ea96eab913d40f41b37962b56516b16ace7.tar.gz
> > Exploding layer: sha256:64facce03c1968b7d769ec992dbea6805bee2d226766a1c474ad5dd26d6cfc54.tar.gz
> > Exploding layer: sha256:962a1da5315cb09e02c747c5c7d089c9b3bd9882a8f3a3ade7b9fbcb41b79c74.tar.gz
> > Exploding layer: sha256:194e1efc6763fd80e30fdde12a4ef9b23e9256a2f558271b538824154138d185.tar.gz
> > Exploding layer: sha256:f6e7b5fea36201eb8d6e05b55c11b61f3d4e2e53b4ea47e473f5cbefc53e2bfc.tar.gz
> > Exploding layer: sha256:7b4f132cf6b658e9ba3ae77ddacc44f25e2173463d084e8ee2cbad14cceb6247.tar.gz
> > Exploding layer: sha256:a7b9f4862932d794bd825994d2bd1395877f09ad5d4384cc3e5aa8a0c1a7acec.tar.gz
> > Exploding layer: sha256:a90f02738b7659105627db1232ba06b308fe8db1a11b835c297c7bafa82417c9.tar.gz
> > Building Singularity image...
> > Singularity container built: ./remoll-develop.simg
> > Cleaning up...
> > Done. Container is at: ./remoll-develop.simg
> > $ singularity run remoll-develop.simg remoll
> > ~~~
> {: .solution}
{: .challenge}

> ## Retrieve the Jefferson Lab MOLLER analyzer container
>
> The location on Docker Hub is `jeffersonlab/japan:develop`
>
> > ## Solution
> > ~~~
> > $ singularity pull docker://jeffersonlab/japan:develop
> > $ singularity run japan-develop.simg build/qwparity
> > ~~~
> {: .solution}
{: .challenge}

## Submitting farm jobs with singularity

Of course, ultimately the goal is to submit farm jobs with singularity. Here is a basic xml job scripts which just prints the usage information for one of the japan components:
```
<Request>
  <Email email="username@jlab.org" request="false" job="false"/>
  <Project name="moller12gev"/>
  <Track name="simulation"/>
  <Name name="remoll-singularity"/>
  <Command><![CDATA[
   setenv SINGULARITY_CACHEDIR .
   module load singularity
   cd /volatile/halla/parity/$USER/singularity
   singularity run remoll-develop.simg build/remoll /volatile/halla/parity/$USER/singularity/runexample.mac
  ]]></Command>

  <Job>
  </Job>
</Request>
```
Since (currently) the command is run from a fixed directory inside the container, you have to both specify an absolute path to the macro on the command line and specify an absolute path to the output ROOT file inside the macro.
