---
title: "Running the JLab CE container"
teaching: 5
exercises: 5
questions:
- "How can we replicate the Jefferson Lab Common Environment on other systems?"
objectives:
- "Understand how tags are used to version containers."
- "Load and use the Jefferson Lab Common Environment on the interactive farm nodes."
keypoints:
- "The Jefferson Lab Common Environment containers provide a standard environment."
---

## Tags: versioning of containers

In the previous episode we downloaded the lolcow container, at
`shub://GodloveD/lolcow` and the container was stored with the filename
`GodloveD-lolcow-master-latest.simg`. Let's analyze that URL and filename.

- `shub` indicates that the URL points to a Singularity Hub location.
- `GodloveD` is the user who provided this container (David Godlove, if you
  must know, see for example this [GitHub page](https://github.com/GodloveD/lolcow)).
- `lolcow` is the name of the repository that was used to build this container.
- `master` is the branch from which the container was built.
- `latest` is the tag of the container, with latest for the most recent build.

The tag is commonly used for versioning of containers. By specifying the URL as
`shub://GodloveD/lolcow:latest` we can explicitly ask for the latest version of
the lolcow container.

Since there is not a lot of versioning one can do on this container, we will
first introduce a container where versions ARE important.

## Retrieving the Jefferson Lab Common Environment container

Now that we have the basics of containers behind us, we can use our first
'useful' physics container: the Jefferson Lab Common Environment container. This
container replicates the scientific software suite that is installed on the
interactive farm nodes, but packages it up in a nice container.

Of course, there is no real practical need to load the Jefferson Lab Common
Environment on a Jefferson Lab interactive farm node, but bear with me for now.

Here is how we download the container:
~~~
singularity pull shub://JeffersonLab/jlabce:2.1
singularity shell JeffersonLab-jlabce-master-2.1.simg
~~~
Notice how we specified as the tag `2.1` which will instruct singularity to
retrieve container version 2.1. We could also retrieve versions 2.0 and 2.2.
In fact, the three available containers are listed on the [Singularity Hub page](https://www.singularity-hub.org/collections/363).

We could have used the `singularity shell` command as well, but this
demonstrates how with `pull` we can separate the downloading from running (when
using the container as an appliance) or opening a shell (when using the
container as an environment).

> ## Retrieve the Jefferson Lab Common Environment container, tag 2.2
>
> 1. Navigate to a directory where you can write large files
>    ~~~
>    mkdir -p /volatile/hallc/qweak/$USER/singularity
>    cd /volatile/hallc/qweak/$USER/singularity
>    ~~~
> 1. Retrieve the Jefferson Lab Common Environment container, tag 2.2, with
>    `singularity pull`.
>
> > ## Solution
> > The following command should have worked:
> > ~~~
> > singularity pull shub://JeffersonLab/jlabce:2.2
> > ~~~
> > This produces the following output:
> > ~~~
> > Progress |===================================| 100.0%
> > Done. Container is at: /lustre/expphy/volatile/hallc/qweak/wdconinc/singularity/JeffersonLab-jlabce-master-2.2.simg
> > ~~~
> {: .solution}
{: .challenge}

## Using the Jefferson Lab Common Environment container
