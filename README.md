Ubuntu 15.10 Docker image
=============================

Description
-----------

This is the Original Ubuntu 15.10 root docker images. It is small and basic.

It includes fresh installation of Ubuntu 15.10 distribution, english language, universe apt packages and some basic common packages: vim-tiny editor, bash-completion to save time, curl to use webservices and supervisor to run easily more process in Docker VM.  

So, this image respects pragmatic simple vision of Docker.  
If you are looking for a complete VM, just use LXC.  
**LXC** is an amazing product to get fast **full VM** where **Docker** is amazing to get only **one service by VM**.

This ref how Sylvain Lasnier built his ubuntu image for my own custom setting

Usage
-----

You can run shell like this:

    $ docker run --rm -t -i kiralpoon/ubuntu /bin/bash
    
You can calculate the first thousand pi decimals:

    $ docker run --rm -ti kiralpoon/ubuntu
    
You can extend this image for testing service. For example, test `nginx` web server:
    
    $ docker run --rm -ti -p 80 kiralpoon/ubuntu /bin/bash
    
Test it from another terminal:
  
    