docker2vagrant
==============

Simple script to transform a Dockerfile into a Vagrantfile.

Needs this some days ago, did this script, thought it might be useful to someone else too.

Prerequisite
------------
- vagrant
- perl

What is working
---------------
- Transform all the run commands from the Dockerfile, into a provision script named bootstrap.sh.
- Create a new Vagrantfile with the specified box (or precise64 by default).
- Forward all the exposed ports of the Dockerfile. All the exposed guest ports are forwarded to the host ports with the same number, except for system ports (<= 1024), for those ones, 9000 is added (for example 80 will be forwarded to 9080).
- Copy all the files in the vagrant VM that were copied into the docker using ADD commands (commands appended in the bootstrap script).
- Create a service that launch the docker command (CMD) during the VM startup (if one was specified).

What is not working
-------------------
Don't know yet. Might be a lot of things though. Just tested this on some Dockerfile I'd got on my computer.

How to
------
The simple way to use this script, is to place the command line where the docker image is. And to just launch the script.
```
/path/docker/image$ /path/script/docker2vagrant
```

Some options can be used:
```
-f or --file    -> specify the Dockerfile path    (default is ./Dockerfile)
-b or --box     -> specify the vagrant box to use (default is precise64)
-u or --url     -> specify the vagrant box url    (default is http://files.vagrantup.com/precise64.box)
-o or --output  -> specify the output path        (default is .) (NOT YET TESTED)
```

Appendix
--------
Vagrant is releasing a new feature in its 1.6 version permitting to provision a vagrant image with docker.
http://www.vagrantup.com/blog/feature-preview-vagrant-1-6-docker-dev-environments.html
So once released, it might be more straightforward to use this new feature, than a custom script.
