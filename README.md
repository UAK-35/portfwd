portfwd
=======

User-space TCP/UDP port forwarding services

## Summary
 This project contains two applications: tcpfwd, udpfwd, which are for TCP and UDP port forwarding literally.
 Written in pure C, with libevent2 library.

##### Details of modificatons by UAK-35 - commit 1
    1) Added CI file .travis.yml FROM https://github.com/muzea-ci/portfwd
    2) Updated udpfwd.c FROM https://github.com/towserchen/portfwd
    3) Updated udpfwd.c FROM https://github.com/V-E-O/portfwd
    4) Updated tcpfwd.c FROM https://github.com/YueLun/portfwd
    5) Added .gitignore file
 
## Usage ##

    tcpfwd|udpfwd <local_addr:local_port> <dest_addr:dest_port> [-d] [-o]
     
    Options:
      -d              run in background
      -o              accept IPv6 connections only for IPv6 listener
      -p <pidfile>    write PID to file

## Examples

##### Map local TCP port 1022 to 192.168.1.77:22

    tcpfwd 0.0.0.0:1022 192.168.1.77:22     # allow access from all hosts
    tcpfwd 127.0.0.1:1022 192.168.1.77:22   # only allow localhost
    tcpfwd [::]:1022 192.168.1.77:22        # allow access to port 1022 via both IPv4 and IPv6

##### Map local UDP port 53 to 8.8.8.8:53

    udpfwd 0.0.0.0:53 8.8.8.8:53
    udpfwd [::]:53 8.8.8.8:53

##### IPv4-IPv6 transforming

    udpfwd [::]:1701 localhost:1701         # add IPv6 support for a local L2TP service
    tcpfwd 0.0.0.0:80 [2001:db8:3::2]:80    # enable IPv4 access for an IPv6-only web service
