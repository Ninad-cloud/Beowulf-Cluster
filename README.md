# Beowulf-Cluster
Configuration Set-Up for the Cluster.
Configuration:
•	installing the redhat(rhel-5.4) the stable version.
•	give the hostname to each node; 
         -using    #vi /etc/sysconfig/network
          - and make the entris of following ;
       bc1-01
       bc1-02
       bc1-03    and so on;
       for evry node.
•	then reboot the systems (using init 6 command).
config the ip-add for each node using ;"system-config-network" command.
    192.168.13.1/255.255.255.0
    192.168.13.2/255.255.255.0
    192.168.13.3/255.255.255.0

•	for host based authentication- make the entreis in
•	# vi /etc/hosts(eg. 192.168.13.1     bc1-01     bc1-01)
•	In this type of clusters we required remote ssh login to all nodes;
•	for this following commands
  -cd  ~ 
  - ssh-keygen(then simply enter for each step)
 - ssh root@192.168.13.1
 - ssh root@bc1-01
 - from every node to other nodes
- ssh-copy-id root@bc1-01(from every node to other node)
1.	goto vi /etc/ssh/ssh_config (uncomment the line to "Hostbasedauthentication  yes")
2.	vi /etc/ssh/sshd_config( make sure of the hostbasedauthentication on)
3.	ssh-agent  $SHELL
4.	ssh-add
5.	exit
6.	vi /etc/ssh/shosts.equiv(eg. bc1-01)
7.	/etc/init.d/network restart.
NFS config:
1.	yum install portmap
2.	iptables -F
3.	iptables -L
4.	service iptables stop
5.	service iptables save
6.	iptables -L
7.	service portmap restart
8.	vi /etc/exports(/home *(rw,sync)
9.	service portmap restart
10.	service nfs restart
11.	service nfslock restart
12.	for   client side:
13.	iptables -F
14.	iptables -L
15.	vi /etc/fstab(/home  /home   nfs  defaults  0 0)
16.	mount -a
17.	if not then all services must restart
installing MPICH2-1.0.8p1;(extract in /)
1.	./configure --prefix=/usr/local/mpich2-1.0.8p1 >& configure.log
2.	make >& make.log
3.	make install >& install.log
4.	export PATH=$PATH:/usr/local/mpich2-1.0.8p1/bin
5.	vi mpd.hosts(eg. bc1-01; bc1-02...)
6.	vi /etc/mpd.conf(eg. MPD_SECRETWORD=password)on individual m/c
7.	mpdboot
8.	mpd -d &
9.	mpdtrace -l
10.	cd examples
11.	make cpi
12.	mpiexec -l -n 2(no. of process) ./cpi(program name)
13.	for mpi ther must me exist of gcc in m/c if not
14.	then, yum install gcc*
15.	it shows the output
