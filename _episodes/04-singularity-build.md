---
title: "Building docker containers"
teaching: 5
exercises: 10
questions:
- "How do I create my own containers?"
objectives:
- "Understand how to build a recipe for a docker container."
keypoints:
- "Although using containers with singularity does not require superuser privileges, creating containers still does."
- "Dockerfiles are recipes for docker containers."
- "By storing Dockerfiles in a GitHub repository we gain version both tracking and cloud building."
---

## Creating docker containers

So, you want to build your own docker containers? Excellent. You may be able
to distribute your simulation or analysis code to others more easily without
the need to support a wide range of platforms.

Creating a docker container involves writing a Dockerfile recipe. For the
simplest of examples, let's look back at the lolcow we started with, on the [GitHub repository that houses the Dockerfile](https://github.com/GodloveD/lolcow/blob/master/Dockerfile)
~~~
FROM ubuntu:16.04

RUN apt-get update && apt-get install -y fortune cowsay lolcat

ENV PATH /usr/games:${PATH}
ENV LC_ALL=C

ENTRYPOINT fortune | cowsay | lolcat
~~~
The container uses Ubuntu 16.04 as a base layer, installs fortune, cowsay, and
lolcat, sets the command search path, and defines an entry point (which is
called when we run the container).

There is nothing more to writing a Dockerfile recipe than writing a shell script  
that specifies the steps to take to create container.

## Storing a Dockerfile on GitHub allows integration with Docker Hub

The next step to creating your container on Docker Hub is greatly simplified by
storing your Dockerfile on GitHub. This allows you to take advantage of
automatic building on Docker Hub itself.

> ## Build your own version of the lolcow container
>
> Let's recreate the lolcow container but instead use the most recent Ubuntu
> base layer, version 18.04.
>
> 1. Fork the [lolcow GitHub repository](https://github.com/GodloveD/lolcow/)
>    to your personal GitHub account.
> 2. Modify the base layer `FROM` statement to reflect the newer Ubuntu version
> 3. Create an account on Docker Hub
> 4. Create an automated build based on GitHub.
>
> > ## Solution
> >
> > It may take some time while Docker Hub creates your container, but you
> > should end up with a GitHub repository like [this one](https://github.com/wdconinc/lolcow)
> > and a Docker Hub page like [this one](https://hub.docker.com/r/wdconinc/lolcow/).
> {: .solution}
{: .challenge}
