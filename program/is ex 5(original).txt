[student@fedora ~]$ su  
Password:  
[root@localhost security lab]# cd /usr/src  
[root@localhost security lab]# wget https://www.snort.org/downloads/snort/daq-2.0.7.tar.gz  
--2025-03-07 12:34:56--  https://www.snort.org/downloads/snort/daq-2.0.7.tar.gz  
Resolving www.snort.org... 104.16.37.37, 104.16.36.36  
Connecting to www.snort.org|104.16.37.37|:443... connected.  
HTTP request sent, awaiting response... 200 OK  
Length: 1420300 (1.3M) [application/x-gzip]  
Saving to: ‘daq-2.0.7.tar.gz’  

100%[====================================>] 1,420,300   2.34MB/s   in 0.6s    

2025-03-07 12:34:57 (2.34 MB/s) - ‘daq-2.0.7.tar.gz’ saved  
[root@localhost security lab]# wget https://www.snort.org/downloads/snort/snort-2.9.16.1.tar.gz  
--2025-03-07 12:35:10--  https://www.snort.org/downloads/snort/snort-2.9.16.1.tar.gz  
Resolving www.snort.org... 104.16.37.37, 104.16.36.36  
Connecting to www.snort.org|104.16.37.37|:443... connected.  
HTTP request sent, awaiting response... 200 OK  
Length: 5250080 (5.0M) [application/x-gzip]  
Saving to: ‘snort-2.9.16.1.tar.gz’  

100%[====================================>] 5,250,080   3.12MB/s   in 1.6s    

2025-03-07 12:35:12 (3.12 MB/s) - ‘snort-2.9.16.1.tar.gz’ saved  
[root@localhost security lab]# tar xvzf daq-2.0.7.tar.gz  
daq-2.0.7/  
daq-2.0.7/configure  
daq-2.0.7/Makefile.am  
daq-2.0.7/README  
...
[root@localhost security lab]# tar xvzf snort-2.9.16.1.tar.gz  
snort-2.9.16.1/  
snort-2.9.16.1/configure  
snort-2.9.16.1/Makefile.am  
snort-2.9.16.1/README  
...
[root@localhost security lab]# yum install libpcap* pcre* libdnet* -y  
...
Complete!  
[root@localhost security lab]# cd daq-2.0.7  
[root@localhost security lab]# ./configure  
checking for gcc... gcc  
checking whether the C compiler works... yes  
checking for C compiler default output file name... a.out  
...
[root@localhost security lab]# make  
...
[root@localhost security lab]# make install  
...
[root@localhost security lab]# cd ../snort-2.9.16.1  
[root@localhost security lab]# ./configure  
checking for gcc... gcc  
checking whether the C compiler works... yes  
checking for C compiler default output file name... a.out  
...
[root@localhost security lab]# make  
...
[root@localhost security lab]# make install  
...
[root@localhost security lab]# snort --version  
   ,,_     -*> Snort! <*-  
  o"  )~   Version 2.9.8.2 GRE (Build 335)  
   ''''    By Martin Roesch & The Snort Team: http://www.snort.org/contact#team  
           Copyright (C) 2014-2015 Cisco and/or its affiliates. All rights reserved.  
           Copyright (C) 1998-2013 Sourcefire, Inc., et al.  
Using libpcap version 1.7.3  
Using PCRE version: 8.38 2015-11-23  
Using ZLIB version: 1.2.8  
[root@localhost security lab]# mkdir /etc/snort  
[root@localhost security lab]# mkdir /etc/snort/rules  
[root@localhost security lab]# mkdir /var/log/snort  
[root@localhost security lab]# vi /etc/snort/snort.conf  
include /etc/snort/rules/icmp.rules  
[root@localhost security lab]# vi /etc/snort/rules/icmp.rules  
alert icmp any any -> any any (msg:"ICMP Packet"; sid:477; rev:3;)
[root@localhost security lab]# snort -i enp3s0 -c /etc/snort/snort.conf -l /var/log/snort/  
Running in IDS mode  
--== Initialization Complete ==--  
[root@localhost security lab]# ping www.yahoo.com  
PING edge.gycpi.b.yahoodns.net (106.10.138.240) 56(84) bytes of data.  
64 bytes from media-router-fp2.prod.media.vip.bf1.yahoo.com (106.10.138.240): icmp_seq=1 ttl=52 time=14.3 ms  
64 bytes from media-router-fp2.prod.media.vip.bf1.yahoo.com (106.10.138.240): icmp_seq=2 ttl=52 time=13.9 ms  
64 bytes from media-router-fp2.prod.media.vip.bf1.yahoo.com (106.10.138.240): icmp_seq=3 ttl=52 time=14.0 ms  
^C  
--- edge.gycpi.b.yahoodns.net ping statistics ---  
3 packets transmitted, 3 received, 0% packet loss, time 2003ms  
rtt min/avg/max/mdev = 13.906/14.095/14.354/0.188 ms  
[root@localhost security lab]# vi /var/log/snort/alert  
[**] [1:477:3] ICMP Packet [**]  
[Priority: 0]  
10/06-15:03:11.187877 192.168.43.148 -> 106.10.138.240  
ICMP TTL:64 TOS:0x0 ID:45855 IpLen:20 DgmLen:84 DF  
Type:8 Code:0 ID:14680 Seq:64 ECHO  

[**] [1:477:3] ICMP Packet [**]  
[Priority: 0]  
10/06-15:03:11.341739 106.10.138.240 -> 192.168.43.148  
ICMP TTL:52 TOS:0x38 ID:2493 IpLen:20 DgmLen:84  
Type:0 Code:0 ID:14680 Seq:64 ECHO REPLY  

[**] [1:477:3] ICMP Packet [**]  
[Priority: 0]  
10/06-15:03:12.189727 192.168.43.148 -> 106.10.138.240  
ICMP TTL:64 TOS:0x0 ID:46238 IpLen:20 DgmLen:84 DF  
Type:8 Code:0 ID:14680 Seq:65 ECHO  

[**] [1:477:3] ICMP Packet [**]  
[Priority: 0]  
10/06-15:03:12.340881 106.10.138.240 -> 192.168.43.148  
ICMP TTL:52 TOS:0x38 ID:7545 IpLen:20 DgmLen:84  
Type:0 Code:0 ID:14680 Seq:65 ECHO REPLY  
