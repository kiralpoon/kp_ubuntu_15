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

    $ docker run --rm -t -i kiralpoon/ubuntu_15 /bin/bash
	root@1817a311eb14:/# cat /etc/lsb-release 
	DISTRIB_ID=Ubuntu
	DISTRIB_RELEASE=15.10
	DISTRIB_CODENAME=wily
	DISTRIB_DESCRIPTION="Ubuntu 15.10"
	root@1817a311eb14:/# exit
	exit

You can install apt in docker's ubunutu to calculate the first thousand pi decimals:

    $ docker run --rm -ti kiralpoon/ubuntu_15
    root@eb1051451f95:/# apt-get install -y -q bc
	Reading package lists...
	Building dependency tree...
	Reading state information...
	The following NEW packages will be installed:
	  bc
	0 upgraded, 1 newly installed, 0 to remove and 0 not upgraded.
	Need to get 82.6 kB of archives.
	After this operation, 246 kB of additional disk space will be used.
	Get:1 http://archive.ubuntu.com/ubuntu/ wily/main bc amd64 1.06.95-9build1 [82.6 kB]
	Fetched 82.6 kB in 0s (168 kB/s)
	debconf: delaying package configuration, since apt-utils is not installed
	Selecting previously unselected package bc.
	(Reading database ... 12428 files and directories currently installed.)
	Preparing to unpack .../bc_1.06.95-9build1_amd64.deb ...
	Unpacking bc (1.06.95-9build1) ...
	Setting up bc (1.06.95-9build1) ...

    # it will use the arc tangent function a() and bc utils to calculate the pi.
    # scale gives you the number of decimal place
    root@eb1051451f95:/# time echo "scale=1000; 4*a(1)" | bc -l
	3.141592653589793238462643383279502884197169399375105820974944592307\
	81640628620899862803482534211706798214808651328230664709384460955058\
	22317253594081284811174502841027019385211055596446229489549303819644\
	28810975665933446128475648233786783165271201909145648566923460348610\
	45432664821339360726024914127372458700660631558817488152092096282925\
	40917153643678925903600113305305488204665213841469519415116094330572\
	70365759591953092186117381932611793105118548074462379962749567351885\
	75272489122793818301194912983367336244065664308602139494639522473719\
	07021798609437027705392171762931767523846748184676694051320005681271\
	45263560827785771342757789609173637178721468440901224953430146549585\
	37105079227968925892354201995611212902196086403441815981362977477130\
	99605187072113499999983729780499510597317328160963185950244594553469\
	08302642522308253344685035261931188171010003137838752886587533208381\
	42061717766914730359825349042875546873115956286388235378759375195778\
	18577805321712268066130019278766111959092164201988

	real    0m0.436s
	user    0m0.428s
	sys     0m0.004s

You can extend this image for testing service. For example, test `nginx` web server:
    
    $ docker run --rm -ti -p 80 kiralpoon/ubuntu_15 /bin/bash
    ...
    root@6742501682fe:/# service nginx start
 	* Starting nginx nginx  

Test it from another terminal:
  
    $ docker ps
 	CONTAINER ID        IMAGE                 COMMAND             CREATED             STATUS              PORTS                   NAMES
	6742501682fe        kiralpoon/ubuntu_15   "/bin/bash"         2 minutes ago       Up 2 minutes        0.0.0.0:32768->80/tcp   dreamy_wright

 	$ curl -I 0.0.0.0:32768
 	HTTP/1.1 200 OK
	Server: nginx/1.9.3 (Ubuntu)
	Date: Mon, 27 Jun 2016 17:07:11 GMT
	Content-Type: text/html
	Content-Length: 612
	Last-Modified: Mon, 27 Jun 2016 17:05:14 GMT
	Connection: keep-alive
	ETag: "57715cca-264"
	Accept-Ranges: bytes

	#In addition, you can also test this with your broswer by typing the url and "Welcome to nginx" should be shown to your page

To stop the service:
	root@6742501682fe:/# service nginx stop
	 * Stopping nginx nginx       [ OK ] 
	root@6742501682fe:/# exit 
	exit




