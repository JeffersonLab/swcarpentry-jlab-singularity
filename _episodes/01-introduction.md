---
title: "Introduction"
teaching: 10
exercises: 5
questions:
- "How can we replicate the Jefferson Lab environment on other systems?"
objectives:
- "Understand how containers are a way of packaging a full running environment."
- "Set up your local shell to allow access to the singularity command."
- "Load an example singularity shell."
keypoints:
- "Containers allow us to package up entire running environments for posterity."
---

## Using the singularity command

The singularity command is not loaded by default on the interactive farm nodes.
Instead, you have to enable access through the `module` command by issuing the
command:
~~~
module load singularity
~~~
Now, the singularity command will be available in your session. You can check
whether singularity is available by just typing `singularity`. A message with
common singularity commands will appear.
~~~
singularity
~~~

When you log in again a next time, you will need to repeat the `module load`
command.

> ## Add the 'module load' command to your login script
>
> To avoid having to enter the same `module load` command every time we log in,
> it is useful to add it to the login script `.login`.
> 1. Edit the script `.login` and add the following line to the end:
>    ~~~
>    module load singularity
>    ~~~
> 2. Log out and log back in
> 3. Verify that you can indeed use the singularity command
>
{: .challenge}

## Where should we run singularity?

Containers can be large: several GB is not uncommon for containers that include
all of geant4, data files and all. We should take care not to store these large
files in quota-restricted directories such as your home directory.

Since singularity uses some of the same terminology as git (in particular,
`singularity pull`), we can benefit from setting up singularity so it also
behaves similarly as git.

Since `git pull` creates files in the current directory, it makes sense to
setup singularity such that `singularity pull` creates files in the current
directory, not in a hidden cache directory in your home directory.

To obtain this behavior, edit your login script `.login` and add the following
line at the end of the file. Make sure to log out and log back in again, and
verify that the cache directory has indeed been correctly set.
~~~
setenv SINGULARITY_CACHEDIR .
~~~

## Running your first container

Naturally, we start by running a first container that just returns "hello,
world!" or something similar.

> ## Running your first container, directly from the cloud!
>
> Just as git can clone from a URL, singularity can pull from a URL. In this
> case we will pull from shub://GodloveD/lolcow.
>
> 1. Create and navigate to a directory where you can write large files
>    ~~~
>    mkdir -p /volatile/hallc/qweak/$USER/singularity
>    cd /volatile/hallc/qweak/$USER/singularity
>    ~~~
> 1. Run the container with the following command.
>    ~~~
>    singularity run shub://GodloveD/lolcow
>    ~~~
>
> > ## Solution
> > You should see the following output:
> > ~~~
> > Progress |===================================| 100.0%
> > / I'll burn my books.    \
> > |                        |
> > \ -- Christopher Marlowe /
> >  ------------------------
> >         \   ^__^
> >          \  (oo)\_______
> >             (__)\       )\/\
> >                 ||----w |
> >                 ||     ||
> > ~~~
> > Likely with a different quote...
> {: .solution}
{: .challenge}

## Running local copies of the container

When you have downloaded a container once, there is no need to download it again
and again. We can run the local copy:
~~~
singularity run GodloveD-lolcow-master-latest.simg
~~~
You will notice that this command, naturally, completed a lot more quickly.

Everywhere a container URL is accepted, we can provide either a local file, a
shub link, or (as we will see later) a docker link.

## Starting a shell in a container

We can also interact with our container through a shell environment. Think of
this as "logging into" your container.
~~~
singularity shell GodloveD-lolcow-master-latest.simg
~~~

> ## Navigate around inside the container shell and note the differences.
>
> Start a shell inside the lolcow container and explore the differences with the
> host operating system.
>
> 1. Do you still have access to the current directory?
> 2. Do you still have access to the home directory?
> 2. Do you still have access to the /cache directory?
> 3. Do you still have access to the /apps directory?
> 4. When you run the container, the command `fortune` is called to generate the
>    quote. Where is the command `fortune` located (use the command `which` to
>    find out)? Is this command available on the host operating system?
> 5. Do you still have access to, for example, the `jcache` command that is
>    available on the host operating system?
>
> > ## Solution
> >
> > The container provides transparent access to the current directory, to the
> > home directories, and to a selection of common data storage paths. However,
> > it provides its own overlay of the system directories where executables are
> > stored. This is where the `fortune` command is found, in `/usr/games/bin`,
> > a path that does not exist on the host operating system.
> {: .solution}
{: .challenge}

## Containers as an appliance vs. containers as an environment

Now is a good time to wade into the intricacies of a fundamental debate in how
containers are to be used.

- Some containers are provided as appliances (or apps). The user calls the
  container as they would call a command, using `singularity run` with possibly
  a list of arguments to be passed to the container. This is how we ran the
  lolcow container above at first.
- Other containers are provided as full-fledged environments, and the user is
  expected to use the `shell` command to interact with them. This is how we
  ran the lolcow container by opening a shell into them.

We are not going to restrict ourselves to one viewpoint. Instead, think about
what best fits the use case that you have in mind. As a user you may find the
'container as an environment' more common at first.

> ## What makes a container an appliance?
>
> Start a shell inside the lolcow container and look at the file `/singularity`.
> What does it contain?
>
> > ## Solution
> >
> > The file `/singularity` contains a simple shell script that is executed
> > when the container is ran in appliance mode.
> > ~~~
> > #!/bin/sh
> >
> > fortune | cowsay | lolcat
> > ~~~
> > We will see later how to specify this run script when creating containers.
> {: .solution}
{: .challenge}

### Using the Jefferson Lab Common Environment container

Now that we have the basics of containers behind us, we can use our first
'useful' container: the Jefferson Lab Common Environment container. This
container replicates the scientific software suite that is installed on the
interactive farm nodes, but packages it up in a nice container.

Here is how we download the container:
~~~
singularity pull shub://JeffersonLab/jlabce
singularity shell jlabce-master.simg
~~~
We could have used the `singularity shell` command as well, but this
demonstrates how we can separate the downloading from running (when using the
container as an appliance) or opening a shell (when using the container as an
environment).
