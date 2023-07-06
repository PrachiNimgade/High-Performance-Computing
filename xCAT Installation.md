
         # xCAT Stateless installation process
         Install CentOs7 version 7.9

         yum update -y

         yum upgrade -y

         hostnamectl set-hostname xCAT

         Entry add both machine name and IP address in /etc/hosts file

         vi /etc/hosts

            10.10.10.2 xCAT


         vi /etc/selinux/config

         getenforce 

         init 6

         systemctl stop firewalld.service

         systemctl disable firewalld.service

         systemctl status firewalld.service

         yum install yum-utils

         yum install epel-release

yum -y install yum-utils

wget -P /etc/yum.repos.d https://xcat.org/files/xcat/repos/yum/latest/xcat-core/xcat-core.repo --no-check-certificate

wget -P /etc/yum.repos.d https://xcat.org/files/xcat/repos/yum/xcat-dep/rh7/x86_64/xcat-dep.repo --no-check-certificate

yum -y install xCAT

cat /etc/profile.d/xcat.sh

source /etc/profile.d/xcat.sh

If you want to change master ip in tab site

#chdef -t site xcat=10.10.10.3 comment

 lsdef -t osimage 
 
 lsblk ( If you are not able to see sr0 OS image then check
         then check DVD is connected or not to Vmware

 
 dd if=/dev/sr0 of=centos.iso
 
 copycds centos.iso 
 
 lsdef -t osimage
 
 OS Path ------------>/install/centos7.9/x86_64

 
 lsdef -t osimage centos7.9-x86_64-netboot-compute
 
 genimage centos7.9-x86_64-netboot-compute
 
 cd /install/netboot/centos7.9/x86_64/compute/
 
 mkdir -p /install/custom/netboot
 
 chdef -t osimage centos7.9-x86_64-netboot-compute synclists="/install/custom/netboot/compute.synclist"

lsdef -t osimage centos7.9-x86_64-netboot-compute

vim /install/custom/netboot/compute.synclist

cat /install/custom/netboot/compute.synclist

lsdef -t osimage

packimage centos7.9-x86_64-netboot-compute

 mkdef -t node cn00 groups=compute,all ip=10.10.10.3 mac=00:0c:29:98:93:43 netboot=xnba

lsdef cn00

chdef -t site domain=cdac.in

tabdump site | grep domain

makehosts

vim /etc/hosts

cat /etc/hosts

127.0.0.1   localhost localhost.localdomain localhost4 localhost4.localdomain4
::1         localhost localhost.localdomain localhost6 localhost6.localdomain6
10.10.10.2 master master.cdac.in (xcat domain added)
10.10.10.3 cn00 cn00.cdac.in

:wq save file


makenetworks

makedhcp -n

cat /etc/dhcp/dhcpd.conf

makedns -n

nodeset compute osimage=centos7.9-x86_64-netboot-compute

chdef -t site dhcpinterfaces=ens37


restart xcatd






chroot /install/netboot/centos7.9/x86_64/compute/rootimg
 

mkdir test

cd test

vi test.txt

exit

ssh cn00

# On second machine check file found

# On master machine

yum --installroot=/install/netboot/centos7.9/x86_64/compute/rootimg install

echo /install/netboot/centos7.9/x86_64/compute/rootimg

yum --installroot=/install/netboot/centos7.9/x86_64/compute/rootimg install vim

packimage centos7.9-x86_64-netboot-compute




# TO MAKE CLONE OF IMAGE

imgaexport centos7.9-x86_64-netboot-compute

ls

imgimport centos7.9-x86_64-netboot-compute.tgz -f compute-bk (computer name of clone image)

lsdef -t osimage

lsdef cn00

chdef -t provmethod=compute-bk

lsdef cn00








Transaction Summary
=============================================================================================================================================================================================
Install  1 Package

Total download size: 15 k
Installed size: 24 k
Is this ok [y/d/N]: y
Downloading packages:
warning: /var/cache/yum/x86_64/7/extras/packages/epel-release-7-11.noarch.rpm: Header V3 RSA/SHA256 Signature, key ID f4a80eb5: NOKEY
Public key for epel-release-7-11.noarch.rpm is not installed
epel-release-7-11.noarch.rpm                                                                                                                                          |  15 kB  00:00:00     
Retrieving key from file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
Importing GPG key 0xF4A80EB5:
 Userid     : "CentOS-7 Key (CentOS 7 Official Signing Key) <security@centos.org>"
 Fingerprint: 6341 ab27 53d7 8a78 a7c2 7bb1 24c6 a8a7 f4a8 0eb5
 Package    : centos-release-7-9.2009.0.el7.centos.x86_64 (@anaconda)
 From       : /etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
Is this ok [y/N]: y
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  Installing : epel-release-7-11.noarch                                                                                                                                                  1/1 
  Verifying  : epel-release-7-11.noarch                                                                                                                                                  1/1 

Installed:
  epel-release.noarch 0:7-11                                                                                                                                                                 

Complete!
[root@master ~]# wget -P /etc/yum.repos.d https://xcat.org/files/xcat/repos/yum/latest/xcat-core/xcat-core.repo --no-check-certificate
--2023-06-03 11:36:43--  https://xcat.org/files/xcat/repos/yum/latest/xcat-core/xcat-core.repo
Resolving xcat.org (xcat.org)... 166.70.135.166
Connecting to xcat.org (xcat.org)|166.70.135.166|:443... connected.
WARNING: cannot verify xcat.org's certificate, issued by ‘/C=US/O=Let's Encrypt/CN=R3’:
  Issued certificate has expired.
HTTP request sent, awaiting response... 200 OK
Length: 206
Saving to: ‘/etc/yum.repos.d/xcat-core.repo’

100%[===================================================================================================================================================>] 206         --.-K/s   in 0s      

2023-06-03 11:36:47 (3.02 MB/s) - ‘/etc/yum.repos.d/xcat-core.repo’ saved [206/206]

[root@master ~]# wget -P /etc/yum.repos.d https://xcat.org/files/xcat/repos/yum/xcat-dep/rh7/x86_64/xcat-dep.repo --no-check-certificate
--2023-06-03 11:37:05--  https://xcat.org/files/xcat/repos/yum/xcat-dep/rh7/x86_64/xcat-dep.repo
Resolving xcat.org (xcat.org)... 166.70.135.166
Connecting to xcat.org (xcat.org)|166.70.135.166|:443... connected.
WARNING: cannot verify xcat.org's certificate, issued by ‘/C=US/O=Let's Encrypt/CN=R3’:
  Issued certificate has expired.
HTTP request sent, awaiting response... 200 OK
Length: 209
Saving to: ‘/etc/yum.repos.d/xcat-dep.repo’

100%[===================================================================================================================================================>] 209         --.-K/s   in 0s      

2023-06-03 11:37:06 (13.5 MB/s) - ‘/etc/yum.repos.d/xcat-dep.repo’ saved [209/209]

[root@master ~]# yum -y install xCAT
Loaded plugins: fastestmirror, langpacks
Loading mirror speeds from cached hostfile
epel/x86_64/metalink                                                                                                                                                  | 6.4 kB  00:00:00     
 * base: repo.extreme-ix.org
 * epel: repo.extreme-ix.org
 * extras: repo.extreme-ix.org
 * updates: repo.extreme-ix.org
https://epel.excellmedia.net/7/x86_64/repodata/repomd.xml: [Errno 14] curl#60 - "Peer's Certificate has expired."
Trying other mirror.
It was impossible to connect to the CentOS servers.
This could mean a connectivity issue in your environment, such as the requirement to configure a proxy,
or a transparent proxy that tampers with TLS security, or an incorrect system clock.
You can try to solve this issue by using the instructions on https://wiki.centos.org/yum-errors
If above article doesn't help to resolve this issue please use https://bugs.centos.org/.

epel                                                                                                                                                                  | 4.7 kB  00:00:00     
xcat-core                                                                                                                                                             | 3.0 kB  00:00:00     
xcat-dep                                                                                                                                                              | 2.9 kB  00:00:00     
(1/5): xcat-dep/primary_db                                                                                                                                            |  35 kB  00:00:00     
(2/5): xcat-core/primary_db                                                                                                                                           |  31 kB  00:00:00     
(3/5): epel/x86_64/group_gz                                                                                                                                           |  99 kB  00:00:01     
(4/5): epel/x86_64/updateinfo                                                                                                                                         | 1.0 MB  00:00:05     
(5/5): epel/x86_64/primary_db                                                                                                                                         | 7.0 MB  00:00:47     
Resolving Dependencies
--> Running transaction check
---> Package xCAT.x86_64 0:2.16.5-snap202303030907 will be installed
--> Processing Dependency: xCAT-client = 4:2.16.5-snap202303030907 for package: xCAT-2.16.5-snap202303030907.x86_64
--> Processing Dependency: xCAT-genesis-scripts-ppc64 = 1:2.16.5-snap202303030907 for package: xCAT-2.16.5-snap202303030907.x86_64
--> Processing Dependency: xCAT-genesis-scripts-x86_64 = 1:2.16.5-snap202303030907 for package: xCAT-2.16.5-snap202303030907.x86_64
--> Processing Dependency: xCAT-probe = 4:2.16.5-snap202303030907 for package: xCAT-2.16.5-snap202303030907.x86_64
--> Processing Dependency: xCAT-server = 4:2.16.5-snap202303030907 for package: xCAT-2.16.5-snap202303030907.x86_64
--> Processing Dependency: goconserver >= 0.3.3 for package: xCAT-2.16.5-snap202303030907.x86_64
--> Processing Dependency: ipmitool-xcat >= 1.8.17-1 for package: xCAT-2.16.5-snap202303030907.x86_64
--> Processing Dependency: /bin/ksh for package: xCAT-2.16.5-snap202303030907.x86_64
--> Processing Dependency: /usr/sbin/dhcpd for package: xCAT-2.16.5-snap202303030907.x86_64
--> Processing Dependency: /usr/sbin/in.tftpd for package: xCAT-2.16.5-snap202303030907.x86_64
--> Processing Dependency: bind for package: xCAT-2.16.5-snap202303030907.x86_64
--> Processing Dependency: elilo-xcat for package: xCAT-2.16.5-snap202303030907.x86_64
--> Processing Dependency: httpd for package: xCAT-2.16.5-snap202303030907.x86_64
--> Processing Dependency: nmap for package: xCAT-2.16.5-snap202303030907.x86_64
--> Processing Dependency: perl(CGI) for package: xCAT-2.16.5-snap202303030907.x86_64
--> Processing Dependency: perl(Expect) for package: xCAT-2.16.5-snap202303030907.x86_64
--> Processing Dependency: perl(XML::Simple) for package: xCAT-2.16.5-snap202303030907.x86_64
--> Processing Dependency: perl(xCAT::MsgUtils) for package: xCAT-2.16.5-snap202303030907.x86_64
--> Processing Dependency: perl(xCAT::NetworkUtils) for package: xCAT-2.16.5-snap202303030907.x86_64
--> Processing Dependency: perl(xCAT::Utils) for package: xCAT-2.16.5-snap202303030907.x86_64
--> Processing Dependency: perl-DBD-SQLite for package: xCAT-2.16.5-snap202303030907.x86_64
--> Processing Dependency: perl-IO-Stty for package: xCAT-2.16.5-snap202303030907.x86_64
--> Processing Dependency: syslinux for package: xCAT-2.16.5-snap202303030907.x86_64
--> Processing Dependency: syslinux-xcat for package: xCAT-2.16.5-snap202303030907.x86_64
--> Processing Dependency: xCAT-buildkit for package: xCAT-2.16.5-snap202303030907.x86_64
--> Processing Dependency: xnba-undi for package: xCAT-2.16.5-snap202303030907.x86_64
--> Running transaction check
---> Package bind.x86_64 32:9.11.4-26.P2.el7_9.13 will be installed
--> Processing Dependency: bind-libs-lite(x86-64) = 32:9.11.4-26.P2.el7_9.13 for package: 32:bind-9.11.4-26.P2.el7_9.13.x86_64
--> Processing Dependency: bind-libs(x86-64) = 32:9.11.4-26.P2.el7_9.13 for package: 32:bind-9.11.4-26.P2.el7_9.13.x86_64
---> Package dhcp.x86_64 12:4.2.5-83.el7.centos.1 will be installed
--> Processing Dependency: dhcp-libs(x86-64) = 12:4.2.5-83.el7.centos.1 for package: 12:dhcp-4.2.5-83.el7.centos.1.x86_64
--> Processing Dependency: dhcp-common = 12:4.2.5-83.el7.centos.1 for package: 12:dhcp-4.2.5-83.el7.centos.1.x86_64
---> Package elilo-xcat.noarch 0:3.14-6 will be installed
---> Package goconserver.x86_64 0:0.3.3-snap202011021058 will be installed
---> Package httpd.x86_64 0:2.4.6-99.el7.centos.1 will be installed
--> Processing Dependency: httpd-tools = 2.4.6-99.el7.centos.1 for package: httpd-2.4.6-99.el7.centos.1.x86_64
--> Processing Dependency: /etc/mime.types for package: httpd-2.4.6-99.el7.centos.1.x86_64
---> Package ipmitool-xcat.x86_64 0:1.8.18-3 will be installed
---> Package ksh.x86_64 0:20120801-144.el7_9 will be installed
---> Package nmap.x86_64 2:6.40-19.el7 will be installed
---> Package perl-CGI.noarch 0:3.63-4.el7 will be installed
--> Processing Dependency: perl(FCGI) >= 0.67 for package: perl-CGI-3.63-4.el7.noarch
---> Package perl-DBD-SQLite.x86_64 0:1.39-3.el7 will be installed
--> Processing Dependency: perl(DBI) >= 1.57 for package: perl-DBD-SQLite-1.39-3.el7.x86_64
---> Package perl-Expect.noarch 0:1.21-14.el7 will be installed
--> Processing Dependency: perl(IO::Pty) >= 1.03 for package: perl-Expect-1.21-14.el7.noarch
--> Processing Dependency: perl(IO::Tty) for package: perl-Expect-1.21-14.el7.noarch
---> Package perl-IO-Stty.noarch 0:0.03-1 will be installed
---> Package perl-XML-Simple.noarch 0:2.20-5.el7 will be installed
--> Processing Dependency: perl(XML::SAX) for package: perl-XML-Simple-2.20-5.el7.noarch
--> Processing Dependency: perl(XML::NamespaceSupport) for package: perl-XML-Simple-2.20-5.el7.noarch
---> Package perl-xCAT.noarch 4:2.16.5-snap202303030907 will be installed
--> Processing Dependency: perl(Digest::MD5) for package: 4:perl-xCAT-2.16.5-snap202303030907.noarch
--> Processing Dependency: perl(HTML::Form) for package: 4:perl-xCAT-2.16.5-snap202303030907.noarch
--> Processing Dependency: perl(HTTP::Cookies) for package: 4:perl-xCAT-2.16.5-snap202303030907.noarch
--> Processing Dependency: perl(HTTP::Headers) for package: 4:perl-xCAT-2.16.5-snap202303030907.noarch
--> Processing Dependency: perl(HTTP::Request) for package: 4:perl-xCAT-2.16.5-snap202303030907.noarch
--> Processing Dependency: perl(IO::Socket::SSL) for package: 4:perl-xCAT-2.16.5-snap202303030907.noarch
--> Processing Dependency: perl(JSON) for package: 4:perl-xCAT-2.16.5-snap202303030907.noarch
--> Processing Dependency: perl(LWP) for package: 4:perl-xCAT-2.16.5-snap202303030907.noarch
--> Processing Dependency: perl(LWP::UserAgent) for package: 4:perl-xCAT-2.16.5-snap202303030907.noarch
--> Processing Dependency: perl(SNMP) for package: 4:perl-xCAT-2.16.5-snap202303030907.noarch
--> Processing Dependency: perl(Sys::Syslog) for package: 4:perl-xCAT-2.16.5-snap202303030907.noarch
--> Processing Dependency: perl(XML::LibXML) for package: 4:perl-xCAT-2.16.5-snap202303030907.noarch
---> Package syslinux.x86_64 0:4.05-15.el7 will be installed
---> Package syslinux-xcat.noarch 0:3.86-2 will be installed
---> Package tftp-server.x86_64 0:5.2-22.el7 will be installed
---> Package xCAT-buildkit.noarch 4:2.16.5-snap202303030907 will be installed
---> Package xCAT-client.noarch 4:2.16.5-snap202303030907 will be installed
---> Package xCAT-genesis-scripts-ppc64.noarch 1:2.16.5-snap202303030907 will be installed
--> Processing Dependency: xCAT-genesis-base-ppc64 >= 2:2.13.10 for package: 1:xCAT-genesis-scripts-ppc64-2.16.5-snap202303030907.noarch
---> Package xCAT-genesis-scripts-x86_64.noarch 1:2.16.5-snap202303030907 will be installed
--> Processing Dependency: xCAT-genesis-base-x86_64 >= 2:2.13.10 for package: 1:xCAT-genesis-scripts-x86_64-2.16.5-snap202303030907.noarch
---> Package xCAT-probe.noarch 4:2.16.5-snap202303030907 will be installed
--> Processing Dependency: /usr/bin/tftp for package: 4:xCAT-probe-2.16.5-snap202303030907.noarch
---> Package xCAT-server.noarch 4:2.16.5-snap202303030907 will be installed
--> Processing Dependency: grub2-xcat >= 2.02-0.76.el7.1.snap201905160255 for package: 4:xCAT-server-2.16.5-snap202303030907.noarch
--> Processing Dependency: perl(Crypt::CBC) for package: 4:xCAT-server-2.16.5-snap202303030907.noarch
--> Processing Dependency: perl(Crypt::Rijndael) for package: 4:xCAT-server-2.16.5-snap202303030907.noarch
--> Processing Dependency: perl(DB_File) for package: 4:xCAT-server-2.16.5-snap202303030907.noarch
--> Processing Dependency: perl(Date::Parse) for package: 4:xCAT-server-2.16.5-snap202303030907.noarch
--> Processing Dependency: perl(HTTP::Async) for package: 4:xCAT-server-2.16.5-snap202303030907.noarch
--> Processing Dependency: perl(LWP::Protocol::https) for package: 4:xCAT-server-2.16.5-snap202303030907.noarch
--> Processing Dependency: perl(Net::DNS) for package: 4:xCAT-server-2.16.5-snap202303030907.noarch
--> Processing Dependency: perl(Net::SSLeay) for package: 4:xCAT-server-2.16.5-snap202303030907.noarch
--> Processing Dependency: perl(Net::Telnet) for package: 4:xCAT-server-2.16.5-snap202303030907.noarch
--> Processing Dependency: perl(Sys::Virt) for package: 4:xCAT-server-2.16.5-snap202303030907.noarch
--> Processing Dependency: perl-Crypt-SSLeay for package: 4:xCAT-server-2.16.5-snap202303030907.noarch
--> Processing Dependency: perl-Digest-SHA1 for package: 4:xCAT-server-2.16.5-snap202303030907.noarch
--> Processing Dependency: perl-HTTP-Async for package: 4:xCAT-server-2.16.5-snap202303030907.noarch
--> Processing Dependency: perl-Net-HTTPS-NB for package: 4:xCAT-server-2.16.5-snap202303030907.noarch
---> Package xnba-undi.noarch 0:1.21.1-1 will be installed
--> Running transaction check
---> Package bind-libs.x86_64 32:9.11.4-26.P2.el7 will be updated
--> Processing Dependency: bind-libs(x86-64) = 32:9.11.4-26.P2.el7 for package: 32:bind-utils-9.11.4-26.P2.el7.x86_64
---> Package bind-libs.x86_64 32:9.11.4-26.P2.el7_9.13 will be an update
--> Processing Dependency: bind-license = 32:9.11.4-26.P2.el7_9.13 for package: 32:bind-libs-9.11.4-26.P2.el7_9.13.x86_64
---> Package bind-libs-lite.x86_64 32:9.11.4-26.P2.el7 will be updated
---> Package bind-libs-lite.x86_64 32:9.11.4-26.P2.el7_9.13 will be an update
---> Package dhcp-common.x86_64 12:4.2.5-82.el7.centos will be updated
--> Processing Dependency: dhcp-common = 12:4.2.5-82.el7.centos for package: 12:dhclient-4.2.5-82.el7.centos.x86_64
---> Package dhcp-common.x86_64 12:4.2.5-83.el7.centos.1 will be an update
---> Package dhcp-libs.x86_64 12:4.2.5-82.el7.centos will be updated
---> Package dhcp-libs.x86_64 12:4.2.5-83.el7.centos.1 will be an update
---> Package grub2-xcat.noarch 0:2.02-0.76.el7.1.snap201905160255 will be installed
---> Package httpd-tools.x86_64 0:2.4.6-99.el7.centos.1 will be installed
---> Package mailcap.noarch 0:2.1.41-2.el7 will be installed
---> Package net-snmp-perl.x86_64 1:5.7.2-49.el7_9.2 will be installed
--> Processing Dependency: net-snmp-libs = 1:5.7.2-49.el7_9.2 for package: 1:net-snmp-perl-5.7.2-49.el7_9.2.x86_64
--> Processing Dependency: net-snmp-devel = 1:5.7.2-49.el7_9.2 for package: 1:net-snmp-perl-5.7.2-49.el7_9.2.x86_64
--> Processing Dependency: net-snmp-agent-libs = 1:5.7.2-49.el7_9.2 for package: 1:net-snmp-perl-5.7.2-49.el7_9.2.x86_64
--> Processing Dependency: net-snmp = 1:5.7.2-49.el7_9.2 for package: 1:net-snmp-perl-5.7.2-49.el7_9.2.x86_64
--> Processing Dependency: libnetsnmptrapd.so.31()(64bit) for package: 1:net-snmp-perl-5.7.2-49.el7_9.2.x86_64
--> Processing Dependency: libnetsnmpmibs.so.31()(64bit) for package: 1:net-snmp-perl-5.7.2-49.el7_9.2.x86_64
--> Processing Dependency: libnetsnmpagent.so.31()(64bit) for package: 1:net-snmp-perl-5.7.2-49.el7_9.2.x86_64
---> Package perl-Crypt-CBC.noarch 0:2.33-2.el7 will be installed
---> Package perl-Crypt-Rijndael.x86_64 0:1.12-1.el7 will be installed
---> Package perl-Crypt-SSLeay.x86_64 0:0.64-5.el7 will be installed
---> Package perl-DBI.x86_64 0:1.627-4.el7 will be installed
--> Processing Dependency: perl(RPC::PlServer) >= 0.2001 for package: perl-DBI-1.627-4.el7.x86_64
--> Processing Dependency: perl(RPC::PlClient) >= 0.2000 for package: perl-DBI-1.627-4.el7.x86_64
---> Package perl-DB_File.x86_64 0:1.830-6.el7 will be installed
---> Package perl-Digest-MD5.x86_64 0:2.52-3.el7 will be installed
--> Processing Dependency: perl(Digest::base) >= 1.00 for package: perl-Digest-MD5-2.52-3.el7.x86_64
---> Package perl-Digest-SHA1.x86_64 0:2.13-9.el7 will be installed
---> Package perl-FCGI.x86_64 1:0.74-8.el7 will be installed
---> Package perl-HTML-Form.noarch 0:6.03-6.el7 will be installed
--> Processing Dependency: perl(HTML::TokeParser) for package: perl-HTML-Form-6.03-6.el7.noarch
--> Processing Dependency: perl(URI) for package: perl-HTML-Form-6.03-6.el7.noarch
---> Package perl-HTTP-Async.noarch 0:0.30-2 will be installed
--> Processing Dependency: perl(Net::HTTP::NB) for package: perl-HTTP-Async-0.30-2.noarch
--> Processing Dependency: perl(Net::HTTP) for package: perl-HTTP-Async-0.30-2.noarch
---> Package perl-HTTP-Cookies.noarch 0:6.01-5.el7 will be installed
--> Processing Dependency: perl(HTTP::Date) >= 6 for package: perl-HTTP-Cookies-6.01-5.el7.noarch
---> Package perl-HTTP-Message.noarch 0:6.06-6.el7 will be installed
--> Processing Dependency: perl(LWP::MediaTypes) >= 6 for package: perl-HTTP-Message-6.06-6.el7.noarch
--> Processing Dependency: perl(IO::Uncompress::Bunzip2) >= 2.021 for package: perl-HTTP-Message-6.06-6.el7.noarch
--> Processing Dependency: perl(IO::Compress::Bzip2) >= 2.021 for package: perl-HTTP-Message-6.06-6.el7.noarch
--> Processing Dependency: perl(Encode::Locale) >= 1 for package: perl-HTTP-Message-6.06-6.el7.noarch
--> Processing Dependency: perl(IO::Uncompress::RawInflate) for package: perl-HTTP-Message-6.06-6.el7.noarch
--> Processing Dependency: perl(IO::Uncompress::Inflate) for package: perl-HTTP-Message-6.06-6.el7.noarch
--> Processing Dependency: perl(IO::Uncompress::Gunzip) for package: perl-HTTP-Message-6.06-6.el7.noarch
--> Processing Dependency: perl(IO::HTML) for package: perl-HTTP-Message-6.06-6.el7.noarch
--> Processing Dependency: perl(IO::Compress::Gzip) for package: perl-HTTP-Message-6.06-6.el7.noarch
--> Processing Dependency: perl(IO::Compress::Deflate) for package: perl-HTTP-Message-6.06-6.el7.noarch
--> Processing Dependency: perl(Compress::Raw::Zlib) for package: perl-HTTP-Message-6.06-6.el7.noarch
---> Package perl-IO-Socket-SSL.noarch 0:1.94-7.el7 will be installed
--> Processing Dependency: perl(IO::Socket::IP) >= 0.20 for package: perl-IO-Socket-SSL-1.94-7.el7.noarch
--> Processing Dependency: perl(Net::LibIDN) for package: perl-IO-Socket-SSL-1.94-7.el7.noarch
--> Processing Dependency: perl(Mozilla::CA) for package: perl-IO-Socket-SSL-1.94-7.el7.noarch
---> Package perl-IO-Tty.x86_64 0:1.10-11.el7 will be installed
---> Package perl-JSON.noarch 0:2.59-2.el7 will be installed
---> Package perl-LWP-Protocol-https.noarch 0:6.04-4.el7 will be installed
---> Package perl-Net-DNS.x86_64 0:0.72-6.el7 will be installed
--> Processing Dependency: perl(Digest::HMAC_MD5) >= 1 for package: perl-Net-DNS-0.72-6.el7.x86_64
---> Package perl-Net-HTTPS-NB.noarch 0:0.14-2 will be installed
---> Package perl-Net-SSLeay.x86_64 0:1.55-6.el7 will be installed
---> Package perl-Net-Telnet.noarch 0:3.03-19.el7 will be installed
---> Package perl-Sys-Syslog.x86_64 0:0.33-3.el7 will be installed
---> Package perl-Sys-Virt.x86_64 0:4.5.0-2.el7 will be installed
---> Package perl-TimeDate.noarch 1:2.30-2.el7 will be installed
---> Package perl-XML-LibXML.x86_64 1:2.0018-5.el7 will be installed
--> Processing Dependency: perl(XML::SAX::Exception) for package: 1:perl-XML-LibXML-2.0018-5.el7.x86_64
--> Processing Dependency: perl(XML::SAX::Base) for package: 1:perl-XML-LibXML-2.0018-5.el7.x86_64
---> Package perl-XML-NamespaceSupport.noarch 0:1.11-10.el7 will be installed
---> Package perl-XML-SAX.noarch 0:0.99-9.el7 will be installed
---> Package perl-libwww-perl.noarch 0:6.05-2.el7 will be installed
--> Processing Dependency: perl(WWW::RobotRules) >= 6 for package: perl-libwww-perl-6.05-2.el7.noarch
--> Processing Dependency: perl(HTTP::Negotiate) >= 6 for package: perl-libwww-perl-6.05-2.el7.noarch
--> Processing Dependency: perl(HTTP::Daemon) >= 6 for package: perl-libwww-perl-6.05-2.el7.noarch
--> Processing Dependency: perl(File::Listing) >= 6 for package: perl-libwww-perl-6.05-2.el7.noarch
---> Package tftp.x86_64 0:5.2-22.el7 will be installed
---> Package xCAT-genesis-base-ppc64.noarch 2:2.16.3-snap202110141642 will be installed
---> Package xCAT-genesis-base-x86_64.noarch 2:2.14.5-snap201811190037 will be installed
--> Running transaction check
---> Package bind-license.noarch 32:9.11.4-26.P2.el7 will be updated
---> Package bind-license.noarch 32:9.11.4-26.P2.el7_9.13 will be an update
---> Package bind-utils.x86_64 32:9.11.4-26.P2.el7 will be updated
---> Package bind-utils.x86_64 32:9.11.4-26.P2.el7_9.13 will be an update
---> Package dhclient.x86_64 12:4.2.5-82.el7.centos will be updated
---> Package dhclient.x86_64 12:4.2.5-83.el7.centos.1 will be an update
---> Package net-snmp.x86_64 1:5.7.2-49.el7_9.2 will be installed
---> Package net-snmp-agent-libs.x86_64 1:5.7.2-49.el7_9.2 will be installed
---> Package net-snmp-devel.x86_64 1:5.7.2-49.el7_9.2 will be installed
--> Processing Dependency: tcp_wrappers-devel for package: 1:net-snmp-devel-5.7.2-49.el7_9.2.x86_64
--> Processing Dependency: rpm-devel for package: 1:net-snmp-devel-5.7.2-49.el7_9.2.x86_64
--> Processing Dependency: perl-devel(x86-64) for package: 1:net-snmp-devel-5.7.2-49.el7_9.2.x86_64
--> Processing Dependency: openssl-devel for package: 1:net-snmp-devel-5.7.2-49.el7_9.2.x86_64
--> Processing Dependency: lm_sensors-devel for package: 1:net-snmp-devel-5.7.2-49.el7_9.2.x86_64
--> Processing Dependency: elfutils-libelf-devel for package: 1:net-snmp-devel-5.7.2-49.el7_9.2.x86_64
--> Processing Dependency: elfutils-devel for package: 1:net-snmp-devel-5.7.2-49.el7_9.2.x86_64
---> Package net-snmp-libs.x86_64 1:5.7.2-49.el7 will be updated
---> Package net-snmp-libs.x86_64 1:5.7.2-49.el7_9.2 will be an update
---> Package perl-Compress-Raw-Zlib.x86_64 1:2.061-4.el7 will be installed
---> Package perl-Digest.noarch 0:1.17-245.el7 will be installed
---> Package perl-Digest-HMAC.noarch 0:1.03-5.el7 will be installed
--> Processing Dependency: perl(Digest::SHA) for package: perl-Digest-HMAC-1.03-5.el7.noarch
---> Package perl-Encode-Locale.noarch 0:1.03-5.el7 will be installed
---> Package perl-File-Listing.noarch 0:6.04-7.el7 will be installed
---> Package perl-HTML-Parser.x86_64 0:3.71-4.el7 will be installed
--> Processing Dependency: perl(HTML::Tagset) >= 3 for package: perl-HTML-Parser-3.71-4.el7.x86_64
---> Package perl-HTTP-Daemon.noarch 0:6.01-8.el7 will be installed
---> Package perl-HTTP-Date.noarch 0:6.02-8.el7 will be installed
---> Package perl-HTTP-Negotiate.noarch 0:6.01-5.el7 will be installed
---> Package perl-IO-Compress.noarch 0:2.061-2.el7 will be installed
--> Processing Dependency: perl(Compress::Raw::Bzip2) >= 2.061 for package: perl-IO-Compress-2.061-2.el7.noarch
---> Package perl-IO-HTML.noarch 0:1.00-2.el7 will be installed
---> Package perl-IO-Socket-IP.noarch 0:0.21-5.el7 will be installed
---> Package perl-LWP-MediaTypes.noarch 0:6.02-2.el7 will be installed
---> Package perl-Mozilla-CA.noarch 0:20130114-5.el7 will be installed
---> Package perl-Net-HTTP.noarch 0:6.06-2.el7 will be installed
---> Package perl-Net-LibIDN.x86_64 0:0.12-15.el7 will be installed
---> Package perl-PlRPC.noarch 0:0.2020-14.el7 will be installed
--> Processing Dependency: perl(Net::Daemon) >= 0.13 for package: perl-PlRPC-0.2020-14.el7.noarch
--> Processing Dependency: perl(Net::Daemon::Test) for package: perl-PlRPC-0.2020-14.el7.noarch
--> Processing Dependency: perl(Net::Daemon::Log) for package: perl-PlRPC-0.2020-14.el7.noarch
---> Package perl-URI.noarch 0:1.60-9.el7 will be installed
--> Processing Dependency: perl(Business::ISBN) for package: perl-URI-1.60-9.el7.noarch
---> Package perl-WWW-RobotRules.noarch 0:6.02-5.el7 will be installed
---> Package perl-XML-SAX-Base.noarch 0:1.08-7.el7 will be installed
--> Running transaction check
---> Package elfutils-devel.x86_64 0:0.176-5.el7 will be installed
--> Processing Dependency: pkgconfig(zlib) for package: elfutils-devel-0.176-5.el7.x86_64
--> Processing Dependency: pkgconfig(liblzma) for package: elfutils-devel-0.176-5.el7.x86_64
---> Package elfutils-libelf-devel.x86_64 0:0.176-5.el7 will be installed
---> Package lm_sensors-devel.x86_64 0:3.4.0-8.20160601gitf9185e5.el7 will be installed
---> Package openssl-devel.x86_64 1:1.0.2k-26.el7_9 will be installed
--> Processing Dependency: openssl-libs(x86-64) = 1:1.0.2k-26.el7_9 for package: 1:openssl-devel-1.0.2k-26.el7_9.x86_64
--> Processing Dependency: krb5-devel(x86-64) for package: 1:openssl-devel-1.0.2k-26.el7_9.x86_64
---> Package perl-Business-ISBN.noarch 0:2.06-2.el7 will be installed
--> Processing Dependency: perl(Business::ISBN::Data) >= 20120719.001 for package: perl-Business-ISBN-2.06-2.el7.noarch
---> Package perl-Compress-Raw-Bzip2.x86_64 0:2.061-3.el7 will be installed
---> Package perl-Digest-SHA.x86_64 1:5.85-4.el7 will be installed
---> Package perl-HTML-Tagset.noarch 0:3.20-15.el7 will be installed
---> Package perl-Net-Daemon.noarch 0:0.48-5.el7 will be installed
---> Package perl-devel.x86_64 4:5.16.3-299.el7_9 will be installed
--> Processing Dependency: systemtap-sdt-devel for package: 4:perl-devel-5.16.3-299.el7_9.x86_64
--> Processing Dependency: perl(ExtUtils::ParseXS) for package: 4:perl-devel-5.16.3-299.el7_9.x86_64
--> Processing Dependency: perl(ExtUtils::MakeMaker) for package: 4:perl-devel-5.16.3-299.el7_9.x86_64
--> Processing Dependency: perl(ExtUtils::Installed) for package: 4:perl-devel-5.16.3-299.el7_9.x86_64
--> Processing Dependency: libdb-devel for package: 4:perl-devel-5.16.3-299.el7_9.x86_64
--> Processing Dependency: gdbm-devel for package: 4:perl-devel-5.16.3-299.el7_9.x86_64
---> Package rpm-devel.x86_64 0:4.11.3-48.el7_9 will be installed
--> Processing Dependency: rpm-libs(x86-64) = 4.11.3-48.el7_9 for package: rpm-devel-4.11.3-48.el7_9.x86_64
--> Processing Dependency: rpm-build-libs(x86-64) = 4.11.3-48.el7_9 for package: rpm-devel-4.11.3-48.el7_9.x86_64
--> Processing Dependency: rpm = 4.11.3-48.el7_9 for package: rpm-devel-4.11.3-48.el7_9.x86_64
--> Processing Dependency: popt-devel(x86-64) for package: rpm-devel-4.11.3-48.el7_9.x86_64
---> Package tcp_wrappers-devel.x86_64 0:7.6-77.el7 will be installed
--> Running transaction check
---> Package gdbm-devel.x86_64 0:1.10-8.el7 will be installed
---> Package krb5-devel.x86_64 0:1.15.1-55.el7_9 will be installed
--> Processing Dependency: libkadm5(x86-64) = 1.15.1-55.el7_9 for package: krb5-devel-1.15.1-55.el7_9.x86_64
--> Processing Dependency: krb5-libs(x86-64) = 1.15.1-55.el7_9 for package: krb5-devel-1.15.1-55.el7_9.x86_64
--> Processing Dependency: libverto-devel for package: krb5-devel-1.15.1-55.el7_9.x86_64
--> Processing Dependency: libselinux-devel for package: krb5-devel-1.15.1-55.el7_9.x86_64
--> Processing Dependency: libcom_err-devel for package: krb5-devel-1.15.1-55.el7_9.x86_64
--> Processing Dependency: keyutils-libs-devel for package: krb5-devel-1.15.1-55.el7_9.x86_64
---> Package libdb-devel.x86_64 0:5.3.21-25.el7 will be installed
---> Package openssl-libs.x86_64 1:1.0.2k-19.el7 will be updated
--> Processing Dependency: openssl-libs(x86-64) = 1:1.0.2k-19.el7 for package: 1:openssl-1.0.2k-19.el7.x86_64
---> Package openssl-libs.x86_64 1:1.0.2k-26.el7_9 will be an update
---> Package perl-Business-ISBN-Data.noarch 0:20120719.001-2.el7 will be installed
---> Package perl-ExtUtils-Install.noarch 0:1.58-299.el7_9 will be installed
---> Package perl-ExtUtils-MakeMaker.noarch 0:6.68-3.el7 will be installed
--> Processing Dependency: perl(ExtUtils::Manifest) for package: perl-ExtUtils-MakeMaker-6.68-3.el7.noarch
---> Package perl-ExtUtils-ParseXS.noarch 1:3.18-3.el7 will be installed
---> Package popt-devel.x86_64 0:1.13-16.el7 will be installed
---> Package rpm.x86_64 0:4.11.3-45.el7 will be updated
--> Processing Dependency: rpm = 4.11.3-45.el7 for package: rpm-python-4.11.3-45.el7.x86_64
--> Processing Dependency: rpm = 4.11.3-45.el7 for package: rpm-build-4.11.3-45.el7.x86_64
---> Package rpm.x86_64 0:4.11.3-48.el7_9 will be an update
---> Package rpm-build-libs.x86_64 0:4.11.3-45.el7 will be updated
--> Processing Dependency: rpm-build-libs(x86-64) = 4.11.3-45.el7 for package: rpm-sign-4.11.3-45.el7.x86_64
---> Package rpm-build-libs.x86_64 0:4.11.3-48.el7_9 will be an update
---> Package rpm-libs.x86_64 0:4.11.3-45.el7 will be updated
---> Package rpm-libs.x86_64 0:4.11.3-48.el7_9 will be an update
---> Package systemtap-sdt-devel.x86_64 0:4.0-13.el7 will be installed
---> Package xz-devel.x86_64 0:5.2.2-2.el7_9 will be installed
--> Processing Dependency: xz-libs = 5.2.2-2.el7_9 for package: xz-devel-5.2.2-2.el7_9.x86_64
---> Package zlib-devel.x86_64 0:1.2.7-21.el7_9 will be installed
--> Processing Dependency: zlib = 1.2.7-21.el7_9 for package: zlib-devel-1.2.7-21.el7_9.x86_64
--> Running transaction check
---> Package keyutils-libs-devel.x86_64 0:1.5.8-3.el7 will be installed
---> Package krb5-libs.x86_64 0:1.15.1-50.el7 will be updated
--> Processing Dependency: krb5-libs(x86-64) = 1.15.1-50.el7 for package: krb5-workstation-1.15.1-50.el7.x86_64
---> Package krb5-libs.x86_64 0:1.15.1-55.el7_9 will be an update
---> Package libcom_err-devel.x86_64 0:1.42.9-19.el7 will be installed
---> Package libkadm5.x86_64 0:1.15.1-50.el7 will be updated
---> Package libkadm5.x86_64 0:1.15.1-55.el7_9 will be an update
---> Package libselinux-devel.x86_64 0:2.5-15.el7 will be installed
--> Processing Dependency: libsepol-devel(x86-64) >= 2.5-10 for package: libselinux-devel-2.5-15.el7.x86_64
--> Processing Dependency: pkgconfig(libsepol) for package: libselinux-devel-2.5-15.el7.x86_64
--> Processing Dependency: pkgconfig(libpcre) for package: libselinux-devel-2.5-15.el7.x86_64
---> Package libverto-devel.x86_64 0:0.2.5-4.el7 will be installed
---> Package openssl.x86_64 1:1.0.2k-19.el7 will be updated
---> Package openssl.x86_64 1:1.0.2k-26.el7_9 will be an update
---> Package perl-ExtUtils-Manifest.noarch 0:1.61-244.el7 will be installed
---> Package rpm-build.x86_64 0:4.11.3-45.el7 will be updated
---> Package rpm-build.x86_64 0:4.11.3-48.el7_9 will be an update
---> Package rpm-python.x86_64 0:4.11.3-45.el7 will be updated
---> Package rpm-python.x86_64 0:4.11.3-48.el7_9 will be an update
---> Package rpm-sign.x86_64 0:4.11.3-45.el7 will be updated
---> Package rpm-sign.x86_64 0:4.11.3-48.el7_9 will be an update
---> Package xz-libs.x86_64 0:5.2.2-1.el7 will be updated
--> Processing Dependency: xz-libs = 5.2.2-1.el7 for package: xz-5.2.2-1.el7.x86_64
---> Package xz-libs.x86_64 0:5.2.2-2.el7_9 will be an update
---> Package zlib.x86_64 0:1.2.7-18.el7 will be updated
---> Package zlib.x86_64 0:1.2.7-21.el7_9 will be an update
--> Running transaction check
---> Package krb5-workstation.x86_64 0:1.15.1-50.el7 will be updated
---> Package krb5-workstation.x86_64 0:1.15.1-55.el7_9 will be an update
---> Package libsepol-devel.x86_64 0:2.5-10.el7 will be installed
---> Package pcre-devel.x86_64 0:8.32-17.el7 will be installed
---> Package xz.x86_64 0:5.2.2-1.el7 will be updated
---> Package xz.x86_64 0:5.2.2-2.el7_9 will be an update
--> Finished Dependency Resolution

Dependencies Resolved

=============================================================================================================================================================================================
 Package                                               Arch                             Version                                                    Repository                           Size
=============================================================================================================================================================================================
Installing:
 xCAT                                                  x86_64                           2.16.5-snap202303030907                                    xcat-core                           255 k
Installing for dependencies:
 bind                                                  x86_64                           32:9.11.4-26.P2.el7_9.13                                   updates                             2.3 M
 dhcp                                                  x86_64                           12:4.2.5-83.el7.centos.1                                   updates                             515 k
 elfutils-devel                                        x86_64                           0.176-5.el7                                                base                                 90 k
 elfutils-libelf-devel                                 x86_64                           0.176-5.el7                                                base                                 40 k
 elilo-xcat                                            noarch                           3.14-6                                                     xcat-dep                             68 k
 gdbm-devel                                            x86_64                           1.10-8.el7                                                 base                                 47 k
 goconserver                                           x86_64                           0.3.3-snap202011021058                                     xcat-dep                            7.8 M
 grub2-xcat                                            noarch                           2.02-0.76.el7.1.snap201905160255                           xcat-dep                            1.9 M
 httpd                                                 x86_64                           2.4.6-99.el7.centos.1                                      updates                             2.7 M
 httpd-tools                                           x86_64                           2.4.6-99.el7.centos.1                                      updates                              94 k
 ipmitool-xcat                                         x86_64                           1.8.18-3                                                   xcat-dep                            328 k
 keyutils-libs-devel                                   x86_64                           1.5.8-3.el7                                                base                                 37 k
 krb5-devel                                            x86_64                           1.15.1-55.el7_9                                            updates                             273 k
 ksh                                                   x86_64                           20120801-144.el7_9                                         updates                             885 k
 libcom_err-devel                                      x86_64                           1.42.9-19.el7                                              base                                 32 k
 libdb-devel                                           x86_64                           5.3.21-25.el7                                              base                                 39 k
 libselinux-devel                                      x86_64                           2.5-15.el7                                                 base                                187 k
 libsepol-devel                                        x86_64                           2.5-10.el7                                                 base                                 77 k
 libverto-devel                                        x86_64                           0.2.5-4.el7                                                base                                 12 k
 lm_sensors-devel                                      x86_64                           3.4.0-8.20160601gitf9185e5.el7                             base                                 27 k
 mailcap                                               noarch                           2.1.41-2.el7                                               base                                 31 k
 net-snmp                                              x86_64                           1:5.7.2-49.el7_9.2                                         updates                             325 k
 net-snmp-agent-libs                                   x86_64                           1:5.7.2-49.el7_9.2                                         updates                             707 k
 net-snmp-devel                                        x86_64                           1:5.7.2-49.el7_9.2                                         updates                             260 k
 net-snmp-perl                                         x86_64                           1:5.7.2-49.el7_9.2                                         updates                             339 k
 nmap                                                  x86_64                           2:6.40-19.el7                                              base                                3.9 M
 openssl-devel                                         x86_64                           1:1.0.2k-26.el7_9                                          updates                             1.5 M
 pcre-devel                                            x86_64                           8.32-17.el7                                                base                                480 k
 perl-Business-ISBN                                    noarch                           2.06-2.el7                                                 base                                 25 k
 perl-Business-ISBN-Data                               noarch                           20120719.001-2.el7                                         base                                 24 k
 perl-CGI                                              noarch                           3.63-4.el7                                                 base                                250 k
 perl-Compress-Raw-Bzip2                               x86_64                           2.061-3.el7                                                base                                 32 k
 perl-Compress-Raw-Zlib                                x86_64                           1:2.061-4.el7                                              base                                 57 k
 perl-Crypt-CBC                                        noarch                           2.33-2.el7                                                 base                                 32 k
 perl-Crypt-Rijndael                                   x86_64                           1.12-1.el7                                                 epel                                 28 k
 perl-Crypt-SSLeay                                     x86_64                           0.64-5.el7                                                 base                                 58 k
 perl-DBD-SQLite                                       x86_64                           1.39-3.el7                                                 base                                1.3 M
 perl-DBI                                              x86_64                           1.627-4.el7                                                base                                802 k
 perl-DB_File                                          x86_64                           1.830-6.el7                                                base                                 74 k
 perl-Digest                                           noarch                           1.17-245.el7                                               base                                 23 k
 perl-Digest-HMAC                                      noarch                           1.03-5.el7                                                 base                                 16 k
 perl-Digest-MD5                                       x86_64                           2.52-3.el7                                                 base                                 30 k
 perl-Digest-SHA                                       x86_64                           1:5.85-4.el7                                               base                                 58 k
 perl-Digest-SHA1                                      x86_64                           2.13-9.el7                                                 base                                 50 k
 perl-Encode-Locale                                    noarch                           1.03-5.el7                                                 base                                 16 k
 perl-Expect                                           noarch                           1.21-14.el7                                                epel                                 75 k
 perl-ExtUtils-Install                                 noarch                           1.58-299.el7_9                                             updates                              75 k
 perl-ExtUtils-MakeMaker                               noarch                           6.68-3.el7                                                 base                                275 k
 perl-ExtUtils-Manifest                                noarch                           1.61-244.el7                                               base                                 31 k
 perl-ExtUtils-ParseXS                                 noarch                           1:3.18-3.el7                                               base                                 77 k
 perl-FCGI                                             x86_64                           1:0.74-8.el7                                               base                                 42 k
 perl-File-Listing                                     noarch                           6.04-7.el7                                                 base                                 13 k
 perl-HTML-Form                                        noarch                           6.03-6.el7                                                 epel                                 28 k
 perl-HTML-Parser                                      x86_64                           3.71-4.el7                                                 base                                115 k
 perl-HTML-Tagset                                      noarch                           3.20-15.el7                                                base                                 18 k
 perl-HTTP-Async                                       noarch                           0.30-2                                                     xcat-dep                             19 k
 perl-HTTP-Cookies                                     noarch                           6.01-5.el7                                                 base                                 26 k
 perl-HTTP-Daemon                                      noarch                           6.01-8.el7                                                 base                                 21 k
 perl-HTTP-Date                                        noarch                           6.02-8.el7                                                 base                                 14 k
 perl-HTTP-Message                                     noarch                           6.06-6.el7                                                 base                                 82 k
 perl-HTTP-Negotiate                                   noarch                           6.01-5.el7                                                 base                                 17 k
 perl-IO-Compress                                      noarch                           2.061-2.el7                                                base                                260 k
 perl-IO-HTML                                          noarch                           1.00-2.el7                                                 base                                 23 k
 perl-IO-Socket-IP                                     noarch                           0.21-5.el7                                                 base                                 36 k
 perl-IO-Socket-SSL                                    noarch                           1.94-7.el7                                                 base                                115 k
 perl-IO-Stty                                          noarch                           0.03-1                                                     xcat-dep                             13 k
 perl-IO-Tty                                           x86_64                           1.10-11.el7                                                base                                 42 k
 perl-JSON                                             noarch                           2.59-2.el7                                                 base                                 96 k
 perl-LWP-MediaTypes                                   noarch                           6.02-2.el7                                                 base                                 24 k
 perl-LWP-Protocol-https                               noarch                           6.04-4.el7                                                 base                                 11 k
 perl-Mozilla-CA                                       noarch                           20130114-5.el7                                             base                                 11 k
 perl-Net-DNS                                          x86_64                           0.72-6.el7                                                 base                                308 k
 perl-Net-Daemon                                       noarch                           0.48-5.el7                                                 base                                 51 k
 perl-Net-HTTP                                         noarch                           6.06-2.el7                                                 base                                 29 k
 perl-Net-HTTPS-NB                                     noarch                           0.14-2                                                     xcat-dep                            9.8 k
 perl-Net-LibIDN                                       x86_64                           0.12-15.el7                                                base                                 28 k
 perl-Net-SSLeay                                       x86_64                           1.55-6.el7                                                 base                                285 k
 perl-Net-Telnet                                       noarch                           3.03-19.el7                                                base                                 56 k
 perl-PlRPC                                            noarch                           0.2020-14.el7                                              base                                 36 k
 perl-Sys-Syslog                                       x86_64                           0.33-3.el7                                                 base                                 42 k
 perl-Sys-Virt                                         x86_64                           4.5.0-2.el7                                                base                                296 k
 perl-TimeDate                                         noarch                           1:2.30-2.el7                                               base                                 52 k
 perl-URI                                              noarch                           1.60-9.el7                                                 base                                106 k
 perl-WWW-RobotRules                                   noarch                           6.02-5.el7                                                 base                                 18 k
 perl-XML-LibXML                                       x86_64                           1:2.0018-5.el7                                             base                                373 k
 perl-XML-NamespaceSupport                             noarch                           1.11-10.el7                                                base                                 18 k
 perl-XML-SAX                                          noarch                           0.99-9.el7                                                 base                                 63 k
 perl-XML-SAX-Base                                     noarch                           1.08-7.el7                                                 base                                 32 k
 perl-XML-Simple                                       noarch                           2.20-5.el7                                                 base                                 74 k
 perl-devel                                            x86_64                           4:5.16.3-299.el7_9                                         updates                             454 k
 perl-libwww-perl                                      noarch                           6.05-2.el7                                                 base                                205 k
 perl-xCAT                                             noarch                           4:2.16.5-snap202303030907                                  xcat-core                           614 k
 popt-devel                                            x86_64                           1.13-16.el7                                                base                                 22 k
 rpm-devel                                             x86_64                           4.11.3-48.el7_9                                            updates                             108 k
 syslinux                                              x86_64                           4.05-15.el7                                                base                                990 k
 syslinux-xcat                                         noarch                           3.86-2                                                     xcat-dep                            499 k
 systemtap-sdt-devel                                   x86_64                           4.0-13.el7                                                 base                                 76 k
 tcp_wrappers-devel                                    x86_64                           7.6-77.el7                                                 base                                 17 k
 tftp                                                  x86_64                           5.2-22.el7                                                 base                                 38 k
 tftp-server                                           x86_64                           5.2-22.el7                                                 base                                 47 k
 xCAT-buildkit                                         noarch                           4:2.16.5-snap202303030907                                  xcat-core                            71 k
 xCAT-client                                           noarch                           4:2.16.5-snap202303030907                                  xcat-core                           446 k
 xCAT-genesis-base-ppc64                               noarch                           2:2.16.3-snap202110141642                                  xcat-dep                            106 M
 xCAT-genesis-base-x86_64                              noarch                           2:2.14.5-snap201811190037                                  xcat-dep                             96 M
 xCAT-genesis-scripts-ppc64                            noarch                           1:2.16.5-snap202303030907                                  xcat-core                            63 k
 xCAT-genesis-scripts-x86_64                           noarch                           1:2.16.5-snap202303030907                                  xcat-core                            63 k
 xCAT-probe                                            noarch                           4:2.16.5-snap202303030907                                  xcat-core                            91 k
 xCAT-server                                           noarch                           4:2.16.5-snap202303030907                                  xcat-core                           1.8 M
 xnba-undi                                             noarch                           1.21.1-1                                                   xcat-dep                            169 k
 xz-devel                                              x86_64                           5.2.2-2.el7_9                                              updates                              46 k
 zlib-devel                                            x86_64                           1.2.7-21.el7_9                                             updates                              50 k
Updating for dependencies:
 bind-libs                                             x86_64                           32:9.11.4-26.P2.el7_9.13                                   updates                             158 k
 bind-libs-lite                                        x86_64                           32:9.11.4-26.P2.el7_9.13                                   updates                             1.1 M
 bind-license                                          noarch                           32:9.11.4-26.P2.el7_9.13                                   updates                              92 k
 bind-utils                                            x86_64                           32:9.11.4-26.P2.el7_9.13                                   updates                             262 k
 dhclient                                              x86_64                           12:4.2.5-83.el7.centos.1                                   updates                             286 k
 dhcp-common                                           x86_64                           12:4.2.5-83.el7.centos.1                                   updates                             177 k
 dhcp-libs                                             x86_64                           12:4.2.5-83.el7.centos.1                                   updates                             133 k
 krb5-libs                                             x86_64                           1.15.1-55.el7_9                                            updates                             810 k
 krb5-workstation                                      x86_64                           1.15.1-55.el7_9                                            updates                             821 k
 libkadm5                                              x86_64                           1.15.1-55.el7_9                                            updates                             180 k
 net-snmp-libs                                         x86_64                           1:5.7.2-49.el7_9.2                                         updates                             752 k
 openssl                                               x86_64                           1:1.0.2k-26.el7_9                                          updates                             494 k
 openssl-libs                                          x86_64                           1:1.0.2k-26.el7_9                                          updates                             1.2 M
 rpm                                                   x86_64                           4.11.3-48.el7_9                                            updates                             1.2 M
 rpm-build                                             x86_64                           4.11.3-48.el7_9                                            updates                             150 k
 rpm-build-libs                                        x86_64                           4.11.3-48.el7_9                                            updates                             108 k
 rpm-libs                                              x86_64                           4.11.3-48.el7_9                                            updates                             279 k
 rpm-python                                            x86_64                           4.11.3-48.el7_9                                            updates                              84 k
 rpm-sign                                              x86_64                           4.11.3-48.el7_9                                            updates                              49 k
 xz                                                    x86_64                           5.2.2-2.el7_9                                              updates                             229 k
 xz-libs                                               x86_64                           5.2.2-2.el7_9                                              updates                             103 k
 zlib                                                  x86_64                           1.2.7-21.el7_9                                             updates                              90 k

Transaction Summary
=============================================================================================================================================================================================
Install  1 Package  (+111 Dependent packages)
Upgrade             (  22 Dependent packages)

Total download size: 249 M
Downloading packages:
No Presto metadata available for updates
(1/134): bind-libs-9.11.4-26.P2.el7_9.13.x86_64.rpm                                                                                                                   | 158 kB  00:00:00     
(2/134): bind-9.11.4-26.P2.el7_9.13.x86_64.rpm                                                                                                                        | 2.3 MB  00:00:00     
(3/134): bind-libs-lite-9.11.4-26.P2.el7_9.13.x86_64.rpm                                                                                                              | 1.1 MB  00:00:00     
(4/134): bind-utils-9.11.4-26.P2.el7_9.13.x86_64.rpm                                                                                                                  | 262 kB  00:00:00     
(5/134): dhclient-4.2.5-83.el7.centos.1.x86_64.rpm                                                                                                                    | 286 kB  00:00:00     
(6/134): bind-license-9.11.4-26.P2.el7_9.13.noarch.rpm                                                                                                                |  92 kB  00:00:00     
(7/134): dhcp-common-4.2.5-83.el7.centos.1.x86_64.rpm                                                                                                                 | 177 kB  00:00:00     
(8/134): dhcp-4.2.5-83.el7.centos.1.x86_64.rpm                                                                                                                        | 515 kB  00:00:00     
(9/134): dhcp-libs-4.2.5-83.el7.centos.1.x86_64.rpm                                                                                                                   | 133 kB  00:00:00     
(10/134): elfutils-libelf-devel-0.176-5.el7.x86_64.rpm                                                                                                                |  40 kB  00:00:00     
(11/134): gdbm-devel-1.10-8.el7.x86_64.rpm                                                                                                                            |  47 kB  00:00:00     
(12/134): elfutils-devel-0.176-5.el7.x86_64.rpm                                                                                                                       |  90 kB  00:00:00     
warning: /var/cache/yum/x86_64/7/xcat-dep/packages/elilo-xcat-3.14-6.noarch.rpm: Header V4 RSA/SHA1 Signature, key ID ca548a47: NOKEY                      ] 2.7 MB/s | 5.3 MB  00:01:30 ETA 
Public key for elilo-xcat-3.14-6.noarch.rpm is not installed
(13/134): elilo-xcat-3.14-6.noarch.rpm                                                                                                                                |  68 kB  00:00:01     
(14/134): httpd-tools-2.4.6-99.el7.centos.1.x86_64.rpm                                                                                                                |  94 kB  00:00:00     
(15/134): httpd-2.4.6-99.el7.centos.1.x86_64.rpm                                                                                                                      | 2.7 MB  00:00:00     
(16/134): grub2-xcat-2.02-0.76.el7.1.snap201905160255.noarch.rpm                                                                                                      | 1.9 MB  00:00:02     
(17/134): keyutils-libs-devel-1.5.8-3.el7.x86_64.rpm                                                                                                                  |  37 kB  00:00:00     
(18/134): krb5-devel-1.15.1-55.el7_9.x86_64.rpm                                                                                                                       | 273 kB  00:00:00     
(19/134): ipmitool-xcat-1.8.18-3.x86_64.rpm                                                                                                                           | 328 kB  00:00:00     
(20/134): krb5-libs-1.15.1-55.el7_9.x86_64.rpm                                                                                                                        | 810 kB  00:00:00     
(21/134): libcom_err-devel-1.42.9-19.el7.x86_64.rpm                                                                                                                   |  32 kB  00:00:00     
(22/134): krb5-workstation-1.15.1-55.el7_9.x86_64.rpm                                                                                                                 | 821 kB  00:00:00     
(23/134): libkadm5-1.15.1-55.el7_9.x86_64.rpm                                                                                                                         | 180 kB  00:00:00     
(24/134): libdb-devel-5.3.21-25.el7.x86_64.rpm                                                                                                                        |  39 kB  00:00:00     
(25/134): libselinux-devel-2.5-15.el7.x86_64.rpm                                                                                                                      | 187 kB  00:00:00     
(26/134): libverto-devel-0.2.5-4.el7.x86_64.rpm                                                                                                                       |  12 kB  00:00:00     
(27/134): lm_sensors-devel-3.4.0-8.20160601gitf9185e5.el7.x86_64.rpm                                                                                                  |  27 kB  00:00:00     
(28/134): libsepol-devel-2.5-10.el7.x86_64.rpm                                                                                                                        |  77 kB  00:00:00     
(29/134): mailcap-2.1.41-2.el7.noarch.rpm                                                                                                                             |  31 kB  00:00:00     
(30/134): ksh-20120801-144.el7_9.x86_64.rpm                                                                                                                           | 885 kB  00:00:00     
(31/134): net-snmp-5.7.2-49.el7_9.2.x86_64.rpm                                                                                                                        | 325 kB  00:00:00     
(32/134): net-snmp-devel-5.7.2-49.el7_9.2.x86_64.rpm                                                                                                                  | 260 kB  00:00:00     
(33/134): net-snmp-agent-libs-5.7.2-49.el7_9.2.x86_64.rpm                                                                                                             | 707 kB  00:00:00     
(34/134): net-snmp-perl-5.7.2-49.el7_9.2.x86_64.rpm                                                                                                                   | 339 kB  00:00:00     
(35/134): nmap-6.40-19.el7.x86_64.rpm                                                                                                                                 | 3.9 MB  00:00:00     
(36/134): openssl-1.0.2k-26.el7_9.x86_64.rpm                                                                                                                          | 494 kB  00:00:00     
(37/134): net-snmp-libs-5.7.2-49.el7_9.2.x86_64.rpm                                                                                                                   | 752 kB  00:00:01     
(38/134): perl-Business-ISBN-2.06-2.el7.noarch.rpm                                                                                                                    |  25 kB  00:00:00     
(39/134): perl-Business-ISBN-Data-20120719.001-2.el7.noarch.rpm                                                                                                       |  24 kB  00:00:00     
(40/134): openssl-devel-1.0.2k-26.el7_9.x86_64.rpm                                                                                                                    | 1.5 MB  00:00:00     
(41/134): perl-CGI-3.63-4.el7.noarch.rpm                                                                                                                              | 250 kB  00:00:00     
(42/134): perl-Compress-Raw-Bzip2-2.061-3.el7.x86_64.rpm                                                                                                              |  32 kB  00:00:00     
(43/134): perl-Compress-Raw-Zlib-2.061-4.el7.x86_64.rpm                                                                                                               |  57 kB  00:00:00     
(44/134): perl-Crypt-CBC-2.33-2.el7.noarch.rpm                                                                                                                        |  32 kB  00:00:00     
(45/134): pcre-devel-8.32-17.el7.x86_64.rpm                                                                                                                           | 480 kB  00:00:00     
(46/134): perl-Crypt-SSLeay-0.64-5.el7.x86_64.rpm                                                                                                                     |  58 kB  00:00:00     
(47/134): openssl-libs-1.0.2k-26.el7_9.x86_64.rpm                                                                                                                     | 1.2 MB  00:00:00     
(48/134): perl-DBI-1.627-4.el7.x86_64.rpm                                                                                                                             | 802 kB  00:00:00     
(49/134): perl-DB_File-1.830-6.el7.x86_64.rpm                                                                                                                         |  74 kB  00:00:00     
(50/134): perl-DBD-SQLite-1.39-3.el7.x86_64.rpm                                                                                                                       | 1.3 MB  00:00:00     
(51/134): perl-Digest-1.17-245.el7.noarch.rpm                                                                                                                         |  23 kB  00:00:00     
(52/134): perl-Digest-MD5-2.52-3.el7.x86_64.rpm                                                                                                                       |  30 kB  00:00:00     
(53/134): perl-Digest-HMAC-1.03-5.el7.noarch.rpm                                                                                                                      |  16 kB  00:00:00     
(54/134): perl-Digest-SHA-5.85-4.el7.x86_64.rpm                                                                                                                       |  58 kB  00:00:00     
(55/134): perl-Digest-SHA1-2.13-9.el7.x86_64.rpm                                                                                                                      |  50 kB  00:00:00     
(56/134): perl-Encode-Locale-1.03-5.el7.noarch.rpm                                                                                                                    |  16 kB  00:00:00     
warning: /var/cache/yum/x86_64/7/epel/packages/perl-Crypt-Rijndael-1.12-1.el7.x86_64.rpm: Header V3 RSA/SHA256 Signature, key ID 352c64e5: NOKEY           ] 3.8 MB/s |  32 MB  00:00:56 ETA 
Public key for perl-Crypt-Rijndael-1.12-1.el7.x86_64.rpm is not installed
(57/134): perl-Crypt-Rijndael-1.12-1.el7.x86_64.rpm                                                                                                                   |  28 kB  00:00:01     
(58/134): perl-ExtUtils-Install-1.58-299.el7_9.noarch.rpm                                                                                                             |  75 kB  00:00:00     
(59/134): perl-ExtUtils-MakeMaker-6.68-3.el7.noarch.rpm                                                                                                               | 275 kB  00:00:00     
(60/134): perl-ExtUtils-Manifest-1.61-244.el7.noarch.rpm                                                                                                              |  31 kB  00:00:00     
(61/134): perl-ExtUtils-ParseXS-3.18-3.el7.noarch.rpm                                                                                                                 |  77 kB  00:00:00     
(62/134): perl-File-Listing-6.04-7.el7.noarch.rpm                                                                                                                     |  13 kB  00:00:00     
(63/134): perl-FCGI-0.74-8.el7.x86_64.rpm                                                                                                                             |  42 kB  00:00:00     
(64/134): perl-HTML-Tagset-3.20-15.el7.noarch.rpm                                                                                                                     |  18 kB  00:00:00     
(65/134): perl-HTML-Parser-3.71-4.el7.x86_64.rpm                                                                                                                      | 115 kB  00:00:00     
(66/134): perl-HTTP-Cookies-6.01-5.el7.noarch.rpm                                                                                                                     |  26 kB  00:00:00     
(67/134): perl-HTTP-Daemon-6.01-8.el7.noarch.rpm                                                                                                                      |  21 kB  00:00:00     
(68/134): perl-HTML-Form-6.03-6.el7.noarch.rpm                                                                                                                        |  28 kB  00:00:00     
(69/134): perl-HTTP-Date-6.02-8.el7.noarch.rpm                                                                                                                        |  14 kB  00:00:00     
perl-Expect-1.21-14.el7.noarch FAILED                                          
https://mirror.hostart.az/fedora-epel/7/x86_64/Packages/p/perl-Expect-1.21-14.el7.noarch.rpm: [Errno 14] curl#60 - "Peer's Certificate has expired."       ] 3.8 MB/s |  33 MB  00:00:56 ETA 
Trying other mirror.
(70/134): perl-HTTP-Negotiate-6.01-5.el7.noarch.rpm                                                                                                                   |  17 kB  00:00:00     
(71/134): perl-HTTP-Message-6.06-6.el7.noarch.rpm                                                                                                                     |  82 kB  00:00:00     
(72/134): perl-IO-Compress-2.061-2.el7.noarch.rpm                                                                                                                     | 260 kB  00:00:00     
(73/134): perl-IO-HTML-1.00-2.el7.noarch.rpm                                                                                                                          |  23 kB  00:00:00     
(74/134): perl-IO-Socket-IP-0.21-5.el7.noarch.rpm                                                                                                                     |  36 kB  00:00:00     
(75/134): perl-IO-Socket-SSL-1.94-7.el7.noarch.rpm                                                                                                                    | 115 kB  00:00:00     
(76/134): perl-HTTP-Async-0.30-2.noarch.rpm                                                                                                                           |  19 kB  00:00:00     
(77/134): perl-IO-Tty-1.10-11.el7.x86_64.rpm                                                                                                                          |  42 kB  00:00:00     
(78/134): perl-LWP-MediaTypes-6.02-2.el7.noarch.rpm                                                                                                                   |  24 kB  00:00:00     
(79/134): perl-LWP-Protocol-https-6.04-4.el7.noarch.rpm                                                                                                               |  11 kB  00:00:00     
(80/134): perl-Mozilla-CA-20130114-5.el7.noarch.rpm                                                                                                                   |  11 kB  00:00:00     
(81/134): perl-IO-Stty-0.03-1.noarch.rpm                                                                                                                              |  13 kB  00:00:00     
(82/134): perl-Net-DNS-0.72-6.el7.x86_64.rpm                                                                                                                          | 308 kB  00:00:00     
(83/134): perl-JSON-2.59-2.el7.noarch.rpm                                                                                                                             |  96 kB  00:00:00     
(84/134): perl-Net-Daemon-0.48-5.el7.noarch.rpm                                                                                                                       |  51 kB  00:00:00     
(85/134): perl-Net-LibIDN-0.12-15.el7.x86_64.rpm                                                                                                                      |  28 kB  00:00:00     
(86/134): perl-Net-SSLeay-1.55-6.el7.x86_64.rpm                                                                                                                       | 285 kB  00:00:00     
(87/134): perl-Net-Telnet-3.03-19.el7.noarch.rpm                                                                                                                      |  56 kB  00:00:00     
(88/134): perl-Net-HTTPS-NB-0.14-2.noarch.rpm                                                                                                                         | 9.8 kB  00:00:00     
(89/134): perl-PlRPC-0.2020-14.el7.noarch.rpm                                                                                                                         |  36 kB  00:00:00     
(90/134): perl-Net-HTTP-6.06-2.el7.noarch.rpm                                                                                                                         |  29 kB  00:00:00     
(91/134): perl-Sys-Syslog-0.33-3.el7.x86_64.rpm                                                                                                                       |  42 kB  00:00:00     
(92/134): perl-TimeDate-2.30-2.el7.noarch.rpm                                                                                                                         |  52 kB  00:00:00     
(93/134): perl-URI-1.60-9.el7.noarch.rpm                                                                                                                              | 106 kB  00:00:00     
(94/134): perl-WWW-RobotRules-6.02-5.el7.noarch.rpm                                                                                                                   |  18 kB  00:00:00     
(95/134): perl-Sys-Virt-4.5.0-2.el7.x86_64.rpm                                                                                                                        | 296 kB  00:00:00     
(96/134): perl-XML-LibXML-2.0018-5.el7.x86_64.rpm                                                                                                                     | 373 kB  00:00:00     
(97/134): perl-XML-NamespaceSupport-1.11-10.el7.noarch.rpm                                                                                                            |  18 kB  00:00:00     
(98/134): perl-XML-SAX-0.99-9.el7.noarch.rpm                                                                                                                          |  63 kB  00:00:00     
(99/134): perl-XML-Simple-2.20-5.el7.noarch.rpm                                                                                                                       |  74 kB  00:00:00     
(100/134): perl-XML-SAX-Base-1.08-7.el7.noarch.rpm                                                                                                                    |  32 kB  00:00:00     
(101/134): popt-devel-1.13-16.el7.x86_64.rpm                                                                                                                          |  22 kB  00:00:00     
(102/134): perl-libwww-perl-6.05-2.el7.noarch.rpm                                                                                                                     | 205 kB  00:00:00     
(103/134): perl-devel-5.16.3-299.el7_9.x86_64.rpm                                                                                                                     | 454 kB  00:00:00     
(104/134): rpm-build-4.11.3-48.el7_9.x86_64.rpm                                                                                                                       | 150 kB  00:00:00     
(105/134): rpm-build-libs-4.11.3-48.el7_9.x86_64.rpm                                                                                                                  | 108 kB  00:00:00     
(106/134): rpm-devel-4.11.3-48.el7_9.x86_64.rpm                                                                                                                       | 108 kB  00:00:00     
(107/134): rpm-libs-4.11.3-48.el7_9.x86_64.rpm                                                                                                                        | 279 kB  00:00:00     
(108/134): rpm-python-4.11.3-48.el7_9.x86_64.rpm                                                                                                                      |  84 kB  00:00:00     
(109/134): rpm-sign-4.11.3-48.el7_9.x86_64.rpm                                                                                                                        |  49 kB  00:00:00     
(110/134): rpm-4.11.3-48.el7_9.x86_64.rpm                                                                                                                             | 1.2 MB  00:00:01     
(111/134): syslinux-4.05-15.el7.x86_64.rpm                                                                                                                            | 990 kB  00:00:00     
(112/134): tcp_wrappers-devel-7.6-77.el7.x86_64.rpm                                                                                                                   |  17 kB  00:00:00     
(113/134): systemtap-sdt-devel-4.0-13.el7.x86_64.rpm                                                                                                                  |  76 kB  00:00:00     
(114/134): tftp-5.2-22.el7.x86_64.rpm                                                                                                                                 |  38 kB  00:00:00     
(115/134): tftp-server-5.2-22.el7.x86_64.rpm                                                                                                                          |  47 kB  00:00:00     
(116/134): goconserver-0.3.3-snap202011021058.x86_64.rpm                                                                                                              | 7.8 MB  00:00:11     
Public key for perl-xCAT-2.16.5-snap202303030907.noarch.rpm is not installed
(117/134): perl-xCAT-2.16.5-snap202303030907.noarch.rpm                                                                                                               | 614 kB  00:00:01     
(118/134): xCAT-buildkit-2.16.5-snap202303030907.noarch.rpm                                                                                                           |  71 kB  00:00:00     
(119/134): xCAT-2.16.5-snap202303030907.x86_64.rpm                                                                                                                    | 255 kB  00:00:01     
(120/134): xCAT-client-2.16.5-snap202303030907.noarch.rpm                                                                                                             | 446 kB  00:00:01     
(121/134): syslinux-xcat-3.86-2.noarch.rpm                                                                                                                            | 499 kB  00:00:02     
(122/134): xCAT-genesis-scripts-ppc64-2.16.5-snap202303030907.noarch.rpm                                                                                              |  63 kB  00:00:01     
(123/134): xCAT-probe-2.16.5-snap202303030907.noarch.rpm                                                                                                              |  91 kB  00:00:03     
(124/134): xCAT-genesis-scripts-x86_64-2.16.5-snap202303030907.noarch.rpm                                                                                             |  63 kB  00:00:08     
(125/134): xCAT-server-2.16.5-snap202303030907.noarch.rpm                                                                                                             | 1.8 MB  00:00:10     
(126/134): xCAT-genesis-base-ppc64-2.16.3-snap202110141642.noarch.rpm                                                                                                 | 106 MB  00:00:34     
(127/134): xz-devel-5.2.2-2.el7_9.x86_64.rpm                                                                                                                          |  46 kB  00:00:00     
(128/134): xz-libs-5.2.2-2.el7_9.x86_64.rpm                                                                                                                           | 103 kB  00:00:00     
(129/134): xnba-undi-1.21.1-1.noarch.rpm                                                                                                                              | 169 kB  00:00:00     
(130/134): zlib-1.2.7-21.el7_9.x86_64.rpm                                                                                                                             |  90 kB  00:00:00     
(131/134): zlib-devel-1.2.7-21.el7_9.x86_64.rpm                                                                                                                       |  50 kB  00:00:00     
(132/134): perl-Expect-1.21-14.el7.noarch.rpm                                                                                                                         |  75 kB  00:00:00     
xz-5.2.2-2.el7_9.x86_64.rpm    FAILED                                           91% [===============================================================-      ] 476 kB/s | 226 MB  00:00:47 ETA 
http://centos.excellmedia.net/7.9.2009/updates/x86_64/Packages/xz-5.2.2-2.el7_9.x86_64.rpm: [Errno 12] Timeout on http://centos.excellmedia.net/7.9.2009/updates/x86_64/Packages/xz-5.2.2-2.el7_9.x86_64.rpm: (28, 'Operation too slow. Less than 1000 bytes/sec transferred the last 30 seconds')
Trying other mirror.
(133/134): xz-5.2.2-2.el7_9.x86_64.rpm                                                                                                                                | 229 kB  00:00:00     
(134/134): xCAT-genesis-base-x86_64-2.14.5-snap201811190037.noarch.rpm                                                                                                |  96 MB  00:01:26     
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Total                                                                                                                                                        2.5 MB/s | 249 MB  00:01:40     
Retrieving key from http://xcat.org/files/xcat/repos/yum/latest/xcat-core/repodata/repomd.xml.key
Importing GPG key 0xCA548A47:
 Userid     : "xCAT Automatic Signing Key <xcat@cn.ibm.com>"
 Fingerprint: f2a2 306f 7eb3 3463 487f 7b84 6858 3856 ca54 8a47
 From       : http://xcat.org/files/xcat/repos/yum/latest/xcat-core/repodata/repomd.xml.key
Retrieving key from file:///etc/pki/rpm-gpg/RPM-GPG-KEY-EPEL-7
Importing GPG key 0x352C64E5:
 Userid     : "Fedora EPEL (7) <epel@fedoraproject.org>"
 Fingerprint: 91e9 7d7c 4a5e 96f1 7f3e 888f 6a2f aea2 352c 64e5
 Package    : epel-release-7-11.noarch (@extras)
 From       : /etc/pki/rpm-gpg/RPM-GPG-KEY-EPEL-7
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  Updating   : zlib-1.2.7-21.el7_9.x86_64                                                                                                                                              1/156 
  Updating   : krb5-libs-1.15.1-55.el7_9.x86_64                                                                                                                                        2/156 
  Updating   : 1:openssl-libs-1.0.2k-26.el7_9.x86_64                                                                                                                                   3/156 
  Updating   : xz-libs-5.2.2-2.el7_9.x86_64                                                                                                                                            4/156 
  Updating   : rpm-4.11.3-48.el7_9.x86_64                                                                                                                                              5/156 
  Updating   : rpm-libs-4.11.3-48.el7_9.x86_64                                                                                                                                         6/156 
  Updating   : rpm-build-libs-4.11.3-48.el7_9.x86_64                                                                                                                                   7/156 
  Updating   : 1:net-snmp-libs-5.7.2-49.el7_9.2.x86_64                                                                                                                                 8/156 
  Installing : 1:net-snmp-agent-libs-5.7.2-49.el7_9.2.x86_64                                                                                                                           9/156 
  Installing : zlib-devel-1.2.7-21.el7_9.x86_64                                                                                                                                       10/156 
  Installing : 1:perl-Compress-Raw-Zlib-2.061-4.el7.x86_64                                                                                                                            11/156 
  Installing : ksh-20120801-144.el7_9.x86_64                                                                                                                                          12/156 
  Updating   : 12:dhcp-libs-4.2.5-83.el7.centos.1.x86_64                                                                                                                              13/156 
  Installing : perl-XML-NamespaceSupport-1.11-10.el7.noarch                                                                                                                           14/156 
  Installing : perl-Sys-Syslog-0.33-3.el7.x86_64                                                                                                                                      15/156 
  Updating   : 12:dhcp-common-4.2.5-83.el7.centos.1.x86_64                                                                                                                            16/156 
  Installing : elfutils-libelf-devel-0.176-5.el7.x86_64                                                                                                                               17/156 
  Installing : 1:net-snmp-5.7.2-49.el7_9.2.x86_64                                                                                                                                     18/156 
  Installing : perl-Net-SSLeay-1.55-6.el7.x86_64                                                                                                                                      19/156 
  Installing : 2:nmap-6.40-19.el7.x86_64                                                                                                                                              20/156 
  Updating   : libkadm5-1.15.1-55.el7_9.x86_64                                                                                                                                        21/156 
  Installing : perl-Mozilla-CA-20130114-5.el7.noarch                                                                                                                                  22/156 
  Installing : perl-XML-SAX-Base-1.08-7.el7.noarch                                                                                                                                    23/156 
  Installing : 1:perl-TimeDate-2.30-2.el7.noarch                                                                                                                                      24/156 
  Installing : perl-HTTP-Date-6.02-8.el7.noarch                                                                                                                                       25/156 
  Installing : perl-IO-Tty-1.10-11.el7.x86_64                                                                                                                                         26/156 
  Installing : perl-Expect-1.21-14.el7.noarch                                                                                                                                         27/156 
  Installing : mailcap-2.1.41-2.el7.noarch                                                                                                                                            28/156 
  Installing : perl-LWP-MediaTypes-6.02-2.el7.noarch                                                                                                                                  29/156 
  Installing : perl-JSON-2.59-2.el7.noarch                                                                                                                                            30/156 
  Installing : perl-Digest-1.17-245.el7.noarch                                                                                                                                        31/156 
  Installing : perl-Digest-MD5-2.52-3.el7.x86_64                                                                                                                                      32/156 
  Updating   : 32:bind-license-9.11.4-26.P2.el7_9.13.noarch                                                                                                                           33/156 
  Updating   : 32:bind-libs-lite-9.11.4-26.P2.el7_9.13.x86_64                                                                                                                         34/156 
  Updating   : 32:bind-libs-9.11.4-26.P2.el7_9.13.x86_64                                                                                                                              35/156 
  Installing : perl-Encode-Locale-1.03-5.el7.noarch                                                                                                                                   36/156 
  Installing : perl-IO-Socket-IP-0.21-5.el7.noarch                                                                                                                                    37/156 
  Installing : 32:bind-9.11.4-26.P2.el7_9.13.x86_64                                                                                                                                   38/156 
  Updating   : 32:bind-utils-9.11.4-26.P2.el7_9.13.x86_64                                                                                                                             39/156 
  Installing : perl-Crypt-CBC-2.33-2.el7.noarch                                                                                                                                       40/156 
  Installing : 1:perl-Digest-SHA-5.85-4.el7.x86_64                                                                                                                                    41/156 
  Installing : perl-Digest-HMAC-1.03-5.el7.noarch                                                                                                                                     42/156 
  Installing : perl-Net-DNS-0.72-6.el7.x86_64                                                                                                                                         43/156 
  Installing : perl-File-Listing-6.04-7.el7.noarch                                                                                                                                    44/156 
  Installing : 12:dhcp-4.2.5-83.el7.centos.1.x86_64                                                                                                                                   45/156 
  Installing : xz-devel-5.2.2-2.el7_9.x86_64                                                                                                                                          46/156 
  Installing : elfutils-devel-0.176-5.el7.x86_64                                                                                                                                      47/156 
  Updating   : xz-5.2.2-2.el7_9.x86_64                                                                                                                                                48/156 
  Updating   : rpm-build-4.11.3-48.el7_9.x86_64                                                                                                                                       49/156 
  Installing : 4:xCAT-buildkit-2.16.5-snap202303030907.noarch                                                                                                                         50/156 
  Installing : ipmitool-xcat-1.8.18-3.x86_64                                                                                                                                          51/156 
  Installing : perl-Crypt-SSLeay-0.64-5.el7.x86_64                                                                                                                                    52/156 
  Installing : httpd-tools-2.4.6-99.el7.centos.1.x86_64                                                                                                                               53/156 
  Installing : httpd-2.4.6-99.el7.centos.1.x86_64                                                                                                                                     54/156 
  Updating   : 1:openssl-1.0.2k-26.el7_9.x86_64                                                                                                                                       55/156 
  Installing : perl-Net-LibIDN-0.12-15.el7.x86_64                                                                                                                                     56/156 
  Installing : perl-IO-Socket-SSL-1.94-7.el7.noarch                                                                                                                                   57/156 
  Installing : grub2-xcat-2.02-0.76.el7.1.snap201905160255.noarch                                                                                                                     58/156 
  Installing : goconserver-0.3.3-snap202011021058.x86_64                                                                                                                              59/156 
  Installing : perl-Crypt-Rijndael-1.12-1.el7.x86_64                                                                                                                                  60/156 
  Installing : systemtap-sdt-devel-4.0-13.el7.x86_64                                                                                                                                  61/156 
  Installing : perl-Net-Daemon-0.48-5.el7.noarch                                                                                                                                      62/156 
  Installing : xnba-undi-1.21.1-1.noarch                                                                                                                                              63/156 
  Installing : libcom_err-devel-1.42.9-19.el7.x86_64                                                                                                                                  64/156 
  Installing : elilo-xcat-3.14-6.noarch                                                                                                                                               65/156 
  Installing : tftp-5.2-22.el7.x86_64                                                                                                                                                 66/156 
  Installing : syslinux-xcat-3.86-2.noarch                                                                                                                                            67/156 
  Installing : perl-Net-Telnet-3.03-19.el7.noarch                                                                                                                                     68/156 
  Installing : perl-Compress-Raw-Bzip2-2.061-3.el7.x86_64                                                                                                                             69/156 
  Installing : perl-IO-Compress-2.061-2.el7.noarch                                                                                                                                    70/156 
  Installing : perl-Net-HTTP-6.06-2.el7.noarch                                                                                                                                        71/156 
  Installing : perl-Net-HTTPS-NB-0.14-2.noarch                                                                                                                                        72/156 
  Installing : perl-PlRPC-0.2020-14.el7.noarch                                                                                                                                        73/156 
  Installing : perl-DBI-1.627-4.el7.x86_64                                                                                                                                            74/156 
  Installing : perl-DBD-SQLite-1.39-3.el7.x86_64                                                                                                                                      75/156 
  Installing : pcre-devel-8.32-17.el7.x86_64                                                                                                                                          76/156 
  Installing : perl-ExtUtils-Manifest-1.61-244.el7.noarch                                                                                                                             77/156 
  Installing : perl-IO-HTML-1.00-2.el7.noarch                                                                                                                                         78/156 
  Installing : 2:xCAT-genesis-base-ppc64-2.16.3-snap202110141642.noarch                                                                                                               79/156 
  Installing : 1:xCAT-genesis-scripts-ppc64-2.16.5-snap202303030907.noarch                                                                                                            80/156 
If you are installing/updating xCAT-genesis-base separately, not as part of installing/updating all of xCAT, run 'mknb <arch>' manually
  Installing : popt-devel-1.13-16.el7.x86_64                                                                                                                                          81/156 
  Installing : rpm-devel-4.11.3-48.el7_9.x86_64                                                                                                                                       82/156 
  Installing : perl-DB_File-1.830-6.el7.x86_64                                                                                                                                        83/156 
  Installing : perl-Sys-Virt-4.5.0-2.el7.x86_64                                                                                                                                       84/156 
  Installing : 1:perl-FCGI-0.74-8.el7.x86_64                                                                                                                                          85/156 
  Installing : perl-CGI-3.63-4.el7.noarch                                                                                                                                             86/156 
  Installing : gdbm-devel-1.10-8.el7.x86_64                                                                                                                                           87/156 
  Installing : lm_sensors-devel-3.4.0-8.20160601gitf9185e5.el7.x86_64                                                                                                                 88/156 
  Installing : keyutils-libs-devel-1.5.8-3.el7.x86_64                                                                                                                                 89/156 
  Installing : perl-HTML-Tagset-3.20-15.el7.noarch                                                                                                                                    90/156 
  Installing : tcp_wrappers-devel-7.6-77.el7.x86_64                                                                                                                                   91/156 
  Installing : 2:xCAT-genesis-base-x86_64-2.14.5-snap201811190037.noarch                                                                                                              92/156 
  Installing : 1:xCAT-genesis-scripts-x86_64-2.16.5-snap202303030907.noarch                                                                                                           93/156 
If you are installing/updating xCAT-genesis-base separately, not as part of installing/updating all of xCAT, run 'mknb <arch>' manually
  Installing : tftp-server-5.2-22.el7.x86_64                                                                                                                                          94/156 
  Installing : syslinux-4.05-15.el7.x86_64                                                                                                                                            95/156 
  Installing : perl-Digest-SHA1-2.13-9.el7.x86_64                                                                                                                                     96/156 
  Installing : libdb-devel-5.3.21-25.el7.x86_64                                                                                                                                       97/156 
  Installing : perl-ExtUtils-MakeMaker-6.68-3.el7.noarch                                                                                                                              98/156 
  Installing : 1:perl-ExtUtils-ParseXS-3.18-3.el7.noarch                                                                                                                              99/156 
  Installing : 4:perl-devel-5.16.3-299.el7_9.x86_64                                                                                                                                  100/156 
  Installing : perl-ExtUtils-Install-1.58-299.el7_9.noarch                                                                                                                           101/156 
  Installing : perl-Business-ISBN-Data-20120719.001-2.el7.noarch                                                                                                                     102/156 
  Installing : perl-Business-ISBN-2.06-2.el7.noarch                                                                                                                                  103/156 
  Installing : perl-URI-1.60-9.el7.noarch                                                                                                                                            104/156 
  Installing : perl-HTTP-Message-6.06-6.el7.noarch                                                                                                                                   105/156 
  Installing : perl-HTTP-Cookies-6.01-5.el7.noarch                                                                                                                                   106/156 
  Installing : perl-HTML-Parser-3.71-4.el7.x86_64                                                                                                                                    107/156 
  Installing : perl-HTML-Form-6.03-6.el7.noarch                                                                                                                                      108/156 
  Installing : perl-HTTP-Async-0.30-2.noarch                                                                                                                                         109/156 
  Installing : perl-HTTP-Daemon-6.01-8.el7.noarch                                                                                                                                    110/156 
  Installing : perl-HTTP-Negotiate-6.01-5.el7.noarch                                                                                                                                 111/156 
  Installing : perl-WWW-RobotRules-6.02-5.el7.noarch                                                                                                                                 112/156 
  Installing : perl-libwww-perl-6.05-2.el7.noarch                                                                                                                                    113/156 
  Installing : perl-XML-SAX-0.99-9.el7.noarch                                                                                                                                        114/156 
  Installing : perl-XML-Simple-2.20-5.el7.noarch                                                                                                                                     115/156 
  Installing : 1:perl-XML-LibXML-2.0018-5.el7.x86_64                                                                                                                                 116/156 
  Installing : perl-LWP-Protocol-https-6.04-4.el7.noarch                                                                                                                             117/156 
  Installing : libverto-devel-0.2.5-4.el7.x86_64                                                                                                                                     118/156 
  Installing : libsepol-devel-2.5-10.el7.x86_64                                                                                                                                      119/156 
  Installing : libselinux-devel-2.5-15.el7.x86_64                                                                                                                                    120/156 
  Installing : krb5-devel-1.15.1-55.el7_9.x86_64                                                                                                                                     121/156 
  Installing : 1:openssl-devel-1.0.2k-26.el7_9.x86_64                                                                                                                                122/156 
  Installing : 1:net-snmp-devel-5.7.2-49.el7_9.2.x86_64                                                                                                                              123/156 
  Installing : 1:net-snmp-perl-5.7.2-49.el7_9.2.x86_64                                                                                                                               124/156 
  Installing : 4:perl-xCAT-2.16.5-snap202303030907.noarch                                                                                                                            125/156 
  Installing : 4:xCAT-client-2.16.5-snap202303030907.noarch                                                                                                                          126/156 
  Installing : 4:xCAT-server-2.16.5-snap202303030907.noarch                                                                                                                          127/156 
Created symlink from /etc/systemd/system/multi-user.target.wants/xcatd.service to /usr/lib/systemd/system/xcatd.service.
  Installing : 4:xCAT-probe-2.16.5-snap202303030907.noarch                                                                                                                           128/156 
  Installing : perl-IO-Stty-0.03-1.noarch                                                                                                                                            129/156 
  Installing : xCAT-2.16.5-snap202303030907.x86_64                                                                                                                                   130/156 
Generating new node hostkeys...
Generating SSH2 RSA Key...
Generating SSH2 DSA Key...
Generating SSH2 ECDSA Key...
Generating SSH2 ed25519 Key...
Added updates to the /root/.ssh/config file.
Generated /root/.ssh/id_rsa.pub.
Copied /root/.ssh/id_rsa.pub to /install/postscripts/_ssh/authorized_keys.
NFS has been restarted.

Setting up basic certificates.  Respond with a 'y' when prompted.

# NOTE use "-newkey rsa:2048" if running OpenSSL 0.9.8a or higher
Generating RSA private key, 2048 bit long modulus
......................+++
.........+++
e is 65537 (0x10001)
Using configuration from openssl.cnf
Check that the request matches the signature
Signature ok
Certificate Details:
        Serial Number: 1 (0x1)
        Validity
            Not Before: Jan  1 01:01:01 1970 GMT
            Not After : Jun  3 15:40:34 2043 GMT
        Subject:
            commonName                = xCAT CA
        X509v3 extensions:
            X509v3 Subject Key Identifier: 
                CC:69:A3:03:96:1C:39:8B:64:EB:EC:0F:1D:E4:1F:3B:62:70:29:B7
            X509v3 Authority Key Identifier: 
                keyid:CC:69:A3:03:96:1C:39:8B:64:EB:EC:0F:1D:E4:1F:3B:62:70:29:B7

            X509v3 Basic Constraints: critical
                CA:TRUE
            X509v3 Key Usage: 
                Certificate Sign, CRL Sign
            Netscape Cert Type: 
                SSL CA, S/MIME CA
Certificate is to be certified until Jun  3 15:40:34 2043 GMT (7305 days)
Sign the certificate? [y/n]:

1 out of 1 certificate requests certified, commit? [y/n]Write out database with 1 new entries
Data Base Updated
/
Created xCAT certificate.
Generating RSA private key, 2048 bit long modulus
....................+++
..................................................................................................+++
e is 65537 (0x10001)
/
Using configuration from openssl.cnf
Check that the request matches the signature
Signature ok
Certificate Details:
        Serial Number: 2 (0x2)
        Validity
            Not Before: Jan  1 01:01:01 1960 GMT
            Not After : May 29 15:40:34 2043 GMT
        Subject:
            commonName                = master
        X509v3 extensions:
            X509v3 Subject Alternative Name: 
                DNS:master, DNS:master
Certificate is to be certified until May 29 15:40:34 2043 GMT (7300 days)
Sign the certificate? [y/n]:

1 out of 1 certificate requests certified, commit? [y/n]Write out database with 1 new entries
Data Base Updated
/
/opt/xcat/share/xcat/scripts/setup-dockerhost-cert.sh xcatdockerhost
Generating RSA private key, 2048 bit long modulus
....................................+++
...................+++
e is 65537 (0x10001)
/
Using configuration from openssl.cnf
Check that the request matches the signature
Signature ok
Certificate Details:
        Serial Number: 0 (0x0)
        Validity
            Not Before: Jan  1 01:01:01 1960 GMT
            Not After : May 29 15:40:34 2043 GMT
        Subject:
            commonName                = xcatdockerhost
        X509v3 extensions:
            X509v3 Basic Constraints: 
                CA:FALSE
            Netscape Cert Type: 
                SSL Client, SSL Server, Object Signing
            Netscape Comment: 
                OpenSSL Generated Server Certificate
            X509v3 Subject Key Identifier: 
                7A:0A:C9:F2:10:AA:E0:6D:AB:FF:82:E7:42:6C:D0:9C:30:4F:B0:2E
            X509v3 Authority Key Identifier: 
                keyid:CC:69:A3:03:96:1C:39:8B:64:EB:EC:0F:1D:E4:1F:3B:62:70:29:B7

            X509v3 Key Usage: 
                Digital Signature, Key Encipherment, Key Agreement
            X509v3 Extended Key Usage: 
                TLS Web Server Authentication, TLS Web Client Authentication
Certificate is to be certified until May 29 15:40:34 2043 GMT (7300 days)

Write out database with 1 new entries
Data Base Updated
/
Generating RSA private key, 2048 bit long modulus
.................................+++
.................................................................................+++
e is 65537 (0x10001)
Using configuration from openssl.cnf
Check that the request matches the signature
Signature ok
Certificate Details:
        Serial Number: 3 (0x3)
        Validity
            Not Before: Jan  1 01:01:01 1960 GMT
            Not After : May 29 15:40:34 2043 GMT
        Subject:
            commonName                = root
        X509v3 extensions:
            X509v3 Basic Constraints: 
                CA:FALSE
            X509v3 Key Usage: 
                Digital Signature, Key Encipherment, Key Agreement
            X509v3 Extended Key Usage: 
                TLS Web Client Authentication
            Netscape Cert Type: 
                SSL Client, S/MIME, Object Signing
            Netscape Comment: 
                OpenSSL Generated Client Certificate
            X509v3 Subject Key Identifier: 
                E4:DA:5A:54:EF:07:23:B3:E7:1A:BE:51:79:1F:D3:4D:AC:99:46:46
            X509v3 Authority Key Identifier: 
                keyid:CC:69:A3:03:96:1C:39:8B:64:EB:EC:0F:1D:E4:1F:3B:62:70:29:B7

Certificate is to be certified until May 29 15:40:34 2043 GMT (7300 days)
Sign the certificate? [y/n]:

1 out of 1 certificate requests certified, commit? [y/n]Write out database with 1 new entries
Data Base Updated
Created xCAT certificate.
Generating RSA private key, 2048 bit long modulus
.+++
.......................+++
e is 65537 (0x10001)
Using configuration from openssl.cnf
Check that the request matches the signature
Signature ok
Certificate Details:
        Serial Number: 4 (0x4)
        Validity
            Not Before: Jan  1 01:01:01 1960 GMT
            Not After : May 29 15:40:34 2043 GMT
        Subject:
            commonName                = conserver
        X509v3 extensions:
            X509v3 Basic Constraints: 
                CA:FALSE
            X509v3 Key Usage: 
                Digital Signature, Key Encipherment, Key Agreement
            X509v3 Extended Key Usage: 
                TLS Web Client Authentication
            Netscape Cert Type: 
                SSL Client, S/MIME, Object Signing
            Netscape Comment: 
                OpenSSL Generated Client Certificate
            X509v3 Subject Key Identifier: 
                56:33:9F:FD:95:52:E7:F1:65:78:F8:45:86:2D:F9:8B:85:30:D5:70
            X509v3 Authority Key Identifier: 
                keyid:CC:69:A3:03:96:1C:39:8B:64:EB:EC:0F:1D:E4:1F:3B:62:70:29:B7

Certificate is to be certified until May 29 15:40:34 2043 GMT (7300 days)
Sign the certificate? [y/n]:

1 out of 1 certificate requests certified, commit? [y/n]Write out database with 1 new entries
Data Base Updated
Created xCAT certificate.
dns server has been enabled on boot.
httpd has been restarted.
SELINUX is not disabled, disabling it now...
xCAT is now running, it is recommended to tabedit networks 
and set a dynamic ip address range on any networks where nodes 
are to be discovered. Then, run makedhcp -n to create a new dhcpd 
configuration file, and /etc/init.d/dhcpd restart. Either examine sample 
configuration templates, or write your own, or specify a value per 
node with nodeadd or tabedit.
Running '/opt/xcat/sbin/mknb', triggered by the installation/update of xCAT-genesis-scripts ...
Creating genesis.fs.ppc64.gz in /tftpboot/xcat
The 'mknb ppc64' command completed successfully.
Creating genesis.fs.x86_64.gz in /tftpboot/xcat
The 'mknb x86_64' command completed successfully.
  Updating   : krb5-workstation-1.15.1-55.el7_9.x86_64                                                                                                                               131/156 
  Updating   : 12:dhclient-4.2.5-83.el7.centos.1.x86_64                                                                                                                              132/156 
  Updating   : rpm-sign-4.11.3-48.el7_9.x86_64                                                                                                                                       133/156 
  Updating   : rpm-python-4.11.3-48.el7_9.x86_64                                                                                                                                     134/156 
  Cleanup    : 32:bind-utils-9.11.4-26.P2.el7.x86_64                                                                                                                                 135/156 
  Cleanup    : 12:dhclient-4.2.5-82.el7.centos.x86_64                                                                                                                                136/156 
  Cleanup    : 32:bind-libs-9.11.4-26.P2.el7.x86_64                                                                                                                                  137/156 
  Cleanup    : rpm-python-4.11.3-45.el7.x86_64                                                                                                                                       138/156 
  Cleanup    : rpm-build-4.11.3-45.el7.x86_64                                                                                                                                        139/156 
  Cleanup    : 1:openssl-1.0.2k-19.el7.x86_64                                                                                                                                        140/156 
  Cleanup    : rpm-sign-4.11.3-45.el7.x86_64                                                                                                                                         141/156 
  Cleanup    : rpm-build-libs-4.11.3-45.el7.x86_64                                                                                                                                   142/156 
  Cleanup    : 32:bind-libs-lite-9.11.4-26.P2.el7.x86_64                                                                                                                             143/156 
  Cleanup    : rpm-4.11.3-45.el7.x86_64                                                                                                                                              144/156 
  Cleanup    : rpm-libs-4.11.3-45.el7.x86_64                                                                                                                                         145/156 
  Cleanup    : krb5-workstation-1.15.1-50.el7.x86_64                                                                                                                                 146/156 
  Cleanup    : 12:dhcp-common-4.2.5-82.el7.centos.x86_64                                                                                                                             147/156 
  Cleanup    : libkadm5-1.15.1-50.el7.x86_64                                                                                                                                         148/156 
  Cleanup    : xz-5.2.2-1.el7.x86_64                                                                                                                                                 149/156 
  Cleanup    : 1:net-snmp-libs-5.7.2-49.el7.x86_64                                                                                                                                   150/156 
  Cleanup    : 12:dhcp-libs-4.2.5-82.el7.centos.x86_64                                                                                                                               151/156 
  Cleanup    : 32:bind-license-9.11.4-26.P2.el7.noarch                                                                                                                               152/156 
  Cleanup    : 1:openssl-libs-1.0.2k-19.el7.x86_64                                                                                                                                   153/156 
  Cleanup    : krb5-libs-1.15.1-50.el7.x86_64                                                                                                                                        154/156 
  Cleanup    : zlib-1.2.7-18.el7.x86_64                                                                                                                                              155/156 
  Cleanup    : xz-libs-5.2.2-1.el7.x86_64                                                                                                                                            156/156 
  Verifying  : rpm-libs-4.11.3-48.el7_9.x86_64                                                                                                                                         1/156 
  Verifying  : 4:xCAT-server-2.16.5-snap202303030907.noarch                                                                                                                            2/156 
  Verifying  : xz-devel-5.2.2-2.el7_9.x86_64                                                                                                                                           3/156 
  Verifying  : perl-ExtUtils-Install-1.58-299.el7_9.noarch                                                                                                                             4/156 
  Verifying  : httpd-2.4.6-99.el7.centos.1.x86_64                                                                                                                                      5/156 
  Verifying  : 4:xCAT-client-2.16.5-snap202303030907.noarch                                                                                                                            6/156 
  Verifying  : perl-IO-Stty-0.03-1.noarch                                                                                                                                              7/156 
  Verifying  : 1:openssl-devel-1.0.2k-26.el7_9.x86_64                                                                                                                                  8/156 
  Verifying  : libsepol-devel-2.5-10.el7.x86_64                                                                                                                                        9/156 
  Verifying  : perl-LWP-MediaTypes-6.02-2.el7.noarch                                                                                                                                  10/156 
  Verifying  : libverto-devel-0.2.5-4.el7.x86_64                                                                                                                                      11/156 
  Verifying  : perl-File-Listing-6.04-7.el7.noarch                                                                                                                                    12/156 
  Verifying  : ipmitool-xcat-1.8.18-3.x86_64                                                                                                                                          13/156 
  Verifying  : perl-Sys-Syslog-0.33-3.el7.x86_64                                                                                                                                      14/156 
  Verifying  : perl-Business-ISBN-Data-20120719.001-2.el7.noarch                                                                                                                      15/156 
  Verifying  : perl-DBI-1.627-4.el7.x86_64                                                                                                                                            16/156 
  Verifying  : libdb-devel-5.3.21-25.el7.x86_64                                                                                                                                       17/156 
  Verifying  : 12:dhcp-common-4.2.5-83.el7.centos.1.x86_64                                                                                                                            18/156 
  Verifying  : perl-XML-NamespaceSupport-1.11-10.el7.noarch                                                                                                                           19/156 
  Verifying  : perl-IO-Socket-IP-0.21-5.el7.noarch                                                                                                                                    20/156 
  Verifying  : perl-Digest-SHA1-2.13-9.el7.x86_64                                                                                                                                     21/156 
  Verifying  : perl-Net-SSLeay-1.55-6.el7.x86_64                                                                                                                                      22/156 
  Verifying  : syslinux-4.05-15.el7.x86_64                                                                                                                                            23/156 
  Verifying  : tftp-server-5.2-22.el7.x86_64                                                                                                                                          24/156 
  Verifying  : rpm-devel-4.11.3-48.el7_9.x86_64                                                                                                                                       25/156 
  Verifying  : perl-HTTP-Async-0.30-2.noarch                                                                                                                                          26/156 
  Verifying  : perl-Net-HTTP-6.06-2.el7.noarch                                                                                                                                        27/156 
  Verifying  : 1:net-snmp-devel-5.7.2-49.el7_9.2.x86_64                                                                                                                               28/156 
  Verifying  : 1:perl-Digest-SHA-5.85-4.el7.x86_64                                                                                                                                    29/156 
  Verifying  : 2:xCAT-genesis-base-x86_64-2.14.5-snap201811190037.noarch                                                                                                              30/156 
  Verifying  : tcp_wrappers-devel-7.6-77.el7.x86_64                                                                                                                                   31/156 
  Verifying  : 32:bind-libs-lite-9.11.4-26.P2.el7_9.13.x86_64                                                                                                                         32/156 
  Verifying  : perl-HTML-Tagset-3.20-15.el7.noarch                                                                                                                                    33/156 
  Verifying  : rpm-sign-4.11.3-48.el7_9.x86_64                                                                                                                                        34/156 
  Verifying  : keyutils-libs-devel-1.5.8-3.el7.x86_64                                                                                                                                 35/156 
  Verifying  : perl-HTTP-Cookies-6.01-5.el7.noarch                                                                                                                                    36/156 
  Verifying  : lm_sensors-devel-3.4.0-8.20160601gitf9185e5.el7.x86_64                                                                                                                 37/156 
  Verifying  : 32:bind-9.11.4-26.P2.el7_9.13.x86_64                                                                                                                                   38/156 
  Verifying  : 1:xCAT-genesis-scripts-ppc64-2.16.5-snap202303030907.noarch                                                                                                            39/156 
  Verifying  : perl-ExtUtils-MakeMaker-6.68-3.el7.noarch                                                                                                                              40/156 
  Verifying  : gdbm-devel-1.10-8.el7.x86_64                                                                                                                                           41/156 
  Verifying  : 1:openssl-libs-1.0.2k-26.el7_9.x86_64                                                                                                                                  42/156 
  Verifying  : perl-Crypt-SSLeay-0.64-5.el7.x86_64                                                                                                                                    43/156 
  Verifying  : xCAT-2.16.5-snap202303030907.x86_64                                                                                                                                    44/156 
  Verifying  : krb5-workstation-1.15.1-55.el7_9.x86_64                                                                                                                                45/156 
  Verifying  : 1:perl-ExtUtils-ParseXS-3.18-3.el7.noarch                                                                                                                              46/156 
  Verifying  : perl-Encode-Locale-1.03-5.el7.noarch                                                                                                                                   47/156 
  Verifying  : 1:perl-XML-LibXML-2.0018-5.el7.x86_64                                                                                                                                  48/156 
  Verifying  : 12:dhcp-libs-4.2.5-83.el7.centos.1.x86_64                                                                                                                              49/156 
  Verifying  : perl-Digest-HMAC-1.03-5.el7.noarch                                                                                                                                     50/156 
  Verifying  : 32:bind-utils-9.11.4-26.P2.el7_9.13.x86_64                                                                                                                             51/156 
  Verifying  : 1:perl-FCGI-0.74-8.el7.x86_64                                                                                                                                          52/156 
  Verifying  : perl-Sys-Virt-4.5.0-2.el7.x86_64                                                                                                                                       53/156 
  Verifying  : elfutils-libelf-devel-0.176-5.el7.x86_64                                                                                                                               54/156 
  Verifying  : perl-DB_File-1.830-6.el7.x86_64                                                                                                                                        55/156 
  Verifying  : 32:bind-license-9.11.4-26.P2.el7_9.13.noarch                                                                                                                           56/156 
  Verifying  : popt-devel-1.13-16.el7.x86_64                                                                                                                                          57/156 
  Verifying  : 2:xCAT-genesis-base-ppc64-2.16.3-snap202110141642.noarch                                                                                                               58/156 
  Verifying  : perl-LWP-Protocol-https-6.04-4.el7.noarch                                                                                                                              59/156 
  Verifying  : perl-IO-HTML-1.00-2.el7.noarch                                                                                                                                         60/156 
  Verifying  : perl-Digest-1.17-245.el7.noarch                                                                                                                                        61/156 
  Verifying  : 1:xCAT-genesis-scripts-x86_64-2.16.5-snap202303030907.noarch                                                                                                           62/156 
  Verifying  : perl-URI-1.60-9.el7.noarch                                                                                                                                             63/156 
  Verifying  : 2:nmap-6.40-19.el7.x86_64                                                                                                                                              64/156 
  Verifying  : perl-Net-HTTPS-NB-0.14-2.noarch                                                                                                                                        65/156 
  Verifying  : libselinux-devel-2.5-15.el7.x86_64                                                                                                                                     66/156 
  Verifying  : perl-JSON-2.59-2.el7.noarch                                                                                                                                            67/156 
  Verifying  : perl-Business-ISBN-2.06-2.el7.noarch                                                                                                                                   68/156 
  Verifying  : mailcap-2.1.41-2.el7.noarch                                                                                                                                            69/156 
  Verifying  : krb5-devel-1.15.1-55.el7_9.x86_64                                                                                                                                      70/156 
  Verifying  : perl-ExtUtils-Manifest-1.61-244.el7.noarch                                                                                                                             71/156 
  Verifying  : pcre-devel-8.32-17.el7.x86_64                                                                                                                                          72/156 
  Verifying  : ksh-20120801-144.el7_9.x86_64                                                                                                                                          73/156 
  Verifying  : perl-DBD-SQLite-1.39-3.el7.x86_64                                                                                                                                      74/156 
  Verifying  : perl-Compress-Raw-Bzip2-2.061-3.el7.x86_64                                                                                                                             75/156 
  Verifying  : 1:net-snmp-libs-5.7.2-49.el7_9.2.x86_64                                                                                                                                76/156 
  Verifying  : perl-HTML-Parser-3.71-4.el7.x86_64                                                                                                                                     77/156 
  Verifying  : perl-WWW-RobotRules-6.02-5.el7.noarch                                                                                                                                  78/156 
  Verifying  : perl-Digest-MD5-2.52-3.el7.x86_64                                                                                                                                      79/156 
  Verifying  : perl-HTTP-Message-6.06-6.el7.noarch                                                                                                                                    80/156 
  Verifying  : perl-Net-Telnet-3.03-19.el7.noarch                                                                                                                                     81/156 
  Verifying  : syslinux-xcat-3.86-2.noarch                                                                                                                                            82/156 
  Verifying  : 4:xCAT-buildkit-2.16.5-snap202303030907.noarch                                                                                                                         83/156 
  Verifying  : 32:bind-libs-9.11.4-26.P2.el7_9.13.x86_64                                                                                                                              84/156 
  Verifying  : perl-IO-Tty-1.10-11.el7.x86_64                                                                                                                                         85/156 
  Verifying  : 1:net-snmp-agent-libs-5.7.2-49.el7_9.2.x86_64                                                                                                                          86/156 
  Verifying  : 12:dhcp-4.2.5-83.el7.centos.1.x86_64                                                                                                                                   87/156 
  Verifying  : krb5-libs-1.15.1-55.el7_9.x86_64                                                                                                                                       88/156 
  Verifying  : tftp-5.2-22.el7.x86_64                                                                                                                                                 89/156 
  Verifying  : elilo-xcat-3.14-6.noarch                                                                                                                                               90/156 
  Verifying  : perl-HTTP-Daemon-6.01-8.el7.noarch                                                                                                                                     91/156 
  Verifying  : perl-Expect-1.21-14.el7.noarch                                                                                                                                         92/156 
  Verifying  : perl-IO-Compress-2.061-2.el7.noarch                                                                                                                                    93/156 
  Verifying  : perl-PlRPC-0.2020-14.el7.noarch                                                                                                                                        94/156 
  Verifying  : 12:dhclient-4.2.5-83.el7.centos.1.x86_64                                                                                                                               95/156 
  Verifying  : httpd-tools-2.4.6-99.el7.centos.1.x86_64                                                                                                                               96/156 
  Verifying  : perl-HTML-Form-6.03-6.el7.noarch                                                                                                                                       97/156 
  Verifying  : xz-libs-5.2.2-2.el7_9.x86_64                                                                                                                                           98/156 
  Verifying  : 1:perl-TimeDate-2.30-2.el7.noarch                                                                                                                                      99/156 
  Verifying  : 1:openssl-1.0.2k-26.el7_9.x86_64                                                                                                                                      100/156 
  Verifying  : perl-Crypt-CBC-2.33-2.el7.noarch                                                                                                                                      101/156 
  Verifying  : libcom_err-devel-1.42.9-19.el7.x86_64                                                                                                                                 102/156 
  Verifying  : perl-XML-SAX-Base-1.08-7.el7.noarch                                                                                                                                   103/156 
  Verifying  : perl-XML-Simple-2.20-5.el7.noarch                                                                                                                                     104/156 
  Verifying  : 1:net-snmp-perl-5.7.2-49.el7_9.2.x86_64                                                                                                                               105/156 
  Verifying  : 1:net-snmp-5.7.2-49.el7_9.2.x86_64                                                                                                                                    106/156 
  Verifying  : rpm-4.11.3-48.el7_9.x86_64                                                                                                                                            107/156 
  Verifying  : xnba-undi-1.21.1-1.noarch                                                                                                                                             108/156 
  Verifying  : elfutils-devel-0.176-5.el7.x86_64                                                                                                                                     109/156 
  Verifying  : 4:perl-xCAT-2.16.5-snap202303030907.noarch                                                                                                                            110/156 
  Verifying  : perl-Net-Daemon-0.48-5.el7.noarch                                                                                                                                     111/156 
  Verifying  : zlib-1.2.7-21.el7_9.x86_64                                                                                                                                            112/156 
  Verifying  : perl-HTTP-Date-6.02-8.el7.noarch                                                                                                                                      113/156 
  Verifying  : systemtap-sdt-devel-4.0-13.el7.x86_64                                                                                                                                 114/156 
  Verifying  : perl-Crypt-Rijndael-1.12-1.el7.x86_64                                                                                                                                 115/156 
  Verifying  : zlib-devel-1.2.7-21.el7_9.x86_64                                                                                                                                      116/156 
  Verifying  : perl-Mozilla-CA-20130114-5.el7.noarch                                                                                                                                 117/156 
  Verifying  : 4:perl-devel-5.16.3-299.el7_9.x86_64                                                                                                                                  118/156 
  Verifying  : rpm-build-4.11.3-48.el7_9.x86_64                                                                                                                                      119/156 
  Verifying  : perl-Net-DNS-0.72-6.el7.x86_64                                                                                                                                        120/156 
  Verifying  : 4:xCAT-probe-2.16.5-snap202303030907.noarch                                                                                                                           121/156 
  Verifying  : goconserver-0.3.3-snap202011021058.x86_64                                                                                                                             122/156 
  Verifying  : 1:perl-Compress-Raw-Zlib-2.061-4.el7.x86_64                                                                                                                           123/156 
  Verifying  : perl-libwww-perl-6.05-2.el7.noarch                                                                                                                                    124/156 
  Verifying  : grub2-xcat-2.02-0.76.el7.1.snap201905160255.noarch                                                                                                                    125/156 
  Verifying  : perl-XML-SAX-0.99-9.el7.noarch                                                                                                                                        126/156 
  Verifying  : perl-CGI-3.63-4.el7.noarch                                                                                                                                            127/156 
  Verifying  : rpm-python-4.11.3-48.el7_9.x86_64                                                                                                                                     128/156 
  Verifying  : libkadm5-1.15.1-55.el7_9.x86_64                                                                                                                                       129/156 
  Verifying  : perl-HTTP-Negotiate-6.01-5.el7.noarch                                                                                                                                 130/156 
  Verifying  : perl-IO-Socket-SSL-1.94-7.el7.noarch                                                                                                                                  131/156 
  Verifying  : perl-Net-LibIDN-0.12-15.el7.x86_64                                                                                                                                    132/156 
  Verifying  : xz-5.2.2-2.el7_9.x86_64                                                                                                                                               133/156 
  Verifying  : rpm-build-libs-4.11.3-48.el7_9.x86_64                                                                                                                                 134/156 
  Verifying  : 1:net-snmp-libs-5.7.2-49.el7.x86_64                                                                                                                                   135/156 
  Verifying  : 32:bind-libs-lite-9.11.4-26.P2.el7.x86_64                                                                                                                             136/156 
  Verifying  : zlib-1.2.7-18.el7.x86_64                                                                                                                                              137/156 
  Verifying  : rpm-libs-4.11.3-45.el7.x86_64                                                                                                                                         138/156 
  Verifying  : 12:dhcp-libs-4.2.5-82.el7.centos.x86_64                                                                                                                               139/156 
  Verifying  : 1:openssl-libs-1.0.2k-19.el7.x86_64                                                                                                                                   140/156 
  Verifying  : 12:dhclient-4.2.5-82.el7.centos.x86_64                                                                                                                                141/156 
  Verifying  : 32:bind-utils-9.11.4-26.P2.el7.x86_64                                                                                                                                 142/156 
  Verifying  : libkadm5-1.15.1-50.el7.x86_64                                                                                                                                         143/156 
  Verifying  : krb5-workstation-1.15.1-50.el7.x86_64                                                                                                                                 144/156 
  Verifying  : 1:openssl-1.0.2k-19.el7.x86_64                                                                                                                                        145/156 
  Verifying  : rpm-python-4.11.3-45.el7.x86_64                                                                                                                                       146/156 
  Verifying  : krb5-libs-1.15.1-50.el7.x86_64                                                                                                                                        147/156 
  Verifying  : 32:bind-libs-9.11.4-26.P2.el7.x86_64                                                                                                                                  148/156 
  Verifying  : rpm-build-libs-4.11.3-45.el7.x86_64                                                                                                                                   149/156 
  Verifying  : rpm-build-4.11.3-45.el7.x86_64                                                                                                                                        150/156 
  Verifying  : rpm-4.11.3-45.el7.x86_64                                                                                                                                              151/156 
  Verifying  : xz-5.2.2-1.el7.x86_64                                                                                                                                                 152/156 
  Verifying  : xz-libs-5.2.2-1.el7.x86_64                                                                                                                                            153/156 
  Verifying  : rpm-sign-4.11.3-45.el7.x86_64                                                                                                                                         154/156 
  Verifying  : 32:bind-license-9.11.4-26.P2.el7.noarch                                                                                                                               155/156 
  Verifying  : 12:dhcp-common-4.2.5-82.el7.centos.x86_64                                                                                                                             156/156 

Installed:
  xCAT.x86_64 0:2.16.5-snap202303030907                                                                                                                                                      

Dependency Installed:
  bind.x86_64 32:9.11.4-26.P2.el7_9.13                            dhcp.x86_64 12:4.2.5-83.el7.centos.1                         elfutils-devel.x86_64 0:0.176-5.el7                           
  elfutils-libelf-devel.x86_64 0:0.176-5.el7                      elilo-xcat.noarch 0:3.14-6                                   gdbm-devel.x86_64 0:1.10-8.el7                                
  goconserver.x86_64 0:0.3.3-snap202011021058                     grub2-xcat.noarch 0:2.02-0.76.el7.1.snap201905160255         httpd.x86_64 0:2.4.6-99.el7.centos.1                          
  httpd-tools.x86_64 0:2.4.6-99.el7.centos.1                      ipmitool-xcat.x86_64 0:1.8.18-3                              keyutils-libs-devel.x86_64 0:1.5.8-3.el7                      
  krb5-devel.x86_64 0:1.15.1-55.el7_9                             ksh.x86_64 0:20120801-144.el7_9                              libcom_err-devel.x86_64 0:1.42.9-19.el7                       
  libdb-devel.x86_64 0:5.3.21-25.el7                              libselinux-devel.x86_64 0:2.5-15.el7                         libsepol-devel.x86_64 0:2.5-10.el7                            
  libverto-devel.x86_64 0:0.2.5-4.el7                             lm_sensors-devel.x86_64 0:3.4.0-8.20160601gitf9185e5.el7     mailcap.noarch 0:2.1.41-2.el7                                 
  net-snmp.x86_64 1:5.7.2-49.el7_9.2                              net-snmp-agent-libs.x86_64 1:5.7.2-49.el7_9.2                net-snmp-devel.x86_64 1:5.7.2-49.el7_9.2                      
  net-snmp-perl.x86_64 1:5.7.2-49.el7_9.2                         nmap.x86_64 2:6.40-19.el7                                    openssl-devel.x86_64 1:1.0.2k-26.el7_9                        
  pcre-devel.x86_64 0:8.32-17.el7                                 perl-Business-ISBN.noarch 0:2.06-2.el7                       perl-Business-ISBN-Data.noarch 0:20120719.001-2.el7           
  perl-CGI.noarch 0:3.63-4.el7                                    perl-Compress-Raw-Bzip2.x86_64 0:2.061-3.el7                 perl-Compress-Raw-Zlib.x86_64 1:2.061-4.el7                   
  perl-Crypt-CBC.noarch 0:2.33-2.el7                              perl-Crypt-Rijndael.x86_64 0:1.12-1.el7                      perl-Crypt-SSLeay.x86_64 0:0.64-5.el7                         
  perl-DBD-SQLite.x86_64 0:1.39-3.el7                             perl-DBI.x86_64 0:1.627-4.el7                                perl-DB_File.x86_64 0:1.830-6.el7                             
  perl-Digest.noarch 0:1.17-245.el7                               perl-Digest-HMAC.noarch 0:1.03-5.el7                         perl-Digest-MD5.x86_64 0:2.52-3.el7                           
  perl-Digest-SHA.x86_64 1:5.85-4.el7                             perl-Digest-SHA1.x86_64 0:2.13-9.el7                         perl-Encode-Locale.noarch 0:1.03-5.el7                        
  perl-Expect.noarch 0:1.21-14.el7                                perl-ExtUtils-Install.noarch 0:1.58-299.el7_9                perl-ExtUtils-MakeMaker.noarch 0:6.68-3.el7                   
  perl-ExtUtils-Manifest.noarch 0:1.61-244.el7                    perl-ExtUtils-ParseXS.noarch 1:3.18-3.el7                    perl-FCGI.x86_64 1:0.74-8.el7                                 
  perl-File-Listing.noarch 0:6.04-7.el7                           perl-HTML-Form.noarch 0:6.03-6.el7                           perl-HTML-Parser.x86_64 0:3.71-4.el7                          
  perl-HTML-Tagset.noarch 0:3.20-15.el7                           perl-HTTP-Async.noarch 0:0.30-2                              perl-HTTP-Cookies.noarch 0:6.01-5.el7                         
  perl-HTTP-Daemon.noarch 0:6.01-8.el7                            perl-HTTP-Date.noarch 0:6.02-8.el7                           perl-HTTP-Message.noarch 0:6.06-6.el7                         
  perl-HTTP-Negotiate.noarch 0:6.01-5.el7                         perl-IO-Compress.noarch 0:2.061-2.el7                        perl-IO-HTML.noarch 0:1.00-2.el7                              
  perl-IO-Socket-IP.noarch 0:0.21-5.el7                           perl-IO-Socket-SSL.noarch 0:1.94-7.el7                       perl-IO-Stty.noarch 0:0.03-1                                  
  perl-IO-Tty.x86_64 0:1.10-11.el7                                perl-JSON.noarch 0:2.59-2.el7                                perl-LWP-MediaTypes.noarch 0:6.02-2.el7                       
  perl-LWP-Protocol-https.noarch 0:6.04-4.el7                     perl-Mozilla-CA.noarch 0:20130114-5.el7                      perl-Net-DNS.x86_64 0:0.72-6.el7                              
  perl-Net-Daemon.noarch 0:0.48-5.el7                             perl-Net-HTTP.noarch 0:6.06-2.el7                            perl-Net-HTTPS-NB.noarch 0:0.14-2                             
  perl-Net-LibIDN.x86_64 0:0.12-15.el7                            perl-Net-SSLeay.x86_64 0:1.55-6.el7                          perl-Net-Telnet.noarch 0:3.03-19.el7                          
  perl-PlRPC.noarch 0:0.2020-14.el7                               perl-Sys-Syslog.x86_64 0:0.33-3.el7                          perl-Sys-Virt.x86_64 0:4.5.0-2.el7                            
  perl-TimeDate.noarch 1:2.30-2.el7                               perl-URI.noarch 0:1.60-9.el7                                 perl-WWW-RobotRules.noarch 0:6.02-5.el7                       
  perl-XML-LibXML.x86_64 1:2.0018-5.el7                           perl-XML-NamespaceSupport.noarch 0:1.11-10.el7               perl-XML-SAX.noarch 0:0.99-9.el7                              
  perl-XML-SAX-Base.noarch 0:1.08-7.el7                           perl-XML-Simple.noarch 0:2.20-5.el7                          perl-devel.x86_64 4:5.16.3-299.el7_9                          
  perl-libwww-perl.noarch 0:6.05-2.el7                            perl-xCAT.noarch 4:2.16.5-snap202303030907                   popt-devel.x86_64 0:1.13-16.el7                               
  rpm-devel.x86_64 0:4.11.3-48.el7_9                              syslinux.x86_64 0:4.05-15.el7                                syslinux-xcat.noarch 0:3.86-2                                 
  systemtap-sdt-devel.x86_64 0:4.0-13.el7                         tcp_wrappers-devel.x86_64 0:7.6-77.el7                       tftp.x86_64 0:5.2-22.el7                                      
  tftp-server.x86_64 0:5.2-22.el7                                 xCAT-buildkit.noarch 4:2.16.5-snap202303030907               xCAT-client.noarch 4:2.16.5-snap202303030907                  
  xCAT-genesis-base-ppc64.noarch 2:2.16.3-snap202110141642        xCAT-genesis-base-x86_64.noarch 2:2.14.5-snap201811190037    xCAT-genesis-scripts-ppc64.noarch 1:2.16.5-snap202303030907   
  xCAT-genesis-scripts-x86_64.noarch 1:2.16.5-snap202303030907    xCAT-probe.noarch 4:2.16.5-snap202303030907                  xCAT-server.noarch 4:2.16.5-snap202303030907                  
  xnba-undi.noarch 0:1.21.1-1                                     xz-devel.x86_64 0:5.2.2-2.el7_9                              zlib-devel.x86_64 0:1.2.7-21.el7_9                            

Dependency Updated:
  bind-libs.x86_64 32:9.11.4-26.P2.el7_9.13   bind-libs-lite.x86_64 32:9.11.4-26.P2.el7_9.13   bind-license.noarch 32:9.11.4-26.P2.el7_9.13   bind-utils.x86_64 32:9.11.4-26.P2.el7_9.13  
  dhclient.x86_64 12:4.2.5-83.el7.centos.1    dhcp-common.x86_64 12:4.2.5-83.el7.centos.1      dhcp-libs.x86_64 12:4.2.5-83.el7.centos.1      krb5-libs.x86_64 0:1.15.1-55.el7_9          
  krb5-workstation.x86_64 0:1.15.1-55.el7_9   libkadm5.x86_64 0:1.15.1-55.el7_9                net-snmp-libs.x86_64 1:5.7.2-49.el7_9.2        openssl.x86_64 1:1.0.2k-26.el7_9            
  openssl-libs.x86_64 1:1.0.2k-26.el7_9       rpm.x86_64 0:4.11.3-48.el7_9                     rpm-build.x86_64 0:4.11.3-48.el7_9             rpm-build-libs.x86_64 0:4.11.3-48.el7_9     
  rpm-libs.x86_64 0:4.11.3-48.el7_9           rpm-python.x86_64 0:4.11.3-48.el7_9              rpm-sign.x86_64 0:4.11.3-48.el7_9              xz.x86_64 0:5.2.2-2.el7_9                   
  xz-libs.x86_64 0:5.2.2-2.el7_9              zlib.x86_64 0:1.2.7-21.el7_9                    

Complete!
[root@master ~]# cat /etc/pro
profile    profile.d/ protocols  
[root@master ~]# cat /etc/pro
profile    profile.d/ protocols  
[root@master ~]# cat /etc/profile.d/xcat.sh
XCATROOT=/opt/xcat
PATH=$XCATROOT/bin:$XCATROOT/sbin:$XCATROOT/share/xcat/tools:$PATH
MANPATH=$XCATROOT/share/man:$MANPATH
export XCATROOT PATH MANPATH
export PERL_BADLANG=0
# If /usr/local/share/perl5 is not already in @INC, add it to PERL5LIB
perl -e "print \"@INC\"" | egrep "(^|\W)/usr/local/share/perl5($| )" > /dev/null
if [ $? = 1 ]; then
    export PERL5LIB=/usr/local/share/perl5:$PERL5LIB
fi
[root@master ~]# source /etc/profile.d/xcat.sh
[root@master ~]# lsdef -t osimage 
Could not find any object definitions to display.
[root@master ~]# lsblk
NAME            MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
sda               8:0    0  100G  0 disk 
├─sda1            8:1    0    1G  0 part /boot
└─sda2            8:2    0   99G  0 part 
  ├─centos-root 253:0    0   50G  0 lvm  /
  ├─centos-swap 253:1    0  4.5G  0 lvm  [SWAP]
  └─centos-home 253:2    0 44.5G  0 lvm  /home
sr0              11:0    1 1024M  0 rom  
[root@master ~]# dd if=/dev/sr0 of=centos.iso
dd: failed to open ‘/dev/sr0’: No medium found
[root@master ~]# ll /dev/sr0 
brw-rw----+ 1 root cdrom 11, 0 Jun  3 11:18 /dev/sr0
[root@master ~]# lsdef -t osimage
Could not find any object definitions to display.
[root@master ~]# lsblk
NAME            MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
sda               8:0    0  100G  0 disk 
├─sda1            8:1    0    1G  0 part /boot
└─sda2            8:2    0   99G  0 part 
  ├─centos-root 253:0    0   50G  0 lvm  /
  ├─centos-swap 253:1    0  4.5G  0 lvm  [SWAP]
  └─centos-home 253:2    0 44.5G  0 lvm  /home
sr0              11:0    1 1024M  0 rom  
[root@master ~]# copycds centos.iso
Error: [master]: The management server was unable to find/read /root/centos.iso. Ensure that file exists on the server at the specified location.
[root@master ~]# lsdef -t osimage
Could not find any object definitions to display.
[root@master ~]# lsblk
NAME            MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
sda               8:0    0  100G  0 disk 
├─sda1            8:1    0    1G  0 part /boot
└─sda2            8:2    0   99G  0 part 
  ├─centos-root 253:0    0   50G  0 lvm  /
  ├─centos-swap 253:1    0  4.5G  0 lvm  [SWAP]
  └─centos-home 253:2    0 44.5G  0 lvm  /home
sr0              11:0    1 1024M  0 rom  
[root@master ~]# lsblk
NAME            MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
sda               8:0    0  100G  0 disk 
├─sda1            8:1    0    1G  0 part /boot
└─sda2            8:2    0   99G  0 part 
  ├─centos-root 253:0    0   50G  0 lvm  /
  ├─centos-swap 253:1    0  4.5G  0 lvm  [SWAP]
  └─centos-home 253:2    0 44.5G  0 lvm  /home
sr0              11:0    1  4.4G  0 rom  /run/media/master/CentOS 7 x86_64
[root@master ~]# lsdef -t osimage 
Could not find any object definitions to display.
[root@master ~]# dd if=/dev/sr0 of=centos.iso
9203712+0 records in
9203712+0 records out
4712300544 bytes (4.7 GB) copied, 78.4984 s, 60.0 MB/s
[root@master ~]# copycds centos.iso
Copying media to /install/centos7.9/x86_64
Media copy operation successful
[root@master ~]# lsdef -t osimage
centos7.9-x86_64-install-compute  (osimage)
centos7.9-x86_64-netboot-compute  (osimage)
centos7.9-x86_64-statelite-compute  (osimage)
[root@master ~]# lsdef -t osimage centos7.9-x86_64-netboot-compute
Object name: centos7.9-x86_64-netboot-compute
    exlist=/opt/xcat/share/xcat/netboot/centos/compute.centos7.exlist
    imagetype=linux
    osarch=x86_64
    osdistroname=centos7.9-x86_64
    osname=Linux
    osvers=centos7.9
    otherpkgdir=/install/post/otherpkgs/centos7.9/x86_64
    pkgdir=/install/centos7.9/x86_64
    pkglist=/opt/xcat/share/xcat/netboot/centos/compute.centos7.pkglist
    postinstall=/opt/xcat/share/xcat/netboot/centos/compute.centos7.postinstall
    profile=compute
    provmethod=netboot
    rootimgdir=/install/netboot/centos7.9/x86_64/compute
[root@master ~]# genimage centos7.9-x86_64-netboot-compute
Generating image: 
cd /opt/xcat/share/xcat/netboot/centos; ./genimage -a x86_64 -o centos7.9 -p compute --srcdir "/install/centos7.9/x86_64" --pkglist /opt/xcat/share/xcat/netboot/centos/compute.centos7.pkglist --otherpkgdir "/install/post/otherpkgs/centos7.9/x86_64" --postinstall "/opt/xcat/share/xcat/netboot/centos/compute.centos7.postinstall" --rootimgdir /install/netboot/centos7.9/x86_64/compute --tempfile /tmp/xcat_genimage.14398 centos7.9-x86_64-netboot-compute
112 blocks
/opt/xcat/share/xcat/netboot/centos
112 blocks
/opt/xcat/share/xcat/netboot/centos
 yum -y -c /tmp/genimage.14413.yum.conf --installroot=/install/netboot/centos7.9/x86_64/compute/rootimg/ --disablerepo=* --enablerepo=centos7.9-x86_64-0  install  bash dracut-network nfs-utils openssl dhclient kernel openssh-server openssh-clients iputils bc irqbalance procps-ng wget vim-minimal ntp rpm rsync rsyslog e2fsprogs parted net-tools gzip tar xz ethtool
Resolving Dependencies
--> Running transaction check
---> Package bash.x86_64 0:4.2.46-34.el7 will be installed
--> Processing Dependency: rtld(GNU_HASH) for package: bash-4.2.46-34.el7.x86_64
--> Processing Dependency: libdl.so.2(GLIBC_2.2.5)(64bit) for package: bash-4.2.46-34.el7.x86_64
--> Processing Dependency: libc.so.6(GLIBC_2.15)(64bit) for package: bash-4.2.46-34.el7.x86_64
--> Processing Dependency: libtinfo.so.5()(64bit) for package: bash-4.2.46-34.el7.x86_64
--> Processing Dependency: libdl.so.2()(64bit) for package: bash-4.2.46-34.el7.x86_64
---> Package bc.x86_64 0:1.06.95-13.el7 will be installed
--> Processing Dependency: /sbin/install-info for package: bc-1.06.95-13.el7.x86_64
--> Processing Dependency: /sbin/install-info for package: bc-1.06.95-13.el7.x86_64
--> Processing Dependency: libreadline.so.6()(64bit) for package: bc-1.06.95-13.el7.x86_64
---> Package dhclient.x86_64 12:4.2.5-82.el7.centos will be installed
--> Processing Dependency: dhcp-libs(x86-64) = 12:4.2.5-82.el7.centos for package: 12:dhclient-4.2.5-82.el7.centos.x86_64
--> Processing Dependency: dhcp-common = 12:4.2.5-82.el7.centos for package: 12:dhclient-4.2.5-82.el7.centos.x86_64
--> Processing Dependency: sed for package: 12:dhclient-4.2.5-82.el7.centos.x86_64
--> Processing Dependency: iproute for package: 12:dhclient-4.2.5-82.el7.centos.x86_64
--> Processing Dependency: initscripts for package: 12:dhclient-4.2.5-82.el7.centos.x86_64
--> Processing Dependency: hostname for package: 12:dhclient-4.2.5-82.el7.centos.x86_64
--> Processing Dependency: grep for package: 12:dhclient-4.2.5-82.el7.centos.x86_64
--> Processing Dependency: gawk for package: 12:dhclient-4.2.5-82.el7.centos.x86_64
--> Processing Dependency: coreutils for package: 12:dhclient-4.2.5-82.el7.centos.x86_64
--> Processing Dependency: libsystemd-daemon.so.0()(64bit) for package: 12:dhclient-4.2.5-82.el7.centos.x86_64
--> Processing Dependency: libomapi.so.0()(64bit) for package: 12:dhclient-4.2.5-82.el7.centos.x86_64
--> Processing Dependency: libldap-2.4.so.2()(64bit) for package: 12:dhclient-4.2.5-82.el7.centos.x86_64
--> Processing Dependency: liblber-2.4.so.2()(64bit) for package: 12:dhclient-4.2.5-82.el7.centos.x86_64
--> Processing Dependency: libkrb5.so.3()(64bit) for package: 12:dhclient-4.2.5-82.el7.centos.x86_64
--> Processing Dependency: libk5crypto.so.3()(64bit) for package: 12:dhclient-4.2.5-82.el7.centos.x86_64
--> Processing Dependency: libisc-export.so.169()(64bit) for package: 12:dhclient-4.2.5-82.el7.centos.x86_64
--> Processing Dependency: libgssapi_krb5.so.2()(64bit) for package: 12:dhclient-4.2.5-82.el7.centos.x86_64
--> Processing Dependency: libdns-export.so.1102()(64bit) for package: 12:dhclient-4.2.5-82.el7.centos.x86_64
--> Processing Dependency: libcrypto.so.10()(64bit) for package: 12:dhclient-4.2.5-82.el7.centos.x86_64
--> Processing Dependency: libcom_err.so.2()(64bit) for package: 12:dhclient-4.2.5-82.el7.centos.x86_64
--> Processing Dependency: libcap.so.2()(64bit) for package: 12:dhclient-4.2.5-82.el7.centos.x86_64
--> Processing Dependency: libcap-ng.so.0()(64bit) for package: 12:dhclient-4.2.5-82.el7.centos.x86_64
---> Package dracut-network.x86_64 0:033-572.el7 will be installed
--> Processing Dependency: dracut = 033-572.el7 for package: dracut-network-033-572.el7.x86_64
---> Package e2fsprogs.x86_64 0:1.42.9-19.el7 will be installed
--> Processing Dependency: libss = 1.42.9-19.el7 for package: e2fsprogs-1.42.9-19.el7.x86_64
--> Processing Dependency: e2fsprogs-libs(x86-64) = 1.42.9-19.el7 for package: e2fsprogs-1.42.9-19.el7.x86_64
--> Processing Dependency: libuuid.so.1(UUID_1.0)(64bit) for package: e2fsprogs-1.42.9-19.el7.x86_64
--> Processing Dependency: libblkid.so.1(BLKID_2.17)(64bit) for package: e2fsprogs-1.42.9-19.el7.x86_64
--> Processing Dependency: libblkid.so.1(BLKID_2.15)(64bit) for package: e2fsprogs-1.42.9-19.el7.x86_64
--> Processing Dependency: libblkid.so.1(BLKID_1.0)(64bit) for package: e2fsprogs-1.42.9-19.el7.x86_64
--> Processing Dependency: libuuid.so.1()(64bit) for package: e2fsprogs-1.42.9-19.el7.x86_64
--> Processing Dependency: libss.so.2()(64bit) for package: e2fsprogs-1.42.9-19.el7.x86_64
--> Processing Dependency: libext2fs.so.2()(64bit) for package: e2fsprogs-1.42.9-19.el7.x86_64
--> Processing Dependency: libe2p.so.2()(64bit) for package: e2fsprogs-1.42.9-19.el7.x86_64
--> Processing Dependency: libblkid.so.1()(64bit) for package: e2fsprogs-1.42.9-19.el7.x86_64
---> Package ethtool.x86_64 2:4.8-10.el7 will be installed
---> Package gzip.x86_64 0:1.5-10.el7 will be installed
---> Package iputils.x86_64 0:20160308-10.el7 will be installed
--> Processing Dependency: filesystem >= 3 for package: iputils-20160308-10.el7.x86_64
--> Processing Dependency: systemd for package: iputils-20160308-10.el7.x86_64
--> Processing Dependency: systemd for package: iputils-20160308-10.el7.x86_64
--> Processing Dependency: libidn.so.11(LIBIDN_1.0)(64bit) for package: iputils-20160308-10.el7.x86_64
--> Processing Dependency: /sbin/chkconfig for package: iputils-20160308-10.el7.x86_64
--> Processing Dependency: /sbin/chkconfig for package: iputils-20160308-10.el7.x86_64
--> Processing Dependency: libidn.so.11()(64bit) for package: iputils-20160308-10.el7.x86_64
---> Package irqbalance.x86_64 3:1.0.7-12.el7 will be installed
--> Processing Dependency: numactl-libs for package: 3:irqbalance-1.0.7-12.el7.x86_64
--> Processing Dependency: libnuma.so.1(libnuma_1.1)(64bit) for package: 3:irqbalance-1.0.7-12.el7.x86_64
--> Processing Dependency: libnuma.so.1()(64bit) for package: 3:irqbalance-1.0.7-12.el7.x86_64
--> Processing Dependency: libglib-2.0.so.0()(64bit) for package: 3:irqbalance-1.0.7-12.el7.x86_64
---> Package kernel.x86_64 0:3.10.0-1160.el7 will be installed
--> Processing Dependency: module-init-tools >= 3.16-2 for package: kernel-3.10.0-1160.el7.x86_64
--> Processing Dependency: linux-firmware >= 20190429-72 for package: kernel-3.10.0-1160.el7.x86_64
--> Processing Dependency: grubby >= 8.28-2 for package: kernel-3.10.0-1160.el7.x86_64
--> Processing Dependency: system-release for package: kernel-3.10.0-1160.el7.x86_64
--> Processing Dependency: /usr/sbin/new-kernel-pkg for package: kernel-3.10.0-1160.el7.x86_64
--> Processing Dependency: /usr/sbin/new-kernel-pkg for package: kernel-3.10.0-1160.el7.x86_64
---> Package net-tools.x86_64 0:2.0-0.25.20131004git.el7 will be installed
--> Processing Dependency: libselinux.so.1()(64bit) for package: net-tools-2.0-0.25.20131004git.el7.x86_64
---> Package nfs-utils.x86_64 1:1.3.0-0.68.el7 will be installed
--> Processing Dependency: shadow-utils >= 4.0.3-25 for package: 1:nfs-utils-1.3.0-0.68.el7.x86_64
--> Processing Dependency: libtirpc >= 0.2.4-0.7 for package: 1:nfs-utils-1.3.0-0.68.el7.x86_64
--> Processing Dependency: gssproxy >= 0.7.0-3 for package: 1:nfs-utils-1.3.0-0.68.el7.x86_64
--> Processing Dependency: rpcbind for package: 1:nfs-utils-1.3.0-0.68.el7.x86_64
--> Processing Dependency: quota for package: 1:nfs-utils-1.3.0-0.68.el7.x86_64
--> Processing Dependency: libnfsidmap for package: 1:nfs-utils-1.3.0-0.68.el7.x86_64
--> Processing Dependency: libmount.so.1(MOUNT_2.19)(64bit) for package: 1:nfs-utils-1.3.0-0.68.el7.x86_64
--> Processing Dependency: libmount for package: 1:nfs-utils-1.3.0-0.68.el7.x86_64
--> Processing Dependency: libkeyutils.so.1(KEYUTILS_1.5)(64bit) for package: 1:nfs-utils-1.3.0-0.68.el7.x86_64
--> Processing Dependency: libkeyutils.so.1(KEYUTILS_1.4)(64bit) for package: 1:nfs-utils-1.3.0-0.68.el7.x86_64
--> Processing Dependency: libkeyutils.so.1(KEYUTILS_1.0)(64bit) for package: 1:nfs-utils-1.3.0-0.68.el7.x86_64
--> Processing Dependency: libkeyutils.so.1(KEYUTILS_0.3)(64bit) for package: 1:nfs-utils-1.3.0-0.68.el7.x86_64
--> Processing Dependency: libevent for package: 1:nfs-utils-1.3.0-0.68.el7.x86_64
--> Processing Dependency: libdevmapper.so.1.02(DM_1_02_97)(64bit) for package: 1:nfs-utils-1.3.0-0.68.el7.x86_64
--> Processing Dependency: libdevmapper.so.1.02(Base)(64bit) for package: 1:nfs-utils-1.3.0-0.68.el7.x86_64
--> Processing Dependency: keyutils for package: 1:nfs-utils-1.3.0-0.68.el7.x86_64
--> Processing Dependency: /usr/bin/python for package: 1:nfs-utils-1.3.0-0.68.el7.x86_64
--> Processing Dependency: /sbin/nologin for package: 1:nfs-utils-1.3.0-0.68.el7.x86_64
--> Processing Dependency: libwrap.so.0()(64bit) for package: 1:nfs-utils-1.3.0-0.68.el7.x86_64
--> Processing Dependency: libtirpc.so.1()(64bit) for package: 1:nfs-utils-1.3.0-0.68.el7.x86_64
--> Processing Dependency: libsqlite3.so.0()(64bit) for package: 1:nfs-utils-1.3.0-0.68.el7.x86_64
--> Processing Dependency: libnfsidmap.so.0()(64bit) for package: 1:nfs-utils-1.3.0-0.68.el7.x86_64
--> Processing Dependency: libmount.so.1()(64bit) for package: 1:nfs-utils-1.3.0-0.68.el7.x86_64
--> Processing Dependency: libkeyutils.so.1()(64bit) for package: 1:nfs-utils-1.3.0-0.68.el7.x86_64
--> Processing Dependency: libevent-2.0.so.5()(64bit) for package: 1:nfs-utils-1.3.0-0.68.el7.x86_64
--> Processing Dependency: libdevmapper.so.1.02()(64bit) for package: 1:nfs-utils-1.3.0-0.68.el7.x86_64
---> Package ntp.x86_64 0:4.2.6p5-29.el7.centos.2 will be installed
--> Processing Dependency: ntpdate = 4.2.6p5-29.el7.centos.2 for package: ntp-4.2.6p5-29.el7.centos.2.x86_64
--> Processing Dependency: libopts.so.25()(64bit) for package: ntp-4.2.6p5-29.el7.centos.2.x86_64
--> Processing Dependency: libedit.so.0()(64bit) for package: ntp-4.2.6p5-29.el7.centos.2.x86_64
---> Package openssh-clients.x86_64 0:7.4p1-21.el7 will be installed
--> Processing Dependency: openssh = 7.4p1-21.el7 for package: openssh-clients-7.4p1-21.el7.x86_64
--> Processing Dependency: fipscheck-lib(x86-64) >= 1.3.0 for package: openssh-clients-7.4p1-21.el7.x86_64
--> Processing Dependency: libz.so.1()(64bit) for package: openssh-clients-7.4p1-21.el7.x86_64
--> Processing Dependency: libfipscheck.so.1()(64bit) for package: openssh-clients-7.4p1-21.el7.x86_64
---> Package openssh-server.x86_64 0:7.4p1-21.el7 will be installed
--> Processing Dependency: pam >= 1.0.1-3 for package: openssh-server-7.4p1-21.el7.x86_64
--> Processing Dependency: libpam.so.0(LIBPAM_1.0)(64bit) for package: openssh-server-7.4p1-21.el7.x86_64
--> Processing Dependency: libpam.so.0()(64bit) for package: openssh-server-7.4p1-21.el7.x86_64
--> Processing Dependency: libaudit.so.1()(64bit) for package: openssh-server-7.4p1-21.el7.x86_64
---> Package openssl.x86_64 1:1.0.2k-19.el7 will be installed
--> Processing Dependency: make for package: 1:openssl-1.0.2k-19.el7.x86_64
---> Package parted.x86_64 0:3.1-32.el7 will be installed
--> Processing Dependency: libsepol.so.1()(64bit) for package: parted-3.1-32.el7.x86_64
---> Package procps-ng.x86_64 0:3.3.10-28.el7 will be installed
---> Package rpm.x86_64 0:4.11.3-45.el7 will be installed
--> Processing Dependency: popt(x86-64) >= 1.10.2.1 for package: rpm-4.11.3-45.el7.x86_64
--> Processing Dependency: libpopt.so.0(LIBPOPT_0)(64bit) for package: rpm-4.11.3-45.el7.x86_64
--> Processing Dependency: curl for package: rpm-4.11.3-45.el7.x86_64
--> Processing Dependency: /usr/bin/db_stat for package: rpm-4.11.3-45.el7.x86_64
--> Processing Dependency: librpmio.so.3()(64bit) for package: rpm-4.11.3-45.el7.x86_64
--> Processing Dependency: librpm.so.3()(64bit) for package: rpm-4.11.3-45.el7.x86_64
--> Processing Dependency: libpopt.so.0()(64bit) for package: rpm-4.11.3-45.el7.x86_64
--> Processing Dependency: libnss3.so()(64bit) for package: rpm-4.11.3-45.el7.x86_64
--> Processing Dependency: liblzma.so.5()(64bit) for package: rpm-4.11.3-45.el7.x86_64
--> Processing Dependency: liblua-5.1.so()(64bit) for package: rpm-4.11.3-45.el7.x86_64
--> Processing Dependency: libelf.so.1()(64bit) for package: rpm-4.11.3-45.el7.x86_64
--> Processing Dependency: libdb-5.3.so()(64bit) for package: rpm-4.11.3-45.el7.x86_64
--> Processing Dependency: libbz2.so.1()(64bit) for package: rpm-4.11.3-45.el7.x86_64
--> Processing Dependency: libacl.so.1()(64bit) for package: rpm-4.11.3-45.el7.x86_64
---> Package rsync.x86_64 0:3.1.2-10.el7 will be installed
--> Processing Dependency: libattr.so.1(ATTR_1.0)(64bit) for package: rsync-3.1.2-10.el7.x86_64
--> Processing Dependency: libattr.so.1()(64bit) for package: rsync-3.1.2-10.el7.x86_64
---> Package rsyslog.x86_64 0:8.24.0-55.el7 will be installed
--> Processing Dependency: logrotate >= 3.5.2 for package: rsyslog-8.24.0-55.el7.x86_64
--> Processing Dependency: libestr >= 0.1.9 for package: rsyslog-8.24.0-55.el7.x86_64
--> Processing Dependency: libgcc_s.so.1(GCC_3.3.1)(64bit) for package: rsyslog-8.24.0-55.el7.x86_64
--> Processing Dependency: libgcc_s.so.1(GCC_3.0)(64bit) for package: rsyslog-8.24.0-55.el7.x86_64
--> Processing Dependency: libgcc_s.so.1()(64bit) for package: rsyslog-8.24.0-55.el7.x86_64
--> Processing Dependency: libfastjson.so.4()(64bit) for package: rsyslog-8.24.0-55.el7.x86_64
--> Processing Dependency: libestr.so.0()(64bit) for package: rsyslog-8.24.0-55.el7.x86_64
---> Package tar.x86_64 2:1.26-35.el7 will be installed
---> Package vim-minimal.x86_64 2:7.4.629-7.el7 will be installed
---> Package wget.x86_64 0:1.14-18.el7_6.1 will be installed
--> Processing Dependency: libpcre.so.1()(64bit) for package: wget-1.14-18.el7_6.1.x86_64
---> Package xz.x86_64 0:5.2.2-1.el7 will be installed
--> Running transaction check
---> Package audit-libs.x86_64 0:2.8.5-4.el7 will be installed
---> Package autogen-libopts.x86_64 0:5.18-5.el7 will be installed
---> Package bind-export-libs.x86_64 32:9.11.4-26.P2.el7 will be installed
---> Package bzip2-libs.x86_64 0:1.0.6-13.el7 will be installed
---> Package centos-release.x86_64 0:7-9.2009.0.el7.centos will be installed
---> Package chkconfig.x86_64 0:1.7.6-1.el7 will be installed
---> Package coreutils.x86_64 0:8.22-24.el7 will be installed
--> Processing Dependency: ncurses for package: coreutils-8.22-24.el7.x86_64
--> Processing Dependency: gmp for package: coreutils-8.22-24.el7.x86_64
--> Processing Dependency: libgmp.so.10()(64bit) for package: coreutils-8.22-24.el7.x86_64
---> Package curl.x86_64 0:7.29.0-59.el7 will be installed
--> Processing Dependency: libcurl = 7.29.0-59.el7 for package: curl-7.29.0-59.el7.x86_64
--> Processing Dependency: libplds4.so()(64bit) for package: curl-7.29.0-59.el7.x86_64
--> Processing Dependency: libplc4.so()(64bit) for package: curl-7.29.0-59.el7.x86_64
--> Processing Dependency: libnssutil3.so()(64bit) for package: curl-7.29.0-59.el7.x86_64
--> Processing Dependency: libnspr4.so()(64bit) for package: curl-7.29.0-59.el7.x86_64
--> Processing Dependency: libcurl.so.4()(64bit) for package: curl-7.29.0-59.el7.x86_64
---> Package device-mapper-libs.x86_64 7:1.02.170-6.el7 will be installed
--> Processing Dependency: device-mapper = 7:1.02.170-6.el7 for package: 7:device-mapper-libs-1.02.170-6.el7.x86_64
---> Package dhcp-common.x86_64 12:4.2.5-82.el7.centos will be installed
---> Package dhcp-libs.x86_64 12:4.2.5-82.el7.centos will be installed
---> Package dracut.x86_64 0:033-572.el7 will be installed
--> Processing Dependency: kpartx for package: dracut-033-572.el7.x86_64
--> Processing Dependency: hardlink for package: dracut-033-572.el7.x86_64
--> Processing Dependency: findutils for package: dracut-033-572.el7.x86_64
--> Processing Dependency: cpio for package: dracut-033-572.el7.x86_64
--> Processing Dependency: /usr/bin/pkg-config for package: dracut-033-572.el7.x86_64
---> Package e2fsprogs-libs.x86_64 0:1.42.9-19.el7 will be installed
---> Package elfutils-libelf.x86_64 0:0.176-5.el7 will be installed
---> Package filesystem.x86_64 0:3.2-25.el7 will be installed
--> Processing Dependency: setup for package: filesystem-3.2-25.el7.x86_64
---> Package fipscheck-lib.x86_64 0:1.4.1-6.el7 will be installed
--> Processing Dependency: /usr/bin/fipscheck for package: fipscheck-lib-1.4.1-6.el7.x86_64
---> Package gawk.x86_64 0:4.0.2-4.el7_3.1 will be installed
---> Package glib2.x86_64 0:2.56.1-7.el7 will be installed
--> Processing Dependency: shared-mime-info for package: glib2-2.56.1-7.el7.x86_64
--> Processing Dependency: libffi.so.6()(64bit) for package: glib2-2.56.1-7.el7.x86_64
---> Package glibc.x86_64 0:2.17-317.el7 will be installed
--> Processing Dependency: glibc-common = 2.17-317.el7 for package: glibc-2.17-317.el7.x86_64
--> Processing Dependency: libfreebl3.so(NSSRAWHASH_3.12.3)(64bit) for package: glibc-2.17-317.el7.x86_64
--> Processing Dependency: basesystem for package: glibc-2.17-317.el7.x86_64
--> Processing Dependency: libfreebl3.so()(64bit) for package: glibc-2.17-317.el7.x86_64
---> Package grep.x86_64 0:2.20-3.el7 will be installed
---> Package grubby.x86_64 0:8.28-26.el7 will be installed
---> Package gssproxy.x86_64 0:0.7.0-29.el7 will be installed
--> Processing Dependency: libini_config >= 1.3.1-31 for package: gssproxy-0.7.0-29.el7.x86_64
--> Processing Dependency: libverto-module-base for package: gssproxy-0.7.0-29.el7.x86_64
--> Processing Dependency: libref_array.so.1(REF_ARRAY_0.1.1)(64bit) for package: gssproxy-0.7.0-29.el7.x86_64
--> Processing Dependency: libini_config.so.3(INI_CONFIG_1.2.0)(64bit) for package: gssproxy-0.7.0-29.el7.x86_64
--> Processing Dependency: libini_config.so.3(INI_CONFIG_1.1.0)(64bit) for package: gssproxy-0.7.0-29.el7.x86_64
--> Processing Dependency: libverto.so.1()(64bit) for package: gssproxy-0.7.0-29.el7.x86_64
--> Processing Dependency: libref_array.so.1()(64bit) for package: gssproxy-0.7.0-29.el7.x86_64
--> Processing Dependency: libini_config.so.3()(64bit) for package: gssproxy-0.7.0-29.el7.x86_64
--> Processing Dependency: libcollection.so.2()(64bit) for package: gssproxy-0.7.0-29.el7.x86_64
--> Processing Dependency: libbasicobjects.so.0()(64bit) for package: gssproxy-0.7.0-29.el7.x86_64
---> Package hostname.x86_64 0:3.13-3.el7_7.1 will be installed
---> Package info.x86_64 0:5.1-5.el7 will be installed
---> Package initscripts.x86_64 0:9.49.53-1.el7 will be installed
--> Processing Dependency: sysvinit-tools >= 2.87-5 for package: initscripts-9.49.53-1.el7.x86_64
---> Package iproute.x86_64 0:4.11.0-30.el7 will be installed
--> Processing Dependency: libmnl.so.0(LIBMNL_1.0)(64bit) for package: iproute-4.11.0-30.el7.x86_64
--> Processing Dependency: libxtables.so.10()(64bit) for package: iproute-4.11.0-30.el7.x86_64
--> Processing Dependency: libmnl.so.0()(64bit) for package: iproute-4.11.0-30.el7.x86_64
---> Package keyutils.x86_64 0:1.5.8-3.el7 will be installed
---> Package keyutils-libs.x86_64 0:1.5.8-3.el7 will be installed
---> Package kmod.x86_64 0:20-28.el7 will be installed
--> Processing Dependency: diffutils for package: kmod-20-28.el7.x86_64
--> Processing Dependency: /usr/bin/nm for package: kmod-20-28.el7.x86_64
---> Package krb5-libs.x86_64 0:1.15.1-50.el7 will be installed
---> Package libacl.x86_64 0:2.2.51-15.el7 will be installed
---> Package libattr.x86_64 0:2.4.46-13.el7 will be installed
---> Package libblkid.x86_64 0:2.23.2-65.el7 will be installed
---> Package libcap.x86_64 0:2.22-11.el7 will be installed
---> Package libcap-ng.x86_64 0:0.7.5-4.el7 will be installed
---> Package libcom_err.x86_64 0:1.42.9-19.el7 will be installed
---> Package libdb.x86_64 0:5.3.21-25.el7 will be installed
---> Package libdb-utils.x86_64 0:5.3.21-25.el7 will be installed
---> Package libedit.x86_64 0:3.0-12.20121213cvs.el7 will be installed
---> Package libestr.x86_64 0:0.1.9-2.el7 will be installed
---> Package libevent.x86_64 0:2.0.21-4.el7 will be installed
---> Package libfastjson.x86_64 0:0.99.4-3.el7 will be installed
---> Package libgcc.x86_64 0:4.8.5-44.el7 will be installed
---> Package libidn.x86_64 0:1.28-4.el7 will be installed
---> Package libmount.x86_64 0:2.23.2-65.el7 will be installed
---> Package libnfsidmap.x86_64 0:0.25-19.el7 will be installed
---> Package libselinux.x86_64 0:2.5-15.el7 will be installed
---> Package libsepol.x86_64 0:2.5-10.el7 will be installed
---> Package libss.x86_64 0:1.42.9-19.el7 will be installed
---> Package libtirpc.x86_64 0:0.2.4-0.16.el7 will be installed
---> Package libuuid.x86_64 0:2.23.2-65.el7 will be installed
---> Package linux-firmware.noarch 0:20200421-79.git78c0348.el7 will be installed
---> Package logrotate.x86_64 0:3.8.6-19.el7 will be installed
---> Package lua.x86_64 0:5.1.4-15.el7 will be installed
---> Package make.x86_64 1:3.82-24.el7 will be installed
---> Package ncurses-libs.x86_64 0:5.9-14.20130511.el7_4 will be installed
--> Processing Dependency: ncurses-base = 5.9-14.20130511.el7_4 for package: ncurses-libs-5.9-14.20130511.el7_4.x86_64
--> Processing Dependency: libstdc++.so.6(GLIBCXX_3.4)(64bit) for package: ncurses-libs-5.9-14.20130511.el7_4.x86_64
--> Processing Dependency: libstdc++.so.6(CXXABI_1.3)(64bit) for package: ncurses-libs-5.9-14.20130511.el7_4.x86_64
--> Processing Dependency: libstdc++.so.6()(64bit) for package: ncurses-libs-5.9-14.20130511.el7_4.x86_64
---> Package nss.x86_64 0:3.44.0-7.el7_7 will be installed
--> Processing Dependency: nss-softokn(x86-64) >= 3.44.0-1 for package: nss-3.44.0-7.el7_7.x86_64
--> Processing Dependency: nss-system-init for package: nss-3.44.0-7.el7_7.x86_64
--> Processing Dependency: nss-pem(x86-64) for package: nss-3.44.0-7.el7_7.x86_64
---> Package ntpdate.x86_64 0:4.2.6p5-29.el7.centos.2 will be installed
---> Package numactl-libs.x86_64 0:2.0.12-5.el7 will be installed
---> Package openldap.x86_64 0:2.4.44-22.el7 will be installed
--> Processing Dependency: nss-tools for package: openldap-2.4.44-22.el7.x86_64
--> Processing Dependency: libsasl2.so.3()(64bit) for package: openldap-2.4.44-22.el7.x86_64
---> Package openssh.x86_64 0:7.4p1-21.el7 will be installed
---> Package openssl-libs.x86_64 1:1.0.2k-19.el7 will be installed
--> Processing Dependency: ca-certificates >= 2008-5 for package: 1:openssl-libs-1.0.2k-19.el7.x86_64
---> Package pam.x86_64 0:1.1.8-23.el7 will be installed
--> Processing Dependency: libpwquality >= 0.9.9 for package: pam-1.1.8-23.el7.x86_64
--> Processing Dependency: cracklib-dicts >= 2.8 for package: pam-1.1.8-23.el7.x86_64
--> Processing Dependency: libcrack.so.2()(64bit) for package: pam-1.1.8-23.el7.x86_64
---> Package pcre.x86_64 0:8.32-17.el7 will be installed
---> Package popt.x86_64 0:1.13-16.el7 will be installed
---> Package python.x86_64 0:2.7.5-89.el7 will be installed
--> Processing Dependency: python-libs(x86-64) = 2.7.5-89.el7 for package: python-2.7.5-89.el7.x86_64
--> Processing Dependency: libpython2.7.so.1.0()(64bit) for package: python-2.7.5-89.el7.x86_64
---> Package quota.x86_64 1:4.01-19.el7 will be installed
--> Processing Dependency: quota-nls = 1:4.01-19.el7 for package: 1:quota-4.01-19.el7.x86_64
--> Processing Dependency: tcp_wrappers for package: 1:quota-4.01-19.el7.x86_64
---> Package readline.x86_64 0:6.2-11.el7 will be installed
---> Package rpcbind.x86_64 0:0.2.0-49.el7 will be installed
--> Processing Dependency: systemd-sysv for package: rpcbind-0.2.0-49.el7.x86_64
---> Package rpm-libs.x86_64 0:4.11.3-45.el7 will be installed
---> Package sed.x86_64 0:4.2.2-7.el7 will be installed
---> Package shadow-utils.x86_64 2:4.6-5.el7 will be installed
--> Processing Dependency: libsemanage.so.1(LIBSEMANAGE_1.0)(64bit) for package: 2:shadow-utils-4.6-5.el7.x86_64
--> Processing Dependency: libsemanage.so.1()(64bit) for package: 2:shadow-utils-4.6-5.el7.x86_64
---> Package sqlite.x86_64 0:3.7.17-8.el7_7.1 will be installed
---> Package systemd.x86_64 0:219-78.el7 will be installed
--> Processing Dependency: libkmod.so.2(LIBKMOD_5)(64bit) for package: systemd-219-78.el7.x86_64
--> Processing Dependency: libgcrypt.so.11(GCRYPT_1.2)(64bit) for package: systemd-219-78.el7.x86_64
--> Processing Dependency: libdw.so.1(ELFUTILS_0.158)(64bit) for package: systemd-219-78.el7.x86_64
--> Processing Dependency: libdw.so.1(ELFUTILS_0.130)(64bit) for package: systemd-219-78.el7.x86_64
--> Processing Dependency: libdw.so.1(ELFUTILS_0.122)(64bit) for package: systemd-219-78.el7.x86_64
--> Processing Dependency: libcryptsetup.so.12(CRYPTSETUP_2.0)(64bit) for package: systemd-219-78.el7.x86_64
--> Processing Dependency: dbus for package: systemd-219-78.el7.x86_64
--> Processing Dependency: acl for package: systemd-219-78.el7.x86_64
--> Processing Dependency: libqrencode.so.3()(64bit) for package: systemd-219-78.el7.x86_64
--> Processing Dependency: liblz4.so.1()(64bit) for package: systemd-219-78.el7.x86_64
--> Processing Dependency: libkmod.so.2()(64bit) for package: systemd-219-78.el7.x86_64
--> Processing Dependency: libgcrypt.so.11()(64bit) for package: systemd-219-78.el7.x86_64
--> Processing Dependency: libdw.so.1()(64bit) for package: systemd-219-78.el7.x86_64
--> Processing Dependency: libcryptsetup.so.12()(64bit) for package: systemd-219-78.el7.x86_64
---> Package systemd-libs.x86_64 0:219-78.el7 will be installed
--> Processing Dependency: libgpg-error.so.0()(64bit) for package: systemd-libs-219-78.el7.x86_64
---> Package tcp_wrappers-libs.x86_64 0:7.6-77.el7 will be installed
---> Package util-linux.x86_64 0:2.23.2-65.el7 will be installed
--> Processing Dependency: libsmartcols = 2.23.2-65.el7 for package: util-linux-2.23.2-65.el7.x86_64
--> Processing Dependency: libutempter.so.0(UTEMPTER_1.1)(64bit) for package: util-linux-2.23.2-65.el7.x86_64
--> Processing Dependency: libsmartcols.so.1(SMARTCOLS_2.25)(64bit) for package: util-linux-2.23.2-65.el7.x86_64
--> Processing Dependency: libutempter.so.0()(64bit) for package: util-linux-2.23.2-65.el7.x86_64
--> Processing Dependency: libuser.so.1()(64bit) for package: util-linux-2.23.2-65.el7.x86_64
--> Processing Dependency: libsmartcols.so.1()(64bit) for package: util-linux-2.23.2-65.el7.x86_64
---> Package xz-libs.x86_64 0:5.2.2-1.el7 will be installed
---> Package zlib.x86_64 0:1.2.7-18.el7 will be installed
--> Running transaction check
---> Package acl.x86_64 0:2.2.51-15.el7 will be installed
---> Package basesystem.noarch 0:10.0-7.el7.centos will be installed
---> Package binutils.x86_64 0:2.27-44.base.el7 will be installed
---> Package ca-certificates.noarch 0:2020.2.41-70.0.el7_8 will be installed
--> Processing Dependency: p11-kit-trust >= 0.23.5 for package: ca-certificates-2020.2.41-70.0.el7_8.noarch
--> Processing Dependency: p11-kit >= 0.23.5 for package: ca-certificates-2020.2.41-70.0.el7_8.noarch
---> Package cpio.x86_64 0:2.11-28.el7 will be installed
---> Package cracklib.x86_64 0:2.9.0-11.el7 will be installed
---> Package cracklib-dicts.x86_64 0:2.9.0-11.el7 will be installed
---> Package cryptsetup-libs.x86_64 0:2.0.3-6.el7 will be installed
--> Processing Dependency: libjson-c.so.2()(64bit) for package: cryptsetup-libs-2.0.3-6.el7.x86_64
---> Package cyrus-sasl-lib.x86_64 0:2.1.26-23.el7 will be installed
---> Package dbus.x86_64 1:1.10.24-15.el7 will be installed
--> Processing Dependency: dbus-libs(x86-64) = 1:1.10.24-15.el7 for package: 1:dbus-1.10.24-15.el7.x86_64
--> Processing Dependency: libdbus-1.so.3(LIBDBUS_PRIVATE_1.10.24)(64bit) for package: 1:dbus-1.10.24-15.el7.x86_64
--> Processing Dependency: libdbus-1.so.3(LIBDBUS_1_3)(64bit) for package: 1:dbus-1.10.24-15.el7.x86_64
--> Processing Dependency: libexpat.so.1()(64bit) for package: 1:dbus-1.10.24-15.el7.x86_64
--> Processing Dependency: libdbus-1.so.3()(64bit) for package: 1:dbus-1.10.24-15.el7.x86_64
---> Package device-mapper.x86_64 7:1.02.170-6.el7 will be installed
---> Package diffutils.x86_64 0:3.3-5.el7 will be installed
---> Package elfutils-libs.x86_64 0:0.176-5.el7 will be installed
--> Processing Dependency: default-yama-scope for package: elfutils-libs-0.176-5.el7.x86_64
---> Package findutils.x86_64 1:4.5.11-6.el7 will be installed
---> Package fipscheck.x86_64 0:1.4.1-6.el7 will be installed
---> Package glibc-common.x86_64 0:2.17-317.el7 will be installed
--> Processing Dependency: tzdata >= 2003a for package: glibc-common-2.17-317.el7.x86_64
---> Package gmp.x86_64 1:6.0.0-15.el7 will be installed
---> Package hardlink.x86_64 1:1.0-19.el7 will be installed
---> Package iptables.x86_64 0:1.4.21-35.el7 will be installed
--> Processing Dependency: libnfnetlink.so.0()(64bit) for package: iptables-1.4.21-35.el7.x86_64
--> Processing Dependency: libnetfilter_conntrack.so.3()(64bit) for package: iptables-1.4.21-35.el7.x86_64
---> Package kmod-libs.x86_64 0:20-28.el7 will be installed
---> Package kpartx.x86_64 0:0.4.9-133.el7 will be installed
---> Package libbasicobjects.x86_64 0:0.1.1-32.el7 will be installed
---> Package libcollection.x86_64 0:0.7.0-32.el7 will be installed
---> Package libcurl.x86_64 0:7.29.0-59.el7 will be installed
--> Processing Dependency: libssh2(x86-64) >= 1.8.0 for package: libcurl-7.29.0-59.el7.x86_64
--> Processing Dependency: libssh2.so.1()(64bit) for package: libcurl-7.29.0-59.el7.x86_64
---> Package libffi.x86_64 0:3.0.13-19.el7 will be installed
---> Package libgcrypt.x86_64 0:1.5.3-14.el7 will be installed
---> Package libgpg-error.x86_64 0:1.12-3.el7 will be installed
---> Package libini_config.x86_64 0:1.3.1-32.el7 will be installed
--> Processing Dependency: libpath_utils.so.1(PATH_UTILS_0.2.1)(64bit) for package: libini_config-1.3.1-32.el7.x86_64
--> Processing Dependency: libpath_utils.so.1()(64bit) for package: libini_config-1.3.1-32.el7.x86_64
---> Package libmnl.x86_64 0:1.0.3-7.el7 will be installed
---> Package libpwquality.x86_64 0:1.2.3-5.el7 will be installed
---> Package libref_array.x86_64 0:0.1.5-32.el7 will be installed
---> Package libsemanage.x86_64 0:2.5-14.el7 will be installed
--> Processing Dependency: libustr-1.0.so.1(USTR_1.0.1)(64bit) for package: libsemanage-2.5-14.el7.x86_64
--> Processing Dependency: libustr-1.0.so.1(USTR_1.0)(64bit) for package: libsemanage-2.5-14.el7.x86_64
--> Processing Dependency: libustr-1.0.so.1()(64bit) for package: libsemanage-2.5-14.el7.x86_64
---> Package libsmartcols.x86_64 0:2.23.2-65.el7 will be installed
---> Package libstdc++.x86_64 0:4.8.5-44.el7 will be installed
---> Package libuser.x86_64 0:0.60-9.el7 will be installed
---> Package libutempter.x86_64 0:1.1.6-4.el7 will be installed
---> Package libverto.x86_64 0:0.2.5-4.el7 will be installed
---> Package libverto-libevent.x86_64 0:0.2.5-4.el7 will be installed
---> Package lz4.x86_64 0:1.8.3-1.el7 will be installed
---> Package ncurses.x86_64 0:5.9-14.20130511.el7_4 will be installed
---> Package ncurses-base.noarch 0:5.9-14.20130511.el7_4 will be installed
---> Package nspr.x86_64 0:4.21.0-1.el7 will be installed
---> Package nss-pem.x86_64 0:1.0.3-7.el7 will be installed
---> Package nss-softokn.x86_64 0:3.44.0-8.el7_7 will be installed
---> Package nss-softokn-freebl.x86_64 0:3.44.0-8.el7_7 will be installed
---> Package nss-sysinit.x86_64 0:3.44.0-7.el7_7 will be installed
---> Package nss-tools.x86_64 0:3.44.0-7.el7_7 will be installed
---> Package nss-util.x86_64 0:3.44.0-4.el7_7 will be installed
---> Package pkgconfig.x86_64 1:0.27.1-4.el7 will be installed
---> Package python-libs.x86_64 0:2.7.5-89.el7 will be installed
--> Processing Dependency: libgdbm_compat.so.4()(64bit) for package: python-libs-2.7.5-89.el7.x86_64
--> Processing Dependency: libgdbm.so.4()(64bit) for package: python-libs-2.7.5-89.el7.x86_64
---> Package qrencode-libs.x86_64 0:3.4.1-3.el7 will be installed
---> Package quota-nls.noarch 1:4.01-19.el7 will be installed
---> Package setup.noarch 0:2.8.71-11.el7 will be installed
---> Package shared-mime-info.x86_64 0:1.8-5.el7 will be installed
--> Processing Dependency: libxml2.so.2(LIBXML2_2.4.30)(64bit) for package: shared-mime-info-1.8-5.el7.x86_64
--> Processing Dependency: libxml2.so.2()(64bit) for package: shared-mime-info-1.8-5.el7.x86_64
---> Package systemd-sysv.x86_64 0:219-78.el7 will be installed
---> Package sysvinit-tools.x86_64 0:2.88-14.dsf.el7 will be installed
---> Package tcp_wrappers.x86_64 0:7.6-77.el7 will be installed
--> Running transaction check
---> Package dbus-libs.x86_64 1:1.10.24-15.el7 will be installed
---> Package elfutils-default-yama-scope.noarch 0:0.176-5.el7 will be installed
---> Package expat.x86_64 0:2.1.0-12.el7 will be installed
---> Package gdbm.x86_64 0:1.10-8.el7 will be installed
---> Package json-c.x86_64 0:0.11-4.el7_0 will be installed
---> Package libnetfilter_conntrack.x86_64 0:1.0.6-1.el7_3 will be installed
---> Package libnfnetlink.x86_64 0:1.0.1-4.el7 will be installed
---> Package libpath_utils.x86_64 0:0.2.1-32.el7 will be installed
---> Package libssh2.x86_64 0:1.8.0-4.el7 will be installed
---> Package libxml2.x86_64 0:2.9.1-6.el7.5 will be installed
---> Package p11-kit.x86_64 0:0.23.5-3.el7 will be installed
---> Package p11-kit-trust.x86_64 0:0.23.5-3.el7 will be installed
--> Processing Dependency: libtasn1.so.6(LIBTASN1_0_3)(64bit) for package: p11-kit-trust-0.23.5-3.el7.x86_64
--> Processing Dependency: libtasn1.so.6()(64bit) for package: p11-kit-trust-0.23.5-3.el7.x86_64
---> Package tzdata.noarch 0:2020a-1.el7 will be installed
---> Package ustr.x86_64 0:1.0.4-16.el7 will be installed
--> Running transaction check
---> Package libtasn1.x86_64 0:4.10-1.el7 will be installed
--> Finished Dependency Resolution
Dependencies Resolved
================================================================================
 Package             Arch   Version                    Repository          Size
================================================================================
Installing:
 bash                x86_64 4.2.46-34.el7              centos7.9-x86_64-0 1.0 M
 bc                  x86_64 1.06.95-13.el7             centos7.9-x86_64-0 115 k
 dhclient            x86_64 12:4.2.5-82.el7.centos     centos7.9-x86_64-0 286 k
 dracut-network      x86_64 033-572.el7                centos7.9-x86_64-0 103 k
 e2fsprogs           x86_64 1.42.9-19.el7              centos7.9-x86_64-0 701 k
 ethtool             x86_64 2:4.8-10.el7               centos7.9-x86_64-0 127 k
 gzip                x86_64 1.5-10.el7                 centos7.9-x86_64-0 130 k
 iputils             x86_64 20160308-10.el7            centos7.9-x86_64-0 148 k
 irqbalance          x86_64 3:1.0.7-12.el7             centos7.9-x86_64-0  45 k
 kernel              x86_64 3.10.0-1160.el7            centos7.9-x86_64-0  50 M
 net-tools           x86_64 2.0-0.25.20131004git.el7   centos7.9-x86_64-0 306 k
 nfs-utils           x86_64 1:1.3.0-0.68.el7           centos7.9-x86_64-0 412 k
 ntp                 x86_64 4.2.6p5-29.el7.centos.2    centos7.9-x86_64-0 549 k
 openssh-clients     x86_64 7.4p1-21.el7               centos7.9-x86_64-0 655 k
 openssh-server      x86_64 7.4p1-21.el7               centos7.9-x86_64-0 459 k
 openssl             x86_64 1:1.0.2k-19.el7            centos7.9-x86_64-0 493 k
 parted              x86_64 3.1-32.el7                 centos7.9-x86_64-0 609 k
 procps-ng           x86_64 3.3.10-28.el7              centos7.9-x86_64-0 291 k
 rpm                 x86_64 4.11.3-45.el7              centos7.9-x86_64-0 1.2 M
 rsync               x86_64 3.1.2-10.el7               centos7.9-x86_64-0 404 k
 rsyslog             x86_64 8.24.0-55.el7              centos7.9-x86_64-0 621 k
 tar                 x86_64 2:1.26-35.el7              centos7.9-x86_64-0 846 k
 vim-minimal         x86_64 2:7.4.629-7.el7            centos7.9-x86_64-0 443 k
 wget                x86_64 1.14-18.el7_6.1            centos7.9-x86_64-0 547 k
 xz                  x86_64 5.2.2-1.el7                centos7.9-x86_64-0 229 k
Installing for dependencies:
 acl                 x86_64 2.2.51-15.el7              centos7.9-x86_64-0  81 k
 audit-libs          x86_64 2.8.5-4.el7                centos7.9-x86_64-0 102 k
 autogen-libopts     x86_64 5.18-5.el7                 centos7.9-x86_64-0  66 k
 basesystem          noarch 10.0-7.el7.centos          centos7.9-x86_64-0 5.0 k
 bind-export-libs    x86_64 32:9.11.4-26.P2.el7        centos7.9-x86_64-0 1.1 M
 binutils            x86_64 2.27-44.base.el7           centos7.9-x86_64-0 5.9 M
 bzip2-libs          x86_64 1.0.6-13.el7               centos7.9-x86_64-0  40 k
 ca-certificates     noarch 2020.2.41-70.0.el7_8       centos7.9-x86_64-0 382 k
 centos-release      x86_64 7-9.2009.0.el7.centos      centos7.9-x86_64-0  27 k
 chkconfig           x86_64 1.7.6-1.el7                centos7.9-x86_64-0 182 k
 coreutils           x86_64 8.22-24.el7                centos7.9-x86_64-0 3.3 M
 cpio                x86_64 2.11-28.el7                centos7.9-x86_64-0 211 k
 cracklib            x86_64 2.9.0-11.el7               centos7.9-x86_64-0  80 k
 cracklib-dicts      x86_64 2.9.0-11.el7               centos7.9-x86_64-0 3.6 M
 cryptsetup-libs     x86_64 2.0.3-6.el7                centos7.9-x86_64-0 339 k
 curl                x86_64 7.29.0-59.el7              centos7.9-x86_64-0 271 k
 cyrus-sasl-lib      x86_64 2.1.26-23.el7              centos7.9-x86_64-0 155 k
 dbus                x86_64 1:1.10.24-15.el7           centos7.9-x86_64-0 245 k
 dbus-libs           x86_64 1:1.10.24-15.el7           centos7.9-x86_64-0 169 k
 device-mapper       x86_64 7:1.02.170-6.el7           centos7.9-x86_64-0 297 k
 device-mapper-libs  x86_64 7:1.02.170-6.el7           centos7.9-x86_64-0 325 k
 dhcp-common         x86_64 12:4.2.5-82.el7.centos     centos7.9-x86_64-0 176 k
 dhcp-libs           x86_64 12:4.2.5-82.el7.centos     centos7.9-x86_64-0 133 k
 diffutils           x86_64 3.3-5.el7                  centos7.9-x86_64-0 322 k
 dracut              x86_64 033-572.el7                centos7.9-x86_64-0 329 k
 e2fsprogs-libs      x86_64 1.42.9-19.el7              centos7.9-x86_64-0 168 k
 elfutils-default-yama-scope
                     noarch 0.176-5.el7                centos7.9-x86_64-0  33 k
 elfutils-libelf     x86_64 0.176-5.el7                centos7.9-x86_64-0 195 k
 elfutils-libs       x86_64 0.176-5.el7                centos7.9-x86_64-0 291 k
 expat               x86_64 2.1.0-12.el7               centos7.9-x86_64-0  81 k
 filesystem          x86_64 3.2-25.el7                 centos7.9-x86_64-0 1.0 M
 findutils           x86_64 1:4.5.11-6.el7             centos7.9-x86_64-0 559 k
 fipscheck           x86_64 1.4.1-6.el7                centos7.9-x86_64-0  21 k
 fipscheck-lib       x86_64 1.4.1-6.el7                centos7.9-x86_64-0  11 k
 gawk                x86_64 4.0.2-4.el7_3.1            centos7.9-x86_64-0 874 k
 gdbm                x86_64 1.10-8.el7                 centos7.9-x86_64-0  70 k
 glib2               x86_64 2.56.1-7.el7               centos7.9-x86_64-0 2.5 M
 glibc               x86_64 2.17-317.el7               centos7.9-x86_64-0 3.6 M
 glibc-common        x86_64 2.17-317.el7               centos7.9-x86_64-0  11 M
 gmp                 x86_64 1:6.0.0-15.el7             centos7.9-x86_64-0 281 k
 grep                x86_64 2.20-3.el7                 centos7.9-x86_64-0 344 k
 grubby              x86_64 8.28-26.el7                centos7.9-x86_64-0  71 k
 gssproxy            x86_64 0.7.0-29.el7               centos7.9-x86_64-0 111 k
 hardlink            x86_64 1:1.0-19.el7               centos7.9-x86_64-0  14 k
 hostname            x86_64 3.13-3.el7_7.1             centos7.9-x86_64-0  17 k
 info                x86_64 5.1-5.el7                  centos7.9-x86_64-0 233 k
 initscripts         x86_64 9.49.53-1.el7              centos7.9-x86_64-0 440 k
 iproute             x86_64 4.11.0-30.el7              centos7.9-x86_64-0 805 k
 iptables            x86_64 1.4.21-35.el7              centos7.9-x86_64-0 432 k
 json-c              x86_64 0.11-4.el7_0               centos7.9-x86_64-0  31 k
 keyutils            x86_64 1.5.8-3.el7                centos7.9-x86_64-0  54 k
 keyutils-libs       x86_64 1.5.8-3.el7                centos7.9-x86_64-0  25 k
 kmod                x86_64 20-28.el7                  centos7.9-x86_64-0 123 k
 kmod-libs           x86_64 20-28.el7                  centos7.9-x86_64-0  51 k
 kpartx              x86_64 0.4.9-133.el7              centos7.9-x86_64-0  80 k
 krb5-libs           x86_64 1.15.1-50.el7              centos7.9-x86_64-0 809 k
 libacl              x86_64 2.2.51-15.el7              centos7.9-x86_64-0  27 k
 libattr             x86_64 2.4.46-13.el7              centos7.9-x86_64-0  18 k
 libbasicobjects     x86_64 0.1.1-32.el7               centos7.9-x86_64-0  26 k
 libblkid            x86_64 2.23.2-65.el7              centos7.9-x86_64-0 183 k
 libcap              x86_64 2.22-11.el7                centos7.9-x86_64-0  47 k
 libcap-ng           x86_64 0.7.5-4.el7                centos7.9-x86_64-0  25 k
 libcollection       x86_64 0.7.0-32.el7               centos7.9-x86_64-0  42 k
 libcom_err          x86_64 1.42.9-19.el7              centos7.9-x86_64-0  42 k
 libcurl             x86_64 7.29.0-59.el7              centos7.9-x86_64-0 223 k
 libdb               x86_64 5.3.21-25.el7              centos7.9-x86_64-0 720 k
 libdb-utils         x86_64 5.3.21-25.el7              centos7.9-x86_64-0 132 k
 libedit             x86_64 3.0-12.20121213cvs.el7     centos7.9-x86_64-0  92 k
 libestr             x86_64 0.1.9-2.el7                centos7.9-x86_64-0  20 k
 libevent            x86_64 2.0.21-4.el7               centos7.9-x86_64-0 214 k
 libfastjson         x86_64 0.99.4-3.el7               centos7.9-x86_64-0  27 k
 libffi              x86_64 3.0.13-19.el7              centos7.9-x86_64-0  30 k
 libgcc              x86_64 4.8.5-44.el7               centos7.9-x86_64-0 103 k
 libgcrypt           x86_64 1.5.3-14.el7               centos7.9-x86_64-0 263 k
 libgpg-error        x86_64 1.12-3.el7                 centos7.9-x86_64-0  87 k
 libidn              x86_64 1.28-4.el7                 centos7.9-x86_64-0 209 k
 libini_config       x86_64 1.3.1-32.el7               centos7.9-x86_64-0  64 k
 libmnl              x86_64 1.0.3-7.el7                centos7.9-x86_64-0  23 k
 libmount            x86_64 2.23.2-65.el7              centos7.9-x86_64-0 184 k
 libnetfilter_conntrack
                     x86_64 1.0.6-1.el7_3              centos7.9-x86_64-0  55 k
 libnfnetlink        x86_64 1.0.1-4.el7                centos7.9-x86_64-0  26 k
 libnfsidmap         x86_64 0.25-19.el7                centos7.9-x86_64-0  50 k
 libpath_utils       x86_64 0.2.1-32.el7               centos7.9-x86_64-0  28 k
 libpwquality        x86_64 1.2.3-5.el7                centos7.9-x86_64-0  85 k
 libref_array        x86_64 0.1.5-32.el7               centos7.9-x86_64-0  27 k
 libselinux          x86_64 2.5-15.el7                 centos7.9-x86_64-0 162 k
 libsemanage         x86_64 2.5-14.el7                 centos7.9-x86_64-0 151 k
 libsepol            x86_64 2.5-10.el7                 centos7.9-x86_64-0 297 k
 libsmartcols        x86_64 2.23.2-65.el7              centos7.9-x86_64-0 142 k
 libss               x86_64 1.42.9-19.el7              centos7.9-x86_64-0  47 k
 libssh2             x86_64 1.8.0-4.el7                centos7.9-x86_64-0  88 k
 libstdc++           x86_64 4.8.5-44.el7               centos7.9-x86_64-0 306 k
 libtasn1            x86_64 4.10-1.el7                 centos7.9-x86_64-0 320 k
 libtirpc            x86_64 0.2.4-0.16.el7             centos7.9-x86_64-0  89 k
 libuser             x86_64 0.60-9.el7                 centos7.9-x86_64-0 400 k
 libutempter         x86_64 1.1.6-4.el7                centos7.9-x86_64-0  25 k
 libuuid             x86_64 2.23.2-65.el7              centos7.9-x86_64-0  84 k
 libverto            x86_64 0.2.5-4.el7                centos7.9-x86_64-0  16 k
 libverto-libevent   x86_64 0.2.5-4.el7                centos7.9-x86_64-0 8.9 k
 libxml2             x86_64 2.9.1-6.el7.5              centos7.9-x86_64-0 668 k
 linux-firmware      noarch 20200421-79.git78c0348.el7 centos7.9-x86_64-0  80 M
 logrotate           x86_64 3.8.6-19.el7               centos7.9-x86_64-0  70 k
 lua                 x86_64 5.1.4-15.el7               centos7.9-x86_64-0 201 k
 lz4                 x86_64 1.8.3-1.el7                centos7.9-x86_64-0  85 k
 make                x86_64 1:3.82-24.el7              centos7.9-x86_64-0 421 k
 ncurses             x86_64 5.9-14.20130511.el7_4      centos7.9-x86_64-0 304 k
 ncurses-base        noarch 5.9-14.20130511.el7_4      centos7.9-x86_64-0  68 k
 ncurses-libs        x86_64 5.9-14.20130511.el7_4      centos7.9-x86_64-0 316 k
 nspr                x86_64 4.21.0-1.el7               centos7.9-x86_64-0 127 k
 nss                 x86_64 3.44.0-7.el7_7             centos7.9-x86_64-0 854 k
 nss-pem             x86_64 1.0.3-7.el7                centos7.9-x86_64-0  74 k
 nss-softokn         x86_64 3.44.0-8.el7_7             centos7.9-x86_64-0 330 k
 nss-softokn-freebl  x86_64 3.44.0-8.el7_7             centos7.9-x86_64-0 224 k
 nss-sysinit         x86_64 3.44.0-7.el7_7             centos7.9-x86_64-0  65 k
 nss-tools           x86_64 3.44.0-7.el7_7             centos7.9-x86_64-0 528 k
 nss-util            x86_64 3.44.0-4.el7_7             centos7.9-x86_64-0  79 k
 ntpdate             x86_64 4.2.6p5-29.el7.centos.2    centos7.9-x86_64-0  87 k
 numactl-libs        x86_64 2.0.12-5.el7               centos7.9-x86_64-0  30 k
 openldap            x86_64 2.4.44-22.el7              centos7.9-x86_64-0 356 k
 openssh             x86_64 7.4p1-21.el7               centos7.9-x86_64-0 510 k
 openssl-libs        x86_64 1:1.0.2k-19.el7            centos7.9-x86_64-0 1.2 M
 p11-kit             x86_64 0.23.5-3.el7               centos7.9-x86_64-0 252 k
 p11-kit-trust       x86_64 0.23.5-3.el7               centos7.9-x86_64-0 129 k
 pam                 x86_64 1.1.8-23.el7               centos7.9-x86_64-0 721 k
 pcre                x86_64 8.32-17.el7                centos7.9-x86_64-0 422 k
 pkgconfig           x86_64 1:0.27.1-4.el7             centos7.9-x86_64-0  54 k
 popt                x86_64 1.13-16.el7                centos7.9-x86_64-0  42 k
 python              x86_64 2.7.5-89.el7               centos7.9-x86_64-0  96 k
 python-libs         x86_64 2.7.5-89.el7               centos7.9-x86_64-0 5.6 M
 qrencode-libs       x86_64 3.4.1-3.el7                centos7.9-x86_64-0  50 k
 quota               x86_64 1:4.01-19.el7              centos7.9-x86_64-0 179 k
 quota-nls           noarch 1:4.01-19.el7              centos7.9-x86_64-0  90 k
 readline            x86_64 6.2-11.el7                 centos7.9-x86_64-0 193 k
 rpcbind             x86_64 0.2.0-49.el7               centos7.9-x86_64-0  60 k
 rpm-libs            x86_64 4.11.3-45.el7              centos7.9-x86_64-0 278 k
 sed                 x86_64 4.2.2-7.el7                centos7.9-x86_64-0 231 k
 setup               noarch 2.8.71-11.el7              centos7.9-x86_64-0 166 k
 shadow-utils        x86_64 2:4.6-5.el7                centos7.9-x86_64-0 1.2 M
 shared-mime-info    x86_64 1.8-5.el7                  centos7.9-x86_64-0 312 k
 sqlite              x86_64 3.7.17-8.el7_7.1           centos7.9-x86_64-0 394 k
 systemd             x86_64 219-78.el7                 centos7.9-x86_64-0 5.1 M
 systemd-libs        x86_64 219-78.el7                 centos7.9-x86_64-0 418 k
 systemd-sysv        x86_64 219-78.el7                 centos7.9-x86_64-0  96 k
 sysvinit-tools      x86_64 2.88-14.dsf.el7            centos7.9-x86_64-0  63 k
 tcp_wrappers        x86_64 7.6-77.el7                 centos7.9-x86_64-0  78 k
 tcp_wrappers-libs   x86_64 7.6-77.el7                 centos7.9-x86_64-0  66 k
 tzdata              noarch 2020a-1.el7                centos7.9-x86_64-0 495 k
 ustr                x86_64 1.0.4-16.el7               centos7.9-x86_64-0  92 k
 util-linux          x86_64 2.23.2-65.el7              centos7.9-x86_64-0 2.0 M
 xz-libs             x86_64 5.2.2-1.el7                centos7.9-x86_64-0 103 k
 zlib                x86_64 1.2.7-18.el7               centos7.9-x86_64-0  90 k
Transaction Summary
================================================================================
Install  25 Packages (+151 Dependent packages)
Total download size: 214 M
Installed size: 910 M
Downloading packages:
--------------------------------------------------------------------------------
Total                                              439 MB/s | 214 MB  00:00     
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  Installing : libgcc-4.8.5-44.el7.x86_64                                 1/176 
  Installing : centos-release-7-9.2009.0.el7.centos.x86_64                2/176 
  Installing : setup-2.8.71-11.el7.noarch                                 3/176 
  Installing : filesystem-3.2-25.el7.x86_64                               4/176 
  Installing : basesystem-10.0-7.el7.centos.noarch                        5/176 
  Installing : ncurses-base-5.9-14.20130511.el7_4.noarch                  6/176 
  Installing : tzdata-2020a-1.el7.noarch                                  7/176 
  Installing : nss-softokn-freebl-3.44.0-8.el7_7.x86_64                   8/176 
  Installing : glibc-common-2.17-317.el7.x86_64                           9/176 
  Installing : glibc-2.17-317.el7.x86_64                                 10/176 
  Installing : nspr-4.21.0-1.el7.x86_64                                  11/176 
  Installing : nss-util-3.44.0-4.el7_7.x86_64                            12/176 
  Installing : libstdc++-4.8.5-44.el7.x86_64                             13/176 
  Installing : ncurses-libs-5.9-14.20130511.el7_4.x86_64                 14/176 
  Installing : bash-4.2.46-34.el7.x86_64                                 15/176 
  Installing : libsepol-2.5-10.el7.x86_64                                16/176 
  Installing : pcre-8.32-17.el7.x86_64                                   17/176 
  Installing : libselinux-2.5-15.el7.x86_64                              18/176 
  Installing : zlib-1.2.7-18.el7.x86_64                                  19/176 
  Installing : info-5.1-5.el7.x86_64                                     20/176 
  Installing : libcom_err-1.42.9-19.el7.x86_64                           21/176 
  Installing : popt-1.13-16.el7.x86_64                                   22/176 
  Installing : xz-libs-5.2.2-1.el7.x86_64                                23/176 
  Installing : libuuid-2.23.2-65.el7.x86_64                              24/176 
  Installing : chkconfig-1.7.6-1.el7.x86_64                              25/176 
  Installing : sed-4.2.2-7.el7.x86_64                                    26/176 
  Installing : libdb-5.3.21-25.el7.x86_64                                27/176 
  Installing : grep-2.20-3.el7.x86_64                                    28/176 
  Installing : bzip2-libs-1.0.6-13.el7.x86_64                            29/176 
  Installing : libattr-2.4.46-13.el7.x86_64                              30/176 
  Installing : libcap-2.22-11.el7.x86_64                                 31/176 
  Installing : libacl-2.2.51-15.el7.x86_64                               32/176 
  Installing : readline-6.2-11.el7.x86_64                                33/176 
  Installing : gawk-4.0.2-4.el7_3.1.x86_64                               34/176 
  Installing : tcp_wrappers-libs-7.6-77.el7.x86_64                       35/176 
  Installing : libcap-ng-0.7.5-4.el7.x86_64                              36/176 
  Installing : audit-libs-2.8.5-4.el7.x86_64                             37/176 
  Installing : elfutils-libelf-0.176-5.el7.x86_64                        38/176 
  Installing : keyutils-libs-1.5.8-3.el7.x86_64                          39/176 
  Installing : libffi-3.0.13-19.el7.x86_64                               40/176 
  Installing : sqlite-3.7.17-8.el7_7.1.x86_64                            41/176 
  Installing : 1:findutils-4.5.11-6.el7.x86_64                           42/176 
  Installing : libidn-1.28-4.el7.x86_64                                  43/176 
  Installing : cpio-2.11-28.el7.x86_64                                   44/176 
  Installing : libverto-0.2.5-4.el7.x86_64                               45/176 
  Installing : libgpg-error-1.12-3.el7.x86_64                            46/176 
  Installing : libgcrypt-1.5.3-14.el7.x86_64                             47/176 
  Installing : nss-softokn-3.44.0-8.el7_7.x86_64                         48/176 
  Installing : p11-kit-0.23.5-3.el7.x86_64                               49/176 
  Installing : lua-5.1.4-15.el7.x86_64                                   50/176 
  Installing : xz-5.2.2-1.el7.x86_64                                     51/176 
  Installing : e2fsprogs-libs-1.42.9-19.el7.x86_64                       52/176 
  Installing : diffutils-3.3-5.el7.x86_64                                53/176 
  Installing : libedit-3.0-12.20121213cvs.el7.x86_64                     54/176 
  Installing : libnfnetlink-1.0.1-4.el7.x86_64                           55/176 
  Installing : libbasicobjects-0.1.1-32.el7.x86_64                       56/176 
  Installing : libref_array-0.1.5-32.el7.x86_64                          57/176 
  Installing : libmnl-1.0.3-7.el7.x86_64                                 58/176 
  Installing : expat-2.1.0-12.el7.x86_64                                 59/176 
  Installing : hostname-3.13-3.el7_7.1.x86_64                            60/176 
  Installing : lz4-1.8.3-1.el7.x86_64                                    61/176 
  Installing : libcollection-0.7.0-32.el7.x86_64                         62/176 
  Installing : libnetfilter_conntrack-1.0.6-1.el7_3.x86_64               63/176 
  Installing : iptables-1.4.21-35.el7.x86_64                             64/176 
  Installing : iproute-4.11.0-30.el7.x86_64                              65/176 
  Installing : keyutils-1.5.8-3.el7.x86_64                               66/176 
  Installing : tcp_wrappers-7.6-77.el7.x86_64                            67/176 
  Installing : bc-1.06.95-13.el7.x86_64                                  68/176 
  Installing : acl-2.2.51-15.el7.x86_64                                  69/176 
  Installing : 2:tar-1.26-35.el7.x86_64                                  70/176 
  Installing : libdb-utils-5.3.21-25.el7.x86_64                          71/176 
  Installing : kmod-libs-20-28.el7.x86_64                                72/176 
  Installing : libxml2-2.9.1-6.el7.5.x86_64                              73/176 
  Installing : libss-1.42.9-19.el7.x86_64                                74/176 
  Installing : 1:make-3.82-24.el7.x86_64                                 75/176 
  Installing : linux-firmware-20200421-79.git78c0348.el7.noarch          76/176 
  Installing : ncurses-5.9-14.20130511.el7_4.x86_64                      77/176 
  Installing : 1:gmp-6.0.0-15.el7.x86_64                                 78/176 
  Installing : sysvinit-tools-2.88-14.dsf.el7.x86_64                     79/176 
  Installing : libpath_utils-0.2.1-32.el7.x86_64                         80/176 
  Installing : libini_config-1.3.1-32.el7.x86_64                         81/176 
  Installing : ustr-1.0.4-16.el7.x86_64                                  82/176 
  Installing : libsemanage-2.5-14.el7.x86_64                             83/176 
  Installing : autogen-libopts-5.18-5.el7.x86_64                         84/176 
  Installing : libtasn1-4.10-1.el7.x86_64                                85/176 
  Installing : p11-kit-trust-0.23.5-3.el7.x86_64                         86/176 
  Installing : ca-certificates-2020.2.41-70.0.el7_8.noarch               87/176 
  Installing : 1:openssl-libs-1.0.2k-19.el7.x86_64                       88/176 
  Installing : coreutils-8.22-24.el7.x86_64                              89/176 
  Installing : krb5-libs-1.15.1-50.el7.x86_64                            90/176 
  Installing : libblkid-2.23.2-65.el7.x86_64                             91/176 
  Installing : 2:shadow-utils-4.6-5.el7.x86_64                           92/176 
  Installing : libmount-2.23.2-65.el7.x86_64                             93/176 
  Installing : glib2-2.56.1-7.el7.x86_64                                 94/176 
  Installing : shared-mime-info-1.8-5.el7.x86_64                         95/176 
  Installing : gzip-1.5-10.el7.x86_64                                    96/176 
  Installing : cracklib-2.9.0-11.el7.x86_64                              97/176 
  Installing : cracklib-dicts-2.9.0-11.el7.x86_64                        98/176 
  Installing : pam-1.1.8-23.el7.x86_64                                   99/176 
  Installing : libpwquality-1.2.3-5.el7.x86_64                          100/176 
  Installing : libtirpc-0.2.4-0.16.el7.x86_64                           101/176 
  Installing : libevent-2.0.21-4.el7.x86_64                             102/176 
  Installing : libverto-libevent-0.2.5-4.el7.x86_64                     103/176 
  Installing : 1:pkgconfig-0.27.1-4.el7.x86_64                          104/176 
  Installing : libutempter-1.1.6-4.el7.x86_64                           105/176 
  Installing : grubby-8.28-26.el7.x86_64                                106/176 
  Installing : 32:bind-export-libs-9.11.4-26.P2.el7.x86_64              107/176 
  Installing : cyrus-sasl-lib-2.1.26-23.el7.x86_64                      108/176 
  Installing : nss-pem-1.0.3-7.el7.x86_64                               109/176 
  Installing : nss-3.44.0-7.el7_7.x86_64                                110/176 
  Installing : nss-sysinit-3.44.0-7.el7_7.x86_64                        111/176 
  Installing : nss-tools-3.44.0-7.el7_7.x86_64                          112/176 
  Installing : binutils-2.27-44.base.el7.x86_64                         113/176 
  Installing : logrotate-3.8.6-19.el7.x86_64                            114/176 
  Installing : libssh2-1.8.0-4.el7.x86_64                               115/176 
  Installing : libcurl-7.29.0-59.el7.x86_64                             116/176 
  Installing : curl-7.29.0-59.el7.x86_64                                117/176 
  Installing : rpm-libs-4.11.3-45.el7.x86_64                            118/176 
  Installing : rpm-4.11.3-45.el7.x86_64                                 119/176 
  Installing : openldap-2.4.44-22.el7.x86_64                            120/176 
  Installing : libnfsidmap-0.25-19.el7.x86_64                           121/176 
  Installing : libuser-0.60-9.el7.x86_64                                122/176 
  Installing : fipscheck-1.4.1-6.el7.x86_64                             123/176 
  Installing : fipscheck-lib-1.4.1-6.el7.x86_64                         124/176 
  Installing : qrencode-libs-3.4.1-3.el7.x86_64                         125/176 
  Installing : libfastjson-0.99.4-3.el7.x86_64                          126/176 
  Installing : gdbm-1.10-8.el7.x86_64                                   127/176 
  Installing : python-libs-2.7.5-89.el7.x86_64                          128/176 
  Installing : python-2.7.5-89.el7.x86_64                               129/176 
  Installing : libestr-0.1.9-2.el7.x86_64                               130/176 
  Installing : 1:hardlink-1.0-19.el7.x86_64                             131/176 
  Installing : json-c-0.11-4.el7_0.x86_64                               132/176 
  Installing : libsmartcols-2.23.2-65.el7.x86_64                        133/176 
  Installing : procps-ng-3.3.10-28.el7.x86_64                           134/176 
  Installing : 7:device-mapper-1.02.170-6.el7.x86_64                    135/176 
  Installing : kpartx-0.4.9-133.el7.x86_64                              136/176 
  Installing : util-linux-2.23.2-65.el7.x86_64                          137/176 
  Installing : 7:device-mapper-libs-1.02.170-6.el7.x86_64               138/176 
  Installing : cryptsetup-libs-2.0.3-6.el7.x86_64                       139/176 
  Installing : dracut-033-572.el7.x86_64                                140/176 
  Installing : kmod-20-28.el7.x86_64                                    141/176 
  Installing : elfutils-libs-0.176-5.el7.x86_64                         142/176 
  Installing : systemd-libs-219-78.el7.x86_64                           143/176 
  Installing : 1:dbus-libs-1.10.24-15.el7.x86_64                        144/176 
  Installing : systemd-219-78.el7.x86_64                                145/176 
Running in chroot, ignoring request.
  Installing : elfutils-default-yama-scope-0.176-5.el7.noarch           146/176 
  Installing : 1:dbus-1.10.24-15.el7.x86_64                             147/176 
  Installing : iputils-20160308-10.el7.x86_64                           148/176 
  Installing : initscripts-9.49.53-1.el7.x86_64                         149/176 
  Installing : 12:dhcp-libs-4.2.5-82.el7.centos.x86_64                  150/176 
  Installing : openssh-7.4p1-21.el7.x86_64                              151/176 
  Installing : 12:dhcp-common-4.2.5-82.el7.centos.x86_64                152/176 
  Installing : 12:dhclient-4.2.5-82.el7.centos.x86_64                   153/176 
  Installing : ntpdate-4.2.6p5-29.el7.centos.2.x86_64                   154/176 
  Installing : gssproxy-0.7.0-29.el7.x86_64                             155/176 
  Installing : systemd-sysv-219-78.el7.x86_64                           156/176 
  Installing : rpcbind-0.2.0-49.el7.x86_64                              157/176 
  Installing : numactl-libs-2.0.12-5.el7.x86_64                         158/176 
  Installing : 1:quota-nls-4.01-19.el7.noarch                           159/176 
  Installing : 1:quota-4.01-19.el7.x86_64                               160/176 
  Installing : 1:nfs-utils-1.3.0-0.68.el7.x86_64                        161/176 
  Installing : 3:irqbalance-1.0.7-12.el7.x86_64                         162/176 
  Installing : ntp-4.2.6p5-29.el7.centos.2.x86_64                       163/176 
  Installing : dracut-network-033-572.el7.x86_64                        164/176 
  Installing : openssh-server-7.4p1-21.el7.x86_64                       165/176 
  Installing : openssh-clients-7.4p1-21.el7.x86_64                      166/176 
  Installing : kernel-3.10.0-1160.el7.x86_64                            167/176 
  Installing : rsyslog-8.24.0-55.el7.x86_64                             168/176 
  Installing : rsync-3.1.2-10.el7.x86_64                                169/176 
  Installing : net-tools-2.0-0.25.20131004git.el7.x86_64                170/176 
  Installing : parted-3.1-32.el7.x86_64                                 171/176 
  Installing : e2fsprogs-1.42.9-19.el7.x86_64                           172/176 
  Installing : 1:openssl-1.0.2k-19.el7.x86_64                           173/176 
  Installing : wget-1.14-18.el7_6.1.x86_64                              174/176 
  Installing : 2:vim-minimal-7.4.629-7.el7.x86_64                       175/176 
  Installing : 2:ethtool-4.8-10.el7.x86_64                              176/176 
Turning off host-only mode: '/run' is not mounted!
Turning off host-only mode: '/dev' is not mounted!
  Verifying  : fipscheck-lib-1.4.1-6.el7.x86_64                           1/176 
  Verifying  : rpm-4.11.3-45.el7.x86_64                                   2/176 
  Verifying  : acl-2.2.51-15.el7.x86_64                                   3/176 
  Verifying  : 1:pkgconfig-0.27.1-4.el7.x86_64                            4/176 
  Verifying  : libacl-2.2.51-15.el7.x86_64                                5/176 
  Verifying  : libdb-utils-5.3.21-25.el7.x86_64                           6/176 
  Verifying  : libcap-2.22-11.el7.x86_64                                  7/176 
  Verifying  : nss-3.44.0-7.el7_7.x86_64                                  8/176 
  Verifying  : pcre-8.32-17.el7.x86_64                                    9/176 
  Verifying  : sysvinit-tools-2.88-14.dsf.el7.x86_64                     10/176 
  Verifying  : glib2-2.56.1-7.el7.x86_64                                 11/176 
  Verifying  : readline-6.2-11.el7.x86_64                                12/176 
  Verifying  : sqlite-3.7.17-8.el7_7.1.x86_64                            13/176 
  Verifying  : zlib-1.2.7-18.el7.x86_64                                  14/176 
  Verifying  : nss-pem-1.0.3-7.el7.x86_64                                15/176 
  Verifying  : systemd-219-78.el7.x86_64                                 16/176 
  Verifying  : grubby-8.28-26.el7.x86_64                                 17/176 
  Verifying  : 7:device-mapper-1.02.170-6.el7.x86_64                     18/176 
  Verifying  : openssh-server-7.4p1-21.el7.x86_64                        19/176 
  Verifying  : 1:findutils-4.5.11-6.el7.x86_64                           20/176 
  Verifying  : libselinux-2.5-15.el7.x86_64                              21/176 
  Verifying  : libblkid-2.23.2-65.el7.x86_64                             22/176 
  Verifying  : python-libs-2.7.5-89.el7.x86_64                           23/176 
  Verifying  : rpm-libs-4.11.3-45.el7.x86_64                             24/176 
  Verifying  : kmod-libs-20-28.el7.x86_64                                25/176 
  Verifying  : 12:dhcp-libs-4.2.5-82.el7.centos.x86_64                   26/176 
  Verifying  : 1:openssl-libs-1.0.2k-19.el7.x86_64                       27/176 
  Verifying  : iptables-1.4.21-35.el7.x86_64                             28/176 
  Verifying  : ntpdate-4.2.6p5-29.el7.centos.2.x86_64                    29/176 
  Verifying  : procps-ng-3.3.10-28.el7.x86_64                            30/176 
  Verifying  : libpath_utils-0.2.1-32.el7.x86_64                         31/176 
  Verifying  : libnfnetlink-1.0.1-4.el7.x86_64                           32/176 
  Verifying  : cracklib-dicts-2.9.0-11.el7.x86_64                        33/176 
  Verifying  : tcp_wrappers-libs-7.6-77.el7.x86_64                       34/176 
  Verifying  : elfutils-libs-0.176-5.el7.x86_64                          35/176 
  Verifying  : libedit-3.0-12.20121213cvs.el7.x86_64                     36/176 
  Verifying  : libini_config-1.3.1-32.el7.x86_64                         37/176 
  Verifying  : ca-certificates-2020.2.41-70.0.el7_8.noarch               38/176 
  Verifying  : ustr-1.0.4-16.el7.x86_64                                  39/176 
  Verifying  : lua-5.1.4-15.el7.x86_64                                   40/176 
  Verifying  : libgcc-4.8.5-44.el7.x86_64                                41/176 
  Verifying  : libutempter-1.1.6-4.el7.x86_64                            42/176 
  Verifying  : ntp-4.2.6p5-29.el7.centos.2.x86_64                        43/176 
  Verifying  : libuuid-2.23.2-65.el7.x86_64                              44/176 
  Verifying  : 2:vim-minimal-7.4.629-7.el7.x86_64                        45/176 
  Verifying  : setup-2.8.71-11.el7.noarch                                46/176 
  Verifying  : nss-tools-3.44.0-7.el7_7.x86_64                           47/176 
  Verifying  : kernel-3.10.0-1160.el7.x86_64                             48/176 
  Verifying  : autogen-libopts-5.18-5.el7.x86_64                         49/176 
  Verifying  : ncurses-libs-5.9-14.20130511.el7_4.x86_64                 50/176 
  Verifying  : chkconfig-1.7.6-1.el7.x86_64                              51/176 
  Verifying  : e2fsprogs-1.42.9-19.el7.x86_64                            52/176 
  Verifying  : pam-1.1.8-23.el7.x86_64                                   53/176 
  Verifying  : 12:dhclient-4.2.5-82.el7.centos.x86_64                    54/176 
  Verifying  : bzip2-libs-1.0.6-13.el7.x86_64                            55/176 
  Verifying  : libbasicobjects-0.1.1-32.el7.x86_64                       56/176 
  Verifying  : dracut-033-572.el7.x86_64                                 57/176 
  Verifying  : 1:dbus-libs-1.10.24-15.el7.x86_64                         58/176 
  Verifying  : nss-sysinit-3.44.0-7.el7_7.x86_64                         59/176 
  Verifying  : cryptsetup-libs-2.0.3-6.el7.x86_64                        60/176 
  Verifying  : libverto-libevent-0.2.5-4.el7.x86_64                      61/176 
  Verifying  : basesystem-10.0-7.el7.centos.noarch                       62/176 
  Verifying  : libverto-0.2.5-4.el7.x86_64                               63/176 
  Verifying  : rpcbind-0.2.0-49.el7.x86_64                               64/176 
  Verifying  : 1:make-3.82-24.el7.x86_64                                 65/176 
  Verifying  : info-5.1-5.el7.x86_64                                     66/176 
  Verifying  : initscripts-9.49.53-1.el7.x86_64                          67/176 
  Verifying  : 32:bind-export-libs-9.11.4-26.P2.el7.x86_64               68/176 
  Verifying  : rsyslog-8.24.0-55.el7.x86_64                              69/176 
  Verifying  : e2fsprogs-libs-1.42.9-19.el7.x86_64                       70/176 
  Verifying  : iputils-20160308-10.el7.x86_64                            71/176 
  Verifying  : openssh-clients-7.4p1-21.el7.x86_64                       72/176 
  Verifying  : 1:openssl-1.0.2k-19.el7.x86_64                            73/176 
  Verifying  : libsepol-2.5-10.el7.x86_64                                74/176 
  Verifying  : gssproxy-0.7.0-29.el7.x86_64                              75/176 
  Verifying  : libref_array-0.1.5-32.el7.x86_64                          76/176 
  Verifying  : 1:quota-nls-4.01-19.el7.noarch                            77/176 
  Verifying  : tzdata-2020a-1.el7.noarch                                 78/176 
  Verifying  : libcurl-7.29.0-59.el7.x86_64                              79/176 
  Verifying  : libssh2-1.8.0-4.el7.x86_64                                80/176 
  Verifying  : curl-7.29.0-59.el7.x86_64                                 81/176 
  Verifying  : libnfsidmap-0.25-19.el7.x86_64                            82/176 
  Verifying  : libuser-0.60-9.el7.x86_64                                 83/176 
  Verifying  : libtasn1-4.10-1.el7.x86_64                                84/176 
  Verifying  : keyutils-1.5.8-3.el7.x86_64                               85/176 
  Verifying  : rsync-3.1.2-10.el7.x86_64                                 86/176 
  Verifying  : cracklib-2.9.0-11.el7.x86_64                              87/176 
  Verifying  : libgpg-error-1.12-3.el7.x86_64                            88/176 
  Verifying  : nspr-4.21.0-1.el7.x86_64                                  89/176 
  Verifying  : parted-3.1-32.el7.x86_64                                  90/176 
  Verifying  : nss-softokn-3.44.0-8.el7_7.x86_64                         91/176 
  Verifying  : libmnl-1.0.3-7.el7.x86_64                                 92/176 
  Verifying  : popt-1.13-16.el7.x86_64                                   93/176 
  Verifying  : gzip-1.5-10.el7.x86_64                                    94/176 
  Verifying  : p11-kit-0.23.5-3.el7.x86_64                               95/176 
  Verifying  : 2:shadow-utils-4.6-5.el7.x86_64                           96/176 
  Verifying  : qrencode-libs-3.4.1-3.el7.x86_64                          97/176 
  Verifying  : 1:nfs-utils-1.3.0-0.68.el7.x86_64                         98/176 
  Verifying  : expat-2.1.0-12.el7.x86_64                                 99/176 
  Verifying  : binutils-2.27-44.base.el7.x86_64                         100/176 
  Verifying  : bc-1.06.95-13.el7.x86_64                                 101/176 
  Verifying  : libidn-1.28-4.el7.x86_64                                 102/176 
  Verifying  : gawk-4.0.2-4.el7_3.1.x86_64                              103/176 
  Verifying  : audit-libs-2.8.5-4.el7.x86_64                            104/176 
  Verifying  : libxml2-2.9.1-6.el7.5.x86_64                             105/176 
  Verifying  : glibc-2.17-317.el7.x86_64                                106/176 
  Verifying  : centos-release-7-9.2009.0.el7.centos.x86_64              107/176 
  Verifying  : libfastjson-0.99.4-3.el7.x86_64                          108/176 
  Verifying  : systemd-libs-219-78.el7.x86_64                           109/176 
  Verifying  : glibc-common-2.17-317.el7.x86_64                         110/176 
  Verifying  : kmod-20-28.el7.x86_64                                    111/176 
  Verifying  : grep-2.20-3.el7.x86_64                                   112/176 
  Verifying  : openldap-2.4.44-22.el7.x86_64                            113/176 
  Verifying  : hostname-3.13-3.el7_7.1.x86_64                           114/176 
  Verifying  : filesystem-3.2-25.el7.x86_64                             115/176 
  Verifying  : libdb-5.3.21-25.el7.x86_64                               116/176 
  Verifying  : 7:device-mapper-libs-1.02.170-6.el7.x86_64               117/176 
  Verifying  : dracut-network-033-572.el7.x86_64                        118/176 
  Verifying  : libevent-2.0.21-4.el7.x86_64                             119/176 
  Verifying  : libsemanage-2.5-14.el7.x86_64                            120/176 
  Verifying  : gdbm-1.10-8.el7.x86_64                                   121/176 
  Verifying  : libestr-0.1.9-2.el7.x86_64                               122/176 
  Verifying  : util-linux-2.23.2-65.el7.x86_64                          123/176 
  Verifying  : coreutils-8.22-24.el7.x86_64                             124/176 
  Verifying  : linux-firmware-20200421-79.git78c0348.el7.noarch         125/176 
  Verifying  : diffutils-3.3-5.el7.x86_64                               126/176 
  Verifying  : xz-libs-5.2.2-1.el7.x86_64                               127/176 
  Verifying  : python-2.7.5-89.el7.x86_64                               128/176 
  Verifying  : bash-4.2.46-34.el7.x86_64                                129/176 
  Verifying  : 1:quota-4.01-19.el7.x86_64                               130/176 
  Verifying  : libstdc++-4.8.5-44.el7.x86_64                            131/176 
  Verifying  : logrotate-3.8.6-19.el7.x86_64                            132/176 
  Verifying  : tcp_wrappers-7.6-77.el7.x86_64                           133/176 
  Verifying  : ncurses-5.9-14.20130511.el7_4.x86_64                     134/176 
  Verifying  : wget-1.14-18.el7_6.1.x86_64                              135/176 
  Verifying  : ncurses-base-5.9-14.20130511.el7_4.noarch                136/176 
  Verifying  : elfutils-default-yama-scope-0.176-5.el7.noarch           137/176 
  Verifying  : libtirpc-0.2.4-0.16.el7.x86_64                           138/176 
  Verifying  : lz4-1.8.3-1.el7.x86_64                                   139/176 
  Verifying  : 2:ethtool-4.8-10.el7.x86_64                              140/176 
  Verifying  : 2:tar-1.26-35.el7.x86_64                                 141/176 
  Verifying  : libnetfilter_conntrack-1.0.6-1.el7_3.x86_64              142/176 
  Verifying  : krb5-libs-1.15.1-50.el7.x86_64                           143/176 
  Verifying  : keyutils-libs-1.5.8-3.el7.x86_64                         144/176 
  Verifying  : 1:hardlink-1.0-19.el7.x86_64                             145/176 
  Verifying  : openssh-7.4p1-21.el7.x86_64                              146/176 
  Verifying  : libattr-2.4.46-13.el7.x86_64                             147/176 
  Verifying  : kpartx-0.4.9-133.el7.x86_64                              148/176 
  Verifying  : 1:dbus-1.10.24-15.el7.x86_64                             149/176 
  Verifying  : libcom_err-1.42.9-19.el7.x86_64                          150/176 
  Verifying  : net-tools-2.0-0.25.20131004git.el7.x86_64                151/176 
  Verifying  : shared-mime-info-1.8-5.el7.x86_64                        152/176 
  Verifying  : iproute-4.11.0-30.el7.x86_64                             153/176 
  Verifying  : fipscheck-1.4.1-6.el7.x86_64                             154/176 
  Verifying  : json-c-0.11-4.el7_0.x86_64                               155/176 
  Verifying  : libsmartcols-2.23.2-65.el7.x86_64                        156/176 
  Verifying  : xz-5.2.2-1.el7.x86_64                                    157/176 
  Verifying  : 12:dhcp-common-4.2.5-82.el7.centos.x86_64                158/176 
  Verifying  : libcap-ng-0.7.5-4.el7.x86_64                             159/176 
  Verifying  : 1:gmp-6.0.0-15.el7.x86_64                                160/176 
  Verifying  : libcollection-0.7.0-32.el7.x86_64                        161/176 
  Verifying  : p11-kit-trust-0.23.5-3.el7.x86_64                        162/176 
  Verifying  : nss-softokn-freebl-3.44.0-8.el7_7.x86_64                 163/176 
  Verifying  : sed-4.2.2-7.el7.x86_64                                   164/176 
  Verifying  : libgcrypt-1.5.3-14.el7.x86_64                            165/176 
  Verifying  : libss-1.42.9-19.el7.x86_64                               166/176 
  Verifying  : cpio-2.11-28.el7.x86_64                                  167/176 
  Verifying  : 3:irqbalance-1.0.7-12.el7.x86_64                         168/176 
  Verifying  : systemd-sysv-219-78.el7.x86_64                           169/176 
  Verifying  : numactl-libs-2.0.12-5.el7.x86_64                         170/176 
  Verifying  : libpwquality-1.2.3-5.el7.x86_64                          171/176 
  Verifying  : nss-util-3.44.0-4.el7_7.x86_64                           172/176 
  Verifying  : cyrus-sasl-lib-2.1.26-23.el7.x86_64                      173/176 
  Verifying  : elfutils-libelf-0.176-5.el7.x86_64                       174/176 
  Verifying  : libmount-2.23.2-65.el7.x86_64                            175/176 
  Verifying  : libffi-3.0.13-19.el7.x86_64                              176/176 
Installed:
  bash.x86_64 0:4.2.46-34.el7                                                   
  bc.x86_64 0:1.06.95-13.el7                                                    
  dhclient.x86_64 12:4.2.5-82.el7.centos                                        
  dracut-network.x86_64 0:033-572.el7                                           
  e2fsprogs.x86_64 0:1.42.9-19.el7                                              
  ethtool.x86_64 2:4.8-10.el7                                                   
  gzip.x86_64 0:1.5-10.el7                                                      
  iputils.x86_64 0:20160308-10.el7                                              
  irqbalance.x86_64 3:1.0.7-12.el7                                              
  kernel.x86_64 0:3.10.0-1160.el7                                               
  net-tools.x86_64 0:2.0-0.25.20131004git.el7                                   
  nfs-utils.x86_64 1:1.3.0-0.68.el7                                             
  ntp.x86_64 0:4.2.6p5-29.el7.centos.2                                          
  openssh-clients.x86_64 0:7.4p1-21.el7                                         
  openssh-server.x86_64 0:7.4p1-21.el7                                          
  openssl.x86_64 1:1.0.2k-19.el7                                                
  parted.x86_64 0:3.1-32.el7                                                    
  procps-ng.x86_64 0:3.3.10-28.el7                                              
  rpm.x86_64 0:4.11.3-45.el7                                                    
  rsync.x86_64 0:3.1.2-10.el7                                                   
  rsyslog.x86_64 0:8.24.0-55.el7                                                
  tar.x86_64 2:1.26-35.el7                                                      
  vim-minimal.x86_64 2:7.4.629-7.el7                                            
  wget.x86_64 0:1.14-18.el7_6.1                                                 
  xz.x86_64 0:5.2.2-1.el7                                                       
Dependency Installed:
  acl.x86_64 0:2.2.51-15.el7                                                    
  audit-libs.x86_64 0:2.8.5-4.el7                                               
  autogen-libopts.x86_64 0:5.18-5.el7                                           
  basesystem.noarch 0:10.0-7.el7.centos                                         
  bind-export-libs.x86_64 32:9.11.4-26.P2.el7                                   
  binutils.x86_64 0:2.27-44.base.el7                                            
  bzip2-libs.x86_64 0:1.0.6-13.el7                                              
  ca-certificates.noarch 0:2020.2.41-70.0.el7_8                                 
  centos-release.x86_64 0:7-9.2009.0.el7.centos                                 
  chkconfig.x86_64 0:1.7.6-1.el7                                                
  coreutils.x86_64 0:8.22-24.el7                                                
  cpio.x86_64 0:2.11-28.el7                                                     
  cracklib.x86_64 0:2.9.0-11.el7                                                
  cracklib-dicts.x86_64 0:2.9.0-11.el7                                          
  cryptsetup-libs.x86_64 0:2.0.3-6.el7                                          
  curl.x86_64 0:7.29.0-59.el7                                                   
  cyrus-sasl-lib.x86_64 0:2.1.26-23.el7                                         
  dbus.x86_64 1:1.10.24-15.el7                                                  
  dbus-libs.x86_64 1:1.10.24-15.el7                                             
  device-mapper.x86_64 7:1.02.170-6.el7                                         
  device-mapper-libs.x86_64 7:1.02.170-6.el7                                    
  dhcp-common.x86_64 12:4.2.5-82.el7.centos                                     
  dhcp-libs.x86_64 12:4.2.5-82.el7.centos                                       
  diffutils.x86_64 0:3.3-5.el7                                                  
  dracut.x86_64 0:033-572.el7                                                   
  e2fsprogs-libs.x86_64 0:1.42.9-19.el7                                         
  elfutils-default-yama-scope.noarch 0:0.176-5.el7                              
  elfutils-libelf.x86_64 0:0.176-5.el7                                          
  elfutils-libs.x86_64 0:0.176-5.el7                                            
  expat.x86_64 0:2.1.0-12.el7                                                   
  filesystem.x86_64 0:3.2-25.el7                                                
  findutils.x86_64 1:4.5.11-6.el7                                               
  fipscheck.x86_64 0:1.4.1-6.el7                                                
  fipscheck-lib.x86_64 0:1.4.1-6.el7                                            
  gawk.x86_64 0:4.0.2-4.el7_3.1                                                 
  gdbm.x86_64 0:1.10-8.el7                                                      
  glib2.x86_64 0:2.56.1-7.el7                                                   
  glibc.x86_64 0:2.17-317.el7                                                   
  glibc-common.x86_64 0:2.17-317.el7                                            
  gmp.x86_64 1:6.0.0-15.el7                                                     
  grep.x86_64 0:2.20-3.el7                                                      
  grubby.x86_64 0:8.28-26.el7                                                   
  gssproxy.x86_64 0:0.7.0-29.el7                                                
  hardlink.x86_64 1:1.0-19.el7                                                  
  hostname.x86_64 0:3.13-3.el7_7.1                                              
  info.x86_64 0:5.1-5.el7                                                       
  initscripts.x86_64 0:9.49.53-1.el7                                            
  iproute.x86_64 0:4.11.0-30.el7                                                
  iptables.x86_64 0:1.4.21-35.el7                                               
  json-c.x86_64 0:0.11-4.el7_0                                                  
  keyutils.x86_64 0:1.5.8-3.el7                                                 
  keyutils-libs.x86_64 0:1.5.8-3.el7                                            
  kmod.x86_64 0:20-28.el7                                                       
  kmod-libs.x86_64 0:20-28.el7                                                  
  kpartx.x86_64 0:0.4.9-133.el7                                                 
  krb5-libs.x86_64 0:1.15.1-50.el7                                              
  libacl.x86_64 0:2.2.51-15.el7                                                 
  libattr.x86_64 0:2.4.46-13.el7                                                
  libbasicobjects.x86_64 0:0.1.1-32.el7                                         
  libblkid.x86_64 0:2.23.2-65.el7                                               
  libcap.x86_64 0:2.22-11.el7                                                   
  libcap-ng.x86_64 0:0.7.5-4.el7                                                
  libcollection.x86_64 0:0.7.0-32.el7                                           
  libcom_err.x86_64 0:1.42.9-19.el7                                             
  libcurl.x86_64 0:7.29.0-59.el7                                                
  libdb.x86_64 0:5.3.21-25.el7                                                  
  libdb-utils.x86_64 0:5.3.21-25.el7                                            
  libedit.x86_64 0:3.0-12.20121213cvs.el7                                       
  libestr.x86_64 0:0.1.9-2.el7                                                  
  libevent.x86_64 0:2.0.21-4.el7                                                
  libfastjson.x86_64 0:0.99.4-3.el7                                             
  libffi.x86_64 0:3.0.13-19.el7                                                 
  libgcc.x86_64 0:4.8.5-44.el7                                                  
  libgcrypt.x86_64 0:1.5.3-14.el7                                               
  libgpg-error.x86_64 0:1.12-3.el7                                              
  libidn.x86_64 0:1.28-4.el7                                                    
  libini_config.x86_64 0:1.3.1-32.el7                                           
  libmnl.x86_64 0:1.0.3-7.el7                                                   
  libmount.x86_64 0:2.23.2-65.el7                                               
  libnetfilter_conntrack.x86_64 0:1.0.6-1.el7_3                                 
  libnfnetlink.x86_64 0:1.0.1-4.el7                                             
  libnfsidmap.x86_64 0:0.25-19.el7                                              
  libpath_utils.x86_64 0:0.2.1-32.el7                                           
  libpwquality.x86_64 0:1.2.3-5.el7                                             
  libref_array.x86_64 0:0.1.5-32.el7                                            
  libselinux.x86_64 0:2.5-15.el7                                                
  libsemanage.x86_64 0:2.5-14.el7                                               
  libsepol.x86_64 0:2.5-10.el7                                                  
  libsmartcols.x86_64 0:2.23.2-65.el7                                           
  libss.x86_64 0:1.42.9-19.el7                                                  
  libssh2.x86_64 0:1.8.0-4.el7                                                  
  libstdc++.x86_64 0:4.8.5-44.el7                                               
  libtasn1.x86_64 0:4.10-1.el7                                                  
  libtirpc.x86_64 0:0.2.4-0.16.el7                                              
  libuser.x86_64 0:0.60-9.el7                                                   
  libutempter.x86_64 0:1.1.6-4.el7                                              
  libuuid.x86_64 0:2.23.2-65.el7                                                
  libverto.x86_64 0:0.2.5-4.el7                                                 
  libverto-libevent.x86_64 0:0.2.5-4.el7                                        
  libxml2.x86_64 0:2.9.1-6.el7.5                                                
  linux-firmware.noarch 0:20200421-79.git78c0348.el7                            
  logrotate.x86_64 0:3.8.6-19.el7                                               
  lua.x86_64 0:5.1.4-15.el7                                                     
  lz4.x86_64 0:1.8.3-1.el7                                                      
  make.x86_64 1:3.82-24.el7                                                     
  ncurses.x86_64 0:5.9-14.20130511.el7_4                                        
  ncurses-base.noarch 0:5.9-14.20130511.el7_4                                   
  ncurses-libs.x86_64 0:5.9-14.20130511.el7_4                                   
  nspr.x86_64 0:4.21.0-1.el7                                                    
  nss.x86_64 0:3.44.0-7.el7_7                                                   
  nss-pem.x86_64 0:1.0.3-7.el7                                                  
  nss-softokn.x86_64 0:3.44.0-8.el7_7                                           
  nss-softokn-freebl.x86_64 0:3.44.0-8.el7_7                                    
  nss-sysinit.x86_64 0:3.44.0-7.el7_7                                           
  nss-tools.x86_64 0:3.44.0-7.el7_7                                             
  nss-util.x86_64 0:3.44.0-4.el7_7                                              
  ntpdate.x86_64 0:4.2.6p5-29.el7.centos.2                                      
  numactl-libs.x86_64 0:2.0.12-5.el7                                            
  openldap.x86_64 0:2.4.44-22.el7                                               
  openssh.x86_64 0:7.4p1-21.el7                                                 
  openssl-libs.x86_64 1:1.0.2k-19.el7                                           
  p11-kit.x86_64 0:0.23.5-3.el7                                                 
  p11-kit-trust.x86_64 0:0.23.5-3.el7                                           
  pam.x86_64 0:1.1.8-23.el7                                                     
  pcre.x86_64 0:8.32-17.el7                                                     
  pkgconfig.x86_64 1:0.27.1-4.el7                                               
  popt.x86_64 0:1.13-16.el7                                                     
  python.x86_64 0:2.7.5-89.el7                                                  
  python-libs.x86_64 0:2.7.5-89.el7                                             
  qrencode-libs.x86_64 0:3.4.1-3.el7                                            
  quota.x86_64 1:4.01-19.el7                                                    
  quota-nls.noarch 1:4.01-19.el7                                                
  readline.x86_64 0:6.2-11.el7                                                  
  rpcbind.x86_64 0:0.2.0-49.el7                                                 
  rpm-libs.x86_64 0:4.11.3-45.el7                                               
  sed.x86_64 0:4.2.2-7.el7                                                      
  setup.noarch 0:2.8.71-11.el7                                                  
  shadow-utils.x86_64 2:4.6-5.el7                                               
  shared-mime-info.x86_64 0:1.8-5.el7                                           
  sqlite.x86_64 0:3.7.17-8.el7_7.1                                              
  systemd.x86_64 0:219-78.el7                                                   
  systemd-libs.x86_64 0:219-78.el7                                              
  systemd-sysv.x86_64 0:219-78.el7                                              
  sysvinit-tools.x86_64 0:2.88-14.dsf.el7                                       
  tcp_wrappers.x86_64 0:7.6-77.el7                                              
  tcp_wrappers-libs.x86_64 0:7.6-77.el7                                         
  tzdata.noarch 0:2020a-1.el7                                                   
  ustr.x86_64 0:1.0.4-16.el7                                                    
  util-linux.x86_64 0:2.23.2-65.el7                                             
  xz-libs.x86_64 0:5.2.2-1.el7                                                  
  zlib.x86_64 0:1.2.7-18.el7                                                    
Complete!
Enter the dracut mode. Dracut version: 033. Dracut directory: dracut_033.
Try to load drivers: tg3 bnx2 bnx2x e1000 e1000e igb mlx4_en virtio_net be2net ext3 ext4 to initrd.
chroot /install/netboot/centos7.9/x86_64/compute/rootimg dracut  -f /tmp/initrd.14413.gz 3.10.0-1160.el7.x86_64
No '/dev/log' or 'logger' included for syslog logging
Turning off host-only mode: '/sys' is not mounted!
Turning off host-only mode: '/proc' is not mounted!
Turning off host-only mode: '/run' is not mounted!
Turning off host-only mode: '/dev' is not mounted!
dracut-install: ERROR: installing 'mkfs.xfs'
dracut-install: ERROR: installing 'xfs_db'
/usr/lib/dracut/dracut-install -D /var/tmp/dracut.tA0JDb/initramfs -a parted mke2fs bc mkswap swapon chmod mkfs mkfs.ext4 mkfs.xfs xfs_db
grep: /etc/udev/rules.d/*: No such file or directory
the initial ramdisk for stateless is generated successfully.
Try to load drivers: tg3 bnx2 bnx2x e1000 e1000e igb mlx4_en virtio_net be2net ext3 ext4 to initrd.
chroot /install/netboot/centos7.9/x86_64/compute/rootimg dracut  -f /tmp/initrd.14413.gz 3.10.0-1160.el7.x86_64
No '/dev/log' or 'logger' included for syslog logging
Turning off host-only mode: '/sys' is not mounted!
Turning off host-only mode: '/proc' is not mounted!
Turning off host-only mode: '/run' is not mounted!
Turning off host-only mode: '/dev' is not mounted!
dracut-install: ERROR: installing 'mkfs.xfs'
dracut-install: ERROR: installing 'xfs_db'
/usr/lib/dracut/dracut-install -D /var/tmp/dracut.79Klu6/initramfs -a parted mke2fs bc mkswap swapon chmod mkfs mkfs.ext4 mkfs.xfs xfs_db
grep: /etc/udev/rules.d/*: No such file or directory
the initial ramdisk for statelite is generated successfully.
[root@master ~]# cd /install/netboot/centos7.9/x86_64/compute/
[root@master compute]# mkdir -p /install/custom/netboot
[root@master compute]#  chdef -t osimage centos7.9-x86_64-netboot-compute synclists="/install/custom/netboot/compute.synclist"
1 object definitions have been created or modified.
[root@master compute]# lsdef -t osimage centos7.9-x86_64-netboot-compute
Object name: centos7.9-x86_64-netboot-compute
    exlist=/opt/xcat/share/xcat/netboot/centos/compute.centos7.exlist
    imagetype=linux
    osarch=x86_64
    osdistroname=centos7.9-x86_64
    osname=Linux
    osvers=centos7.9
    otherpkgdir=/install/post/otherpkgs/centos7.9/x86_64
    permission=755
    pkgdir=/install/centos7.9/x86_64
    pkglist=/opt/xcat/share/xcat/netboot/centos/compute.centos7.pkglist
    postinstall=/opt/xcat/share/xcat/netboot/centos/compute.centos7.postinstall
    profile=compute
    provmethod=netboot
    rootimgdir=/install/netboot/centos7.9/x86_64/compute
    synclists=/install/custom/netboot/compute.synclist
[root@master compute]# vim /install/custom/netboot/compute.synclist
[root@master compute]# cat /install/custom/netboot/compute.synclist
cat: /install/custom/netboot/compute.synclist: No such file or directory
[root@master compute]# lsdef -t osimage
centos7.9-x86_64-install-compute  (osimage)
centos7.9-x86_64-netboot-compute  (osimage)
centos7.9-x86_64-statelite-compute  (osimage)
[root@master compute]# packimage centos7.9-x86_64-netboot-compute
Packing contents of /install/netboot/centos7.9/x86_64/compute/rootimg
archive method:cpio
compress method:gzip

[root@master compute]# mkdef -t node cn00 groups=compute,all ip=10.10.10.3 mac=00:0c:29:11:A6:49 netboot=xnba
1 object definitions have been created or modified.
[root@master compute]# lsdef cn00
Object name: cn00
    groups=compute,all
    ip=10.10.10.3
    mac=00:0c:29:11:A6:49
    netboot=xnba
    postbootscripts=otherpkgs
    postscripts=syslog,remoteshell,syncfiles
[root@master compute]# chdef -t site domain=cdac.in
1 object definitions have been created or modified.
[root@master compute]# tabdump site | grep domain
"domain","cdac.in",,
[root@master compute]# makehosts
[root@master compute]# vim /etc/hosts
[root@master compute]# makenetworks
Warning: [master]: The network entry '10_10_10_0-255_255_255_0' already exists in xCAT networks table. Cannot create a definition for '10_10_10_0-255_255_255_0'
Warning: [master]: The network entry '192_168_20_0-255_255_255_0' already exists in xCAT networks table. Cannot create a definition for '192_168_20_0-255_255_255_0'
Warning: [master]: The network entry '192_168_122_0-255_255_255_0' already exists in xCAT networks table. Cannot create a definition for '192_168_122_0-255_255_255_0'
[root@master compute]# makedhcp -n
Renamed existing dhcp configuration file to  /etc/dhcp/dhcpd.conf.xcatbak

The dhcp server must be restarted for OMAPI function to work
Warning: [master]: No dynamic range specified for 10.10.10.0. If hardware discovery is being used, a dynamic range is required.
Warning: [master]: No dynamic range specified for 192.168.20.0. If hardware discovery is being used, a dynamic range is required.
Warning: [master]: No dynamic range specified for 192.168.122.0. If hardware discovery is being used, a dynamic range is required.
[root@master compute]# cat /etc/dhcp/dhcpd.conf
#xCAT generated dhcp configuration

option conf-file code 209 = text;
option space isan;
option isan-encap-opts code 43 = encapsulate isan;
option isan.iqn code 203 = string;
option isan.root-path code 201 = string;
option space gpxe;
option gpxe-encap-opts code 175 = encapsulate gpxe;
option gpxe.bus-id code 177 = string;
option user-class-identifier code 77 = string;
option gpxe.no-pxedhcp code 176 = unsigned integer 8;
option tcode code 101 = text;
option iscsi-initiator-iqn code 203 = string;
ddns-update-style interim;
ignore client-updates;
option client-architecture code 93 = unsigned integer 16;
option tcode "America/New_York";
option gpxe.no-pxedhcp 1;
option www-server code 114 = string;
option cumulus-provision-url code 239 = text;

omapi-port 7911;
key xcat_key {
  algorithm hmac-md5;
  secret "QWlUbTRod1A0eEpWeHpGeWllaFpuMlgyenM4MmkwaUg=";
};
omapi-key xcat_key;
class "pxe" {
   match if substring (option vendor-class-identifier, 0, 9) = "PXEClient";
   ddns-updates off;
    max-lease-time 600;
}
shared-network ens37 {
  subnet 10.10.10.0 netmask 255.255.255.0 {
    authoritative;
    max-lease-time 43200;
    min-lease-time 43200;
    default-lease-time 43200;
    option routers  10.10.10.129;
    next-server  10.10.10.129;
    option log-servers 10.10.10.129;
    option ntp-servers 10.10.10.129;
    option domain-name "cdac.in";
    option domain-name-servers  10.10.10.2;
    option interface-mtu 1500;
    option domain-search  "cdac.in";
    option cumulus-provision-url "http://10.10.10.129:80/install/postscripts/cumulusztp";
    zone cdac.in. {
       primary 10.10.10.2; key xcat_key; 
    }
    zone 10.10.10.IN-ADDR.ARPA. {
       primary 10.10.10.2; key xcat_key; 
    }
    if option user-class-identifier = "xNBA" and option client-architecture = 00:00 { #x86, xCAT Network Boot Agent
        always-broadcast on;
        filename = "http://10.10.10.129:80/tftpboot/xcat/xnba/nets/10.10.10.0_24";
    } else if option user-class-identifier = "xNBA" and option client-architecture = 00:09 { #x86, xCAT Network Boot Agent
        filename = "http://10.10.10.129:80/tftpboot/xcat/xnba/nets/10.10.10.0_24.uefi";
    } else if option client-architecture = 00:00  { #x86
        filename "xcat/xnba.kpxe";
    } else if option vendor-class-identifier = "Etherboot-5.4"  { #x86
        filename "xcat/xnba.kpxe";
    } else if option client-architecture = 00:07 { #x86_64 uefi
         filename "xcat/xnba.efi";
    } else if option client-architecture = 00:09 { #x86_64 uefi alternative id
         filename "xcat/xnba.efi";
    } else if option client-architecture = 00:02 { #ia64
         filename "elilo.efi";
    } else if option client-architecture = 00:0e { #OPAL-v3
         option conf-file = "http://10.10.10.129:80/tftpboot/pxelinux.cfg/p/10.10.10.0_24";
    } else if substring (option vendor-class-identifier,0,11) = "onie_vendor" { #for onie on cumulus switch
        option www-server = "http://10.10.10.129:80/install/onie/onie-installer";
    } else if substring(filename,0,1) = null { #otherwise, provide yaboot if the client isn't specific
         filename "/yaboot";
    }
  } # 10.10.10.0/255.255.255.0 subnet_end
} # ens37 nic_end
shared-network ens33 {
  subnet 192.168.20.0 netmask 255.255.255.0 {
    authoritative;
    max-lease-time 43200;
    min-lease-time 43200;
    default-lease-time 43200;
    option routers  192.168.20.2;
    next-server  192.168.20.131;
    option log-servers 192.168.20.131;
    option ntp-servers 192.168.20.131;
    option domain-name "cdac.in";
    option domain-name-servers  10.10.10.2;
    option interface-mtu 1500;
    option domain-search  "cdac.in";
    option cumulus-provision-url "http://192.168.20.131:80/install/postscripts/cumulusztp";
    zone cdac.in. {
       primary 10.10.10.2; key xcat_key; 
    }
    zone 20.168.192.IN-ADDR.ARPA. {
       primary 10.10.10.2; key xcat_key; 
    }
    if option user-class-identifier = "xNBA" and option client-architecture = 00:00 { #x86, xCAT Network Boot Agent
        always-broadcast on;
        filename = "http://192.168.20.131:80/tftpboot/xcat/xnba/nets/192.168.20.0_24";
    } else if option user-class-identifier = "xNBA" and option client-architecture = 00:09 { #x86, xCAT Network Boot Agent
        filename = "http://192.168.20.131:80/tftpboot/xcat/xnba/nets/192.168.20.0_24.uefi";
    } else if option client-architecture = 00:00  { #x86
        filename "xcat/xnba.kpxe";
    } else if option vendor-class-identifier = "Etherboot-5.4"  { #x86
        filename "xcat/xnba.kpxe";
    } else if option client-architecture = 00:07 { #x86_64 uefi
         filename "xcat/xnba.efi";
    } else if option client-architecture = 00:09 { #x86_64 uefi alternative id
         filename "xcat/xnba.efi";
    } else if option client-architecture = 00:02 { #ia64
         filename "elilo.efi";
    } else if option client-architecture = 00:0e { #OPAL-v3
         option conf-file = "http://192.168.20.131:80/tftpboot/pxelinux.cfg/p/192.168.20.0_24";
    } else if substring (option vendor-class-identifier,0,11) = "onie_vendor" { #for onie on cumulus switch
        option www-server = "http://192.168.20.131:80/install/onie/onie-installer";
    } else if substring(filename,0,1) = null { #otherwise, provide yaboot if the client isn't specific
         filename "/yaboot";
    }
  } # 192.168.20.0/255.255.255.0 subnet_end
} # ens33 nic_end
shared-network virbr0 {
  subnet 192.168.122.0 netmask 255.255.255.0 {
    authoritative;
    max-lease-time 43200;
    min-lease-time 43200;
    default-lease-time 43200;
    option routers  192.168.122.1;
    next-server  192.168.122.1;
    option log-servers 192.168.122.1;
    option ntp-servers 192.168.122.1;
    option domain-name "cdac.in";
    option domain-name-servers  10.10.10.2;
    option interface-mtu 1500;
    option domain-search  "cdac.in";
    option cumulus-provision-url "http://192.168.122.1:80/install/postscripts/cumulusztp";
    zone cdac.in. {
       primary 10.10.10.2; key xcat_key; 
    }
    zone 122.168.192.IN-ADDR.ARPA. {
       primary 10.10.10.2; key xcat_key; 
    }
    if option user-class-identifier = "xNBA" and option client-architecture = 00:00 { #x86, xCAT Network Boot Agent
        always-broadcast on;
        filename = "http://192.168.122.1:80/tftpboot/xcat/xnba/nets/192.168.122.0_24";
    } else if option user-class-identifier = "xNBA" and option client-architecture = 00:09 { #x86, xCAT Network Boot Agent
        filename = "http://192.168.122.1:80/tftpboot/xcat/xnba/nets/192.168.122.0_24.uefi";
    } else if option client-architecture = 00:00  { #x86
        filename "xcat/xnba.kpxe";
    } else if option vendor-class-identifier = "Etherboot-5.4"  { #x86
        filename "xcat/xnba.kpxe";
    } else if option client-architecture = 00:07 { #x86_64 uefi
         filename "xcat/xnba.efi";
    } else if option client-architecture = 00:09 { #x86_64 uefi alternative id
         filename "xcat/xnba.efi";
    } else if option client-architecture = 00:02 { #ia64
         filename "elilo.efi";
    } else if option client-architecture = 00:0e { #OPAL-v3
         option conf-file = "http://192.168.122.1:80/tftpboot/pxelinux.cfg/p/192.168.122.0_24";
    } else if substring (option vendor-class-identifier,0,11) = "onie_vendor" { #for onie on cumulus switch
        option www-server = "http://192.168.122.1:80/install/onie/onie-installer";
    } else if substring(filename,0,1) = null { #otherwise, provide yaboot if the client isn't specific
         filename "/yaboot";
    }
  } # 192.168.122.0/255.255.255.0 subnet_end
} # virbr0 nic_end
[root@master compute]# makedns -n
Warning: SELINUX is not disabled. The makedns command will not be able to generate a complete DNS setup. Disable SELINUX and run the command again.
Handling master in /etc/hosts.
Handling localhost in /etc/hosts.
Handling localhost in /etc/hosts.
Handling cn00 in /etc/hosts.
Getting reverse zones, this may take several minutes for a large cluster.
Completed getting reverse zones.
Updating zones.
Completed updating zones.
Restarting named
Restarting named complete
Updating DNS records, this may take several minutes for a large cluster.
Error: [master]: No reply received when sending DNS update to zone 10.10.10.IN-ADDR.ARPA.
Error: [master]: No reply received when sending DNS update to zone cdac.in.
Completed updating DNS records.
DNS setup is completed
[root@master compute]# nodeset compute osimage=centos7.9-x86_64-netboot-compute
cn00: netboot centos7.9-x86_64-compute
[root@master compute]# vim /etc/hosts
[root@master compute]# tabdumb
bash: tabdumb: command not found...
[root@master compute]# tabdump
auditlog
bootparams
boottarget
cfgmgt
chain
deps
discoverydata
domain
eventlog
firmware
hosts
hwinv
hypervisor
ipmi
iscsi
kit
kitcomponent
kitrepo
kvm_masterdata
kvm_nodedata
linuximage
litefile
litetree
mac
mic
monitoring
monsetting
mp
mpa
networks
nics
nimimage
nodegroup
nodehm
nodelist
nodepos
noderes
nodetype
notification
openbmc
osdistro
osdistroupdate
osimage
passwd
pdu
pduoutlet
performance
policy
postscripts
ppc
ppcdirect
ppchcp
prescripts
prodkey
rack
routes
servicenode
site
statelite
storage
switch
switches
taskstate
token
virtsd
vm
vmmaster
vpd
websrv
winimage
zone
zvm
zvmivp
[root@master compute]# tabdump-site
bash: tabdump-site: command not found...
[root@master compute]# tabdump site
#key,value,comments,disable
"blademaxp","64",,
"fsptimeout","0",,
"installdir","/install",,
"ipmimaxp","64",,
"ipmiretries","3",,
"ipmitimeout","2",,
"consoleondemand","no",,
"master","10.10.10.2",,
"forwarders","192.168.20.2,10.10.10.1",,
"nameservers","10.10.10.2",,
"maxssh","8",,
"ppcmaxp","64",,
"ppcretry","3",,
"ppctimeout","0",,
"powerinterval","0",,
"syspowerinterval","0",,
"sharedtftp","1",,
"SNsyncfiledir","/var/xcat/syncfiles",,
"nodesyncfiledir","/var/xcat/node/syncfiles",,
"tftpdir","/tftpboot",,
"xcatdport","3001",,
"xcatiport","3002",,
"xcatconfdir","/etc/xcat",,
"timezone","America/New_York",,
"useNmapfromMN","no",,
"enableASMI","no",,
"db2installloc","/mntdb2",,
"databaseloc","/var/lib",,
"sshbetweennodes","ALLGROUPS",,
"dnshandler","ddns",,
"vsftp","n",,
"cleanupxcatpost","no",,
"cleanupdiskfullxcatpost","no",,
"dhcplease","43200",,
"auditnosyslog","0",,
"auditskipcmds","ALL",,
"domain","cdac.in",,
[root@master compute]# sysstemctl status network
bash: sysstemctl: command not found...
Similar command is: 'systemctl'
[root@master compute]# systemctl status network
● network.service - LSB: Bring up/down networking
   Loaded: loaded (/etc/rc.d/init.d/network; bad; vendor preset: disabled)
   Active: active (exited) since Sat 2023-06-03 11:19:03 EDT; 1 day 13h ago
     Docs: man:systemd-sysv-generator(8)
    Tasks: 0

Jun 03 11:19:02 localhost.localdomain systemd[1]: Starting LSB: Bring up/down networking...
Jun 03 11:19:03 localhost.localdomain network[1214]: Bringing up loopback interface:  [  OK  ]
Jun 03 11:19:03 localhost.localdomain network[1214]: Bringing up interface ens33:  [  OK  ]
Jun 03 11:19:03 localhost.localdomain systemd[1]: Started LSB: Bring up/down networking.
[root@master compute]# ifup ens37
/sbin/ifup: configuration for ens37 not found.
Usage: ifup <configuration>
[root@master compute]# ifup ens36
/sbin/ifup: configuration for ens36 not found.
Usage: ifup <configuration>
[root@master compute]# ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host 
       valid_lft forever preferred_lft forever
2: ens33: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    link/ether 00:0c:29:0a:aa:0c brd ff:ff:ff:ff:ff:ff
    inet 192.168.20.131/24 brd 192.168.20.255 scope global noprefixroute dynamic ens33
       valid_lft 1616sec preferred_lft 1616sec
    inet6 fe80::26df:cf88:8edd:bae8/64 scope link noprefixroute 
       valid_lft forever preferred_lft forever
3: virbr0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc noqueue state DOWN group default qlen 1000
    link/ether 52:54:00:3a:69:b1 brd ff:ff:ff:ff:ff:ff
4: virbr0-nic: <BROADCAST,MULTICAST> mtu 1500 qdisc pfifo_fast master virbr0 state DOWN group default qlen 1000
    link/ether 52:54:00:3a:69:b1 brd ff:ff:ff:ff:ff:ff
5: ens37: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    link/ether 00:0c:29:0a:aa:16 brd ff:ff:ff:ff:ff:ff
    inet 10.10.10.129/24 brd 10.10.10.255 scope global noprefixroute dynamic ens37
       valid_lft 1621sec preferred_lft 1621sec
    inet6 fe80::ef07:57b8:d00d:e812/64 scope link noprefixroute 
       valid_lft forever preferred_lft forever
[root@master compute]# makehosts
[root@master compute]# makenetworks
Warning: [master]: The network entry '10_10_10_0-255_255_255_0' already exists in xCAT networks table. Cannot create a definition for '10_10_10_0-255_255_255_0'
Warning: [master]: The network entry '192_168_20_0-255_255_255_0' already exists in xCAT networks table. Cannot create a definition for '192_168_20_0-255_255_255_0'
[root@master compute]# makedns-n
bash: makedns-n: command not found...
[root@master compute]# makedns -n
Warning: SELINUX is not disabled. The makedns command will not be able to generate a complete DNS setup. Disable SELINUX and run the command again.
Handling master in /etc/hosts.
Handling localhost in /etc/hosts.
Handling localhost in /etc/hosts.
Handling cn00 in /etc/hosts.
Getting reverse zones, this may take several minutes for a large cluster.
Completed getting reverse zones.
Updating zones.
Completed updating zones.
Restarting named
Restarting named complete
Updating DNS records, this may take several minutes for a large cluster.
Error: [master]: No reply received when sending DNS update to zone 10.10.10.IN-ADDR.ARPA.
Error: [master]: No reply received when sending DNS update to zone cdac.in.
Completed updating DNS records.
DNS setup is completed
[root@master compute]# chdef -t site dhcpinterfaces=ens37
1 object definitions have been created or modified.
[root@master compute]# tabdump site
#key,value,comments,disable
"blademaxp","64",,
"fsptimeout","0",,
"installdir","/install",,
"ipmimaxp","64",,
"ipmiretries","3",,
"ipmitimeout","2",,
"consoleondemand","no",,
"master","10.10.10.2",,
"forwarders","192.168.20.2,10.10.10.1",,
"nameservers","10.10.10.2",,
"maxssh","8",,
"ppcmaxp","64",,
"ppcretry","3",,
"ppctimeout","0",,
"powerinterval","0",,
"syspowerinterval","0",,
"sharedtftp","1",,
"SNsyncfiledir","/var/xcat/syncfiles",,
"nodesyncfiledir","/var/xcat/node/syncfiles",,
"tftpdir","/tftpboot",,
"xcatdport","3001",,
"xcatiport","3002",,
"xcatconfdir","/etc/xcat",,
"timezone","America/New_York",,
"useNmapfromMN","no",,
"enableASMI","no",,
"db2installloc","/mntdb2",,
"databaseloc","/var/lib",,
"sshbetweennodes","ALLGROUPS",,
"dnshandler","ddns",,
"vsftp","n",,
"cleanupxcatpost","no",,
"cleanupdiskfullxcatpost","no",,
"dhcplease","43200",,
"auditnosyslog","0",,
"auditskipcmds","ALL",,
"domain","cdac.in",,
"dhcpinterfaces","ens37",,
[root@master compute]# nodeset compute osimage=centos7.9-x86_64-netboot-compute
cn00: netboot centos7.9-x86_64-compute
[root@master compute]# cat /etc/dhcp/dhcpd.conf
#xCAT generated dhcp configuration

option conf-file code 209 = text;
option space isan;
option isan-encap-opts code 43 = encapsulate isan;
option isan.iqn code 203 = string;
option isan.root-path code 201 = string;
option space gpxe;
option gpxe-encap-opts code 175 = encapsulate gpxe;
option gpxe.bus-id code 177 = string;
option user-class-identifier code 77 = string;
option gpxe.no-pxedhcp code 176 = unsigned integer 8;
option tcode code 101 = text;
option iscsi-initiator-iqn code 203 = string;
ddns-update-style interim;
ignore client-updates;
option client-architecture code 93 = unsigned integer 16;
option tcode "America/New_York";
option gpxe.no-pxedhcp 1;
option www-server code 114 = string;
option cumulus-provision-url code 239 = text;

omapi-port 7911;
key xcat_key {
  algorithm hmac-md5;
  secret "QWlUbTRod1A0eEpWeHpGeWllaFpuMlgyenM4MmkwaUg=";
};
omapi-key xcat_key;
class "pxe" {
   match if substring (option vendor-class-identifier, 0, 9) = "PXEClient";
   ddns-updates off;
    max-lease-time 600;
}
shared-network ens37 {
  subnet 10.10.10.0 netmask 255.255.255.0 {
    authoritative;
    max-lease-time 43200;
    min-lease-time 43200;
    default-lease-time 43200;
    option routers  10.10.10.129;
    next-server  10.10.10.129;
    option log-servers 10.10.10.129;
    option ntp-servers 10.10.10.129;
    option domain-name "cdac.in";
    option domain-name-servers  10.10.10.2;
    option interface-mtu 1500;
    option domain-search  "cdac.in";
    option cumulus-provision-url "http://10.10.10.129:80/install/postscripts/cumulusztp";
    zone cdac.in. {
       primary 10.10.10.2; key xcat_key; 
    }
    zone 10.10.10.IN-ADDR.ARPA. {
       primary 10.10.10.2; key xcat_key; 
    }
    if option user-class-identifier = "xNBA" and option client-architecture = 00:00 { #x86, xCAT Network Boot Agent
        always-broadcast on;
        filename = "http://10.10.10.129:80/tftpboot/xcat/xnba/nets/10.10.10.0_24";
    } else if option user-class-identifier = "xNBA" and option client-architecture = 00:09 { #x86, xCAT Network Boot Agent
        filename = "http://10.10.10.129:80/tftpboot/xcat/xnba/nets/10.10.10.0_24.uefi";
    } else if option client-architecture = 00:00  { #x86
        filename "xcat/xnba.kpxe";
    } else if option vendor-class-identifier = "Etherboot-5.4"  { #x86
        filename "xcat/xnba.kpxe";
    } else if option client-architecture = 00:07 { #x86_64 uefi
         filename "xcat/xnba.efi";
    } else if option client-architecture = 00:09 { #x86_64 uefi alternative id
         filename "xcat/xnba.efi";
    } else if option client-architecture = 00:02 { #ia64
         filename "elilo.efi";
    } else if option client-architecture = 00:0e { #OPAL-v3
         option conf-file = "http://10.10.10.129:80/tftpboot/pxelinux.cfg/p/10.10.10.0_24";
    } else if substring (option vendor-class-identifier,0,11) = "onie_vendor" { #for onie on cumulus switch
        option www-server = "http://10.10.10.129:80/install/onie/onie-installer";
    } else if substring(filename,0,1) = null { #otherwise, provide yaboot if the client isn't specific
         filename "/yaboot";
    }
  } # 10.10.10.0/255.255.255.0 subnet_end
} # ens37 nic_end
shared-network ens33 {
  subnet 192.168.20.0 netmask 255.255.255.0 {
    authoritative;
    max-lease-time 43200;
    min-lease-time 43200;
    default-lease-time 43200;
    option routers  192.168.20.2;
    next-server  192.168.20.131;
    option log-servers 192.168.20.131;
    option ntp-servers 192.168.20.131;
    option domain-name "cdac.in";
    option domain-name-servers  10.10.10.2;
    option interface-mtu 1500;
    option domain-search  "cdac.in";
    option cumulus-provision-url "http://192.168.20.131:80/install/postscripts/cumulusztp";
    zone cdac.in. {
       primary 10.10.10.2; key xcat_key; 
    }
    zone 20.168.192.IN-ADDR.ARPA. {
       primary 10.10.10.2; key xcat_key; 
    }
    if option user-class-identifier = "xNBA" and option client-architecture = 00:00 { #x86, xCAT Network Boot Agent
        always-broadcast on;
        filename = "http://192.168.20.131:80/tftpboot/xcat/xnba/nets/192.168.20.0_24";
    } else if option user-class-identifier = "xNBA" and option client-architecture = 00:09 { #x86, xCAT Network Boot Agent
        filename = "http://192.168.20.131:80/tftpboot/xcat/xnba/nets/192.168.20.0_24.uefi";
    } else if option client-architecture = 00:00  { #x86
        filename "xcat/xnba.kpxe";
    } else if option vendor-class-identifier = "Etherboot-5.4"  { #x86
        filename "xcat/xnba.kpxe";
    } else if option client-architecture = 00:07 { #x86_64 uefi
         filename "xcat/xnba.efi";
    } else if option client-architecture = 00:09 { #x86_64 uefi alternative id
         filename "xcat/xnba.efi";
    } else if option client-architecture = 00:02 { #ia64
         filename "elilo.efi";
    } else if option client-architecture = 00:0e { #OPAL-v3
         option conf-file = "http://192.168.20.131:80/tftpboot/pxelinux.cfg/p/192.168.20.0_24";
    } else if substring (option vendor-class-identifier,0,11) = "onie_vendor" { #for onie on cumulus switch
        option www-server = "http://192.168.20.131:80/install/onie/onie-installer";
    } else if substring(filename,0,1) = null { #otherwise, provide yaboot if the client isn't specific
         filename "/yaboot";
    }
  } # 192.168.20.0/255.255.255.0 subnet_end
} # ens33 nic_end
shared-network virbr0 {
  subnet 192.168.122.0 netmask 255.255.255.0 {
    authoritative;
    max-lease-time 43200;
    min-lease-time 43200;
    default-lease-time 43200;
    option routers  192.168.122.1;
    next-server  192.168.122.1;
    option log-servers 192.168.122.1;
    option ntp-servers 192.168.122.1;
    option domain-name "cdac.in";
    option domain-name-servers  10.10.10.2;
    option interface-mtu 1500;
    option domain-search  "cdac.in";
    option cumulus-provision-url "http://192.168.122.1:80/install/postscripts/cumulusztp";
    zone cdac.in. {
       primary 10.10.10.2; key xcat_key; 
    }
    zone 122.168.192.IN-ADDR.ARPA. {
       primary 10.10.10.2; key xcat_key; 
    }
    if option user-class-identifier = "xNBA" and option client-architecture = 00:00 { #x86, xCAT Network Boot Agent
        always-broadcast on;
        filename = "http://192.168.122.1:80/tftpboot/xcat/xnba/nets/192.168.122.0_24";
    } else if option user-class-identifier = "xNBA" and option client-architecture = 00:09 { #x86, xCAT Network Boot Agent
        filename = "http://192.168.122.1:80/tftpboot/xcat/xnba/nets/192.168.122.0_24.uefi";
    } else if option client-architecture = 00:00  { #x86
        filename "xcat/xnba.kpxe";
    } else if option vendor-class-identifier = "Etherboot-5.4"  { #x86
        filename "xcat/xnba.kpxe";
    } else if option client-architecture = 00:07 { #x86_64 uefi
         filename "xcat/xnba.efi";
    } else if option client-architecture = 00:09 { #x86_64 uefi alternative id
         filename "xcat/xnba.efi";
    } else if option client-architecture = 00:02 { #ia64
         filename "elilo.efi";
    } else if option client-architecture = 00:0e { #OPAL-v3
         option conf-file = "http://192.168.122.1:80/tftpboot/pxelinux.cfg/p/192.168.122.0_24";
    } else if substring (option vendor-class-identifier,0,11) = "onie_vendor" { #for onie on cumulus switch
        option www-server = "http://192.168.122.1:80/install/onie/onie-installer";
    } else if substring(filename,0,1) = null { #otherwise, provide yaboot if the client isn't specific
         filename "/yaboot";
    }
  } # 192.168.122.0/255.255.255.0 subnet_end
} # virbr0 nic_end
#definition for host cn00 aka host cn00 can be found in the dhcpd.leases file (typically /var/lib/dhcpd/dhcpd.leases)
[root@master compute]# lsdef cn00
Object name: cn00
    arch=x86_64
    currstate=netboot centos7.9-x86_64-compute
    groups=compute,all
    ip=10.10.10.3
    mac=00:0c:29:11:A6:49
    netboot=xnba
    os=centos7.9
    postbootscripts=otherpkgs
    postscripts=syslog,remoteshell,syncfiles
    profile=compute
    provmethod=centos7.9-x86_64-netboot-compute
[root@master compute]# makehosts
[root@master compute]# makenetworks
Warning: [master]: The network entry '10_10_10_0-255_255_255_0' already exists in xCAT networks table. Cannot create a definition for '10_10_10_0-255_255_255_0'
Warning: [master]: The network entry '192_168_20_0-255_255_255_0' already exists in xCAT networks table. Cannot create a definition for '192_168_20_0-255_255_255_0'
[root@master compute]# makedhcp -n
Renamed existing dhcp configuration file to  /etc/dhcp/dhcpd.conf.xcatbak

Warning: [master]: No dynamic range specified for 10.10.10.0. If hardware discovery is being used, a dynamic range is required.
[root@master compute]#  cat /etc/dhcp/dhcpd.conf.xcatbak
#xCAT generated dhcp configuration

option conf-file code 209 = text;
option space isan;
option isan-encap-opts code 43 = encapsulate isan;
option isan.iqn code 203 = string;
option isan.root-path code 201 = string;
option space gpxe;
option gpxe-encap-opts code 175 = encapsulate gpxe;
option gpxe.bus-id code 177 = string;
option user-class-identifier code 77 = string;
option gpxe.no-pxedhcp code 176 = unsigned integer 8;
option tcode code 101 = text;
option iscsi-initiator-iqn code 203 = string;
ddns-update-style interim;
ignore client-updates;
option client-architecture code 93 = unsigned integer 16;
option tcode "America/New_York";
option gpxe.no-pxedhcp 1;
option www-server code 114 = string;
option cumulus-provision-url code 239 = text;

omapi-port 7911;
key xcat_key {
  algorithm hmac-md5;
  secret "QWlUbTRod1A0eEpWeHpGeWllaFpuMlgyenM4MmkwaUg=";
};
omapi-key xcat_key;
class "pxe" {
   match if substring (option vendor-class-identifier, 0, 9) = "PXEClient";
   ddns-updates off;
    max-lease-time 600;
}
shared-network ens37 {
  subnet 10.10.10.0 netmask 255.255.255.0 {
    authoritative;
    max-lease-time 43200;
    min-lease-time 43200;
    default-lease-time 43200;
    option routers  10.10.10.129;
    next-server  10.10.10.129;
    option log-servers 10.10.10.129;
    option ntp-servers 10.10.10.129;
    option domain-name "cdac.in";
    option domain-name-servers  10.10.10.2;
    option interface-mtu 1500;
    option domain-search  "cdac.in";
    option cumulus-provision-url "http://10.10.10.129:80/install/postscripts/cumulusztp";
    zone cdac.in. {
       primary 10.10.10.2; key xcat_key; 
    }
    zone 10.10.10.IN-ADDR.ARPA. {
       primary 10.10.10.2; key xcat_key; 
    }
    if option user-class-identifier = "xNBA" and option client-architecture = 00:00 { #x86, xCAT Network Boot Agent
        always-broadcast on;
        filename = "http://10.10.10.129:80/tftpboot/xcat/xnba/nets/10.10.10.0_24";
    } else if option user-class-identifier = "xNBA" and option client-architecture = 00:09 { #x86, xCAT Network Boot Agent
        filename = "http://10.10.10.129:80/tftpboot/xcat/xnba/nets/10.10.10.0_24.uefi";
    } else if option client-architecture = 00:00  { #x86
        filename "xcat/xnba.kpxe";
    } else if option vendor-class-identifier = "Etherboot-5.4"  { #x86
        filename "xcat/xnba.kpxe";
    } else if option client-architecture = 00:07 { #x86_64 uefi
         filename "xcat/xnba.efi";
    } else if option client-architecture = 00:09 { #x86_64 uefi alternative id
         filename "xcat/xnba.efi";
    } else if option client-architecture = 00:02 { #ia64
         filename "elilo.efi";
    } else if option client-architecture = 00:0e { #OPAL-v3
         option conf-file = "http://10.10.10.129:80/tftpboot/pxelinux.cfg/p/10.10.10.0_24";
    } else if substring (option vendor-class-identifier,0,11) = "onie_vendor" { #for onie on cumulus switch
        option www-server = "http://10.10.10.129:80/install/onie/onie-installer";
    } else if substring(filename,0,1) = null { #otherwise, provide yaboot if the client isn't specific
         filename "/yaboot";
    }
  } # 10.10.10.0/255.255.255.0 subnet_end
} # ens37 nic_end
shared-network ens33 {
  subnet 192.168.20.0 netmask 255.255.255.0 {
    authoritative;
    max-lease-time 43200;
    min-lease-time 43200;
    default-lease-time 43200;
    option routers  192.168.20.2;
    next-server  192.168.20.131;
    option log-servers 192.168.20.131;
    option ntp-servers 192.168.20.131;
    option domain-name "cdac.in";
    option domain-name-servers  10.10.10.2;
    option interface-mtu 1500;
    option domain-search  "cdac.in";
    option cumulus-provision-url "http://192.168.20.131:80/install/postscripts/cumulusztp";
    zone cdac.in. {
       primary 10.10.10.2; key xcat_key; 
    }
    zone 20.168.192.IN-ADDR.ARPA. {
       primary 10.10.10.2; key xcat_key; 
    }
    if option user-class-identifier = "xNBA" and option client-architecture = 00:00 { #x86, xCAT Network Boot Agent
        always-broadcast on;
        filename = "http://192.168.20.131:80/tftpboot/xcat/xnba/nets/192.168.20.0_24";
    } else if option user-class-identifier = "xNBA" and option client-architecture = 00:09 { #x86, xCAT Network Boot Agent
        filename = "http://192.168.20.131:80/tftpboot/xcat/xnba/nets/192.168.20.0_24.uefi";
    } else if option client-architecture = 00:00  { #x86
        filename "xcat/xnba.kpxe";
    } else if option vendor-class-identifier = "Etherboot-5.4"  { #x86
        filename "xcat/xnba.kpxe";
    } else if option client-architecture = 00:07 { #x86_64 uefi
         filename "xcat/xnba.efi";
    } else if option client-architecture = 00:09 { #x86_64 uefi alternative id
         filename "xcat/xnba.efi";
    } else if option client-architecture = 00:02 { #ia64
         filename "elilo.efi";
    } else if option client-architecture = 00:0e { #OPAL-v3
         option conf-file = "http://192.168.20.131:80/tftpboot/pxelinux.cfg/p/192.168.20.0_24";
    } else if substring (option vendor-class-identifier,0,11) = "onie_vendor" { #for onie on cumulus switch
        option www-server = "http://192.168.20.131:80/install/onie/onie-installer";
    } else if substring(filename,0,1) = null { #otherwise, provide yaboot if the client isn't specific
         filename "/yaboot";
    }
  } # 192.168.20.0/255.255.255.0 subnet_end
} # ens33 nic_end
shared-network virbr0 {
  subnet 192.168.122.0 netmask 255.255.255.0 {
    authoritative;
    max-lease-time 43200;
    min-lease-time 43200;
    default-lease-time 43200;
    option routers  192.168.122.1;
    next-server  192.168.122.1;
    option log-servers 192.168.122.1;
    option ntp-servers 192.168.122.1;
    option domain-name "cdac.in";
    option domain-name-servers  10.10.10.2;
    option interface-mtu 1500;
    option domain-search  "cdac.in";
    option cumulus-provision-url "http://192.168.122.1:80/install/postscripts/cumulusztp";
    zone cdac.in. {
       primary 10.10.10.2; key xcat_key; 
    }
    zone 122.168.192.IN-ADDR.ARPA. {
       primary 10.10.10.2; key xcat_key; 
    }
    if option user-class-identifier = "xNBA" and option client-architecture = 00:00 { #x86, xCAT Network Boot Agent
        always-broadcast on;
        filename = "http://192.168.122.1:80/tftpboot/xcat/xnba/nets/192.168.122.0_24";
    } else if option user-class-identifier = "xNBA" and option client-architecture = 00:09 { #x86, xCAT Network Boot Agent
        filename = "http://192.168.122.1:80/tftpboot/xcat/xnba/nets/192.168.122.0_24.uefi";
    } else if option client-architecture = 00:00  { #x86
        filename "xcat/xnba.kpxe";
    } else if option vendor-class-identifier = "Etherboot-5.4"  { #x86
        filename "xcat/xnba.kpxe";
    } else if option client-architecture = 00:07 { #x86_64 uefi
         filename "xcat/xnba.efi";
    } else if option client-architecture = 00:09 { #x86_64 uefi alternative id
         filename "xcat/xnba.efi";
    } else if option client-architecture = 00:02 { #ia64
         filename "elilo.efi";
    } else if option client-architecture = 00:0e { #OPAL-v3
         option conf-file = "http://192.168.122.1:80/tftpboot/pxelinux.cfg/p/192.168.122.0_24";
    } else if substring (option vendor-class-identifier,0,11) = "onie_vendor" { #for onie on cumulus switch
        option www-server = "http://192.168.122.1:80/install/onie/onie-installer";
    } else if substring(filename,0,1) = null { #otherwise, provide yaboot if the client isn't specific
         filename "/yaboot";
    }
  } # 192.168.122.0/255.255.255.0 subnet_end
} # virbr0 nic_end
#definition for host cn00 aka host cn00 can be found in the dhcpd.leases file (typically /var/lib/dhcpd/dhcpd.leases)
[root@master compute]# vim /etc/hosts
[root@master compute]# lsdef cn00
Object name: cn00
    arch=x86_64
    currstate=netboot centos7.9-x86_64-compute
    groups=compute,all
    ip=10.10.10.3
    mac=00:0c:29:11:A6:49
    netboot=xnba
    os=centos7.9
    postbootscripts=otherpkgs
    postscripts=syslog,remoteshell,syncfiles
    profile=compute
    provmethod=centos7.9-x86_64-netboot-compute
[root@master compute]#  vim /etc/dhcp/dhcpd.conf.xcatbak
[root@master compute]# vim /install/custom/netboot/compute.synclist
[root@master compute]# cat /etc/shadow
root:$6$dm/zCUTo1cmA0ny2$GywBVrXnBS6JgBeIrz9gXkmYca.XnHZ.SBvyuDihWcMlg0XUTEhwShUGhaAng8SdDKNikiaRh/9.o1KG54lNo/::0:99999:7:::
bin:*:18353:0:99999:7:::
daemon:*:18353:0:99999:7:::
adm:*:18353:0:99999:7:::
lp:*:18353:0:99999:7:::
sync:*:18353:0:99999:7:::
shutdown:*:18353:0:99999:7:::
halt:*:18353:0:99999:7:::
mail:*:18353:0:99999:7:::
operator:*:18353:0:99999:7:::
games:*:18353:0:99999:7:::
ftp:*:18353:0:99999:7:::
nobody:*:18353:0:99999:7:::
systemd-network:!!:19511::::::
dbus:!!:19511::::::
polkitd:!!:19511::::::
libstoragemgmt:!!:19511::::::
colord:!!:19511::::::
rpc:!!:19511:0:99999:7:::
saned:!!:19511::::::
gluster:!!:19511::::::
amandabackup:!!:19511::::::
saslauth:!!:19511::::::
abrt:!!:19511::::::
setroubleshoot:!!:19511::::::
rtkit:!!:19511::::::
pulse:!!:19511::::::
radvd:!!:19511::::::
chrony:!!:19511::::::
unbound:!!:19511::::::
qemu:!!:19511::::::
tss:!!:19511::::::
sssd:!!:19511::::::
usbmuxd:!!:19511::::::
geoclue:!!:19511::::::
ntp:!!:19511::::::
gdm:!!:19511::::::
rpcuser:!!:19511::::::
nfsnobody:!!:19511::::::
gnome-initial-setup:!!:19511::::::
sshd:!!:19511::::::
avahi:!!:19511::::::
postfix:!!:19511::::::
tcpdump:!!:19511::::::
master:$6$K8bvw4t/pP4ce7vo$Yb.jQnVgyVCRIVJMPcAt/osCdsyDOUR6hP.1L7aeWN5uzDO67mc5AAQ5HZy1K8cRvsVhbmFici8X7NE4uoYBF.::0:99999:7:::
named:!!:19511::::::
dhcpd:!!:19511::::::
apache:!!:19511::::::
conserver:!!:19511::::::
[root@master compute]# ping 10.10
PING 10.10 (10.0.0.10) 56(84) bytes of data.
^C
--- 10.10 ping statistics ---
6 packets transmitted, 0 received, 100% packet loss, time 5029ms

[root@master compute]# ping 10.10.10.3
PING 10.10.10.3 (10.10.10.3) 56(84) bytes of data.
64 bytes from 10.10.10.3: icmp_seq=1 ttl=64 time=1.23 ms
64 bytes from 10.10.10.3: icmp_seq=2 ttl=64 time=0.901 ms
64 bytes from 10.10.10.3: icmp_seq=3 ttl=64 time=0.889 ms
64 bytes from 10.10.10.3: icmp_seq=4 ttl=64 time=0.929 ms
64 bytes from 10.10.10.3: icmp_seq=5 ttl=64 time=0.930 ms
^C
--- 10.10.10.3 ping statistics ---
5 packets transmitted, 5 received, 0% packet loss, time 4012ms
rtt min/avg/max/mdev = 0.889/0.976/1.234/0.134 ms
[root@master compute]# ssh root@test1
ssh: Could not resolve hostname test1: Name or service not known
[root@master compute]# cat /etc/hosts
127.0.0.1   localhost localhost.localdomain localhost4 localhost4.localdomain4
::1         localhost localhost.localdomain localhost6 localhost6.localdomain6
10.10.10.2 master master.cdac.in

10.10.10.3 cn00 cn00.cdac.in 
[root@master compute]# ssh root@cn00
Warning: Permanently added 'cn00,10.10.10.3' (ECDSA) to the list of known hosts.


Last failed login: Mon Jun  5 07:29:14 EDT 2023 on tty1
There was 1 failed login attempt since the last successful login.
[root@cn00 ~]# 
[root@cn00 ~]# passwd
-bash: passwd: command not found
[root@cn00 ~]# passwd root
-bash: passwd: command not found
[root@cn00 ~]# sudo passwd root
-bash: sudo: command not found
[root@cn00 ~]# passwd
-bash: passwd: command not found
[root@cn00 ~]# cat /etc/shadow
root:cluster:13880:0:99999:7:::
bin:*:18353:0:99999:7:::
daemon:*:18353:0:99999:7:::
adm:*:18353:0:99999:7:::
lp:*:18353:0:99999:7:::
sync:*:18353:0:99999:7:::
shutdown:*:18353:0:99999:7:::
halt:*:18353:0:99999:7:::
mail:*:18353:0:99999:7:::
operator:*:18353:0:99999:7:::
games:*:18353:0:99999:7:::
ftp:*:18353:0:99999:7:::
nobody:*:18353:0:99999:7:::
systemd-network:!!:19511::::::
dbus:!!:19511::::::
ntp:!!:19511::::::
rpc:!!:19511:0:99999:7:::
rpcuser:!!:19511::::::
nfsnobody:!!:19511::::::
sshd:!!:19511::::::
[root@cn00 ~]# hostname
cn00.cdac.in
[root@cn00 ~]# adduser cn00
[root@cn00 ~]# passwd cn00
-bash: passwd: command not found
[root@cn00 ~]# lsdef -t osimage centos7.9-x86_64-netboot-compute
-bash: lsdef: command not found
[root@cn00 ~]# exit
logout
Connection to cn00 closed.
[root@master compute]# lsdef -t osimage centos7.9-x86_64-netboot-compute
Object name: centos7.9-x86_64-netboot-compute
    exlist=/opt/xcat/share/xcat/netboot/centos/compute.centos7.exlist
    imagetype=linux
    osarch=x86_64
    osdistroname=centos7.9-x86_64
    osname=Linux
    osvers=centos7.9
    otherpkgdir=/install/post/otherpkgs/centos7.9/x86_64
    permission=755
    pkgdir=/install/centos7.9/x86_64
    pkglist=/opt/xcat/share/xcat/netboot/centos/compute.centos7.pkglist
    postinstall=/opt/xcat/share/xcat/netboot/centos/compute.centos7.postinstall
    profile=compute
    provmethod=netboot
    rootimgdir=/install/netboot/centos7.9/x86_64/compute
    synclists=/install/custom/netboot/compute.synclist
[root@master compute]# systemctl status sshd
● sshd.service - OpenSSH server daemon
   Loaded: loaded (/usr/lib/systemd/system/sshd.service; enabled; vendor preset: enabled)
   Active: active (running) since Sat 2023-06-03 11:19:03 EDT; 1 day 14h ago
     Docs: man:sshd(8)
           man:sshd_config(5)
 Main PID: 1389 (sshd)
    Tasks: 1
   CGroup: /system.slice/sshd.service
           └─1389 /usr/sbin/sshd -D

Jun 03 11:19:03 localhost.localdomain systemd[1]: Starting OpenSSH server daemon...
Jun 03 11:19:03 localhost.localdomain sshd[1389]: Server listening on 0.0.0.0 port 22.
Jun 03 11:19:03 localhost.localdomain sshd[1389]: Server listening on :: port 22.
Jun 03 11:19:03 localhost.localdomain systemd[1]: Started OpenSSH server daemon.
[root@master compute]# systemctl restart sshd
[root@master compute]# ssh root@cn00




^C

Last failed login: Mon Jun  5 07:39:04 EDT 2023 on tty1
There was 1 failed login attempt since the last successful login.

[root@cn00 ~]# 
[root@cn00 ~]# 
[root@cn00 ~]# 
[root@cn00 ~]# ssh cn00
ssh: Could not resolve hostname cn00: Name or service not known
[root@cn00 ~]# 
[root@cn00 ~]# 
[root@cn00 ~]# 
[root@cn00 ~]# 
[root@cn00 ~]# 
[root@cn00 ~]# 
[root@cn00 ~]# 
[root@cn00 ~]# exit 
logout
Connection to cn00 closed.
[root@master compute]# 
[root@master compute]# 
[root@master compute]# 
[root@master compute]# 
[root@master compute]# 
[root@master compute]# 
[root@master compute]# lsdef -t osimage 
centos7.9-x86_64-install-compute  (osimage)
centos7.9-x86_64-netboot-compute  (osimage)
centos7.9-x86_64-statelite-compute  (osimage)
[root@master compute]# packimage centos7.9-x86_64-netboot-compute
Packing contents of /install/netboot/centos7.9/x86_64/compute/rootimg
archive method:cpio
compress method:gzip

[root@master compute]# lsdef -i osimage centos7.9-x86_64-netboot-compute
Error: [master]: 'osimage' is not a valid attribute name for an object type of 'node'.
Error: [master]: Could not find an object named 'centos7.9-x86_64-netboot-compute' of type 'node'.
No object definitions have been found
[root@master compute]# lsdef -t osimage centos7.9-x86_64-netboot-compute
Object name: centos7.9-x86_64-netboot-compute
    exlist=/opt/xcat/share/xcat/netboot/centos/compute.centos7.exlist
    imagetype=linux
    osarch=x86_64
    osdistroname=centos7.9-x86_64
    osname=Linux
    osvers=centos7.9
    otherpkgdir=/install/post/otherpkgs/centos7.9/x86_64
    permission=755
    pkgdir=/install/centos7.9/x86_64
    pkglist=/opt/xcat/share/xcat/netboot/centos/compute.centos7.pkglist
    postinstall=/opt/xcat/share/xcat/netboot/centos/compute.centos7.postinstall
    profile=compute
    provmethod=netboot
    rootimgdir=/install/netboot/centos7.9/x86_64/compute
    synclists=/install/custom/netboot/compute.synclist
[root@master compute]# cat /install/custom/netboot/compute.synclist
cat: /install/custom/netboot/compute.synclist: No such file or directory
[root@master compute]# vim /install/custom/netboot/compute.synclist
[root@master compute]# vim /install/custom/netboot/compute.synclist
[root@master compute]# cat /install/custom/netboot/compute.synclist
/etc/passwd -> /etc/passwd
/etc/shadow -> /etc/shadow
/etc/group -> /etc/group
[root@master compute]# lsdef -t osimage centos7.9-x86_64-netboot-compute
Object name: centos7.9-x86_64-netboot-compute
    exlist=/opt/xcat/share/xcat/netboot/centos/compute.centos7.exlist
    imagetype=linux
    osarch=x86_64
    osdistroname=centos7.9-x86_64
    osname=Linux
    osvers=centos7.9
    otherpkgdir=/install/post/otherpkgs/centos7.9/x86_64
    permission=755
    pkgdir=/install/centos7.9/x86_64
    pkglist=/opt/xcat/share/xcat/netboot/centos/compute.centos7.pkglist
    postinstall=/opt/xcat/share/xcat/netboot/centos/compute.centos7.postinstall
    profile=compute
    provmethod=netboot
    rootimgdir=/install/netboot/centos7.9/x86_64/compute
    synclists=/install/custom/netboot/compute.synclist
[root@master compute]# nodeset compute osimage=centos7.9-x86_64-netboot-compute
cn00: netboot centos7.9-x86_64-compute
[root@master compute]# packimage centos7.9-x86_64-netboot-compute
Packing contents of /install/netboot/centos7.9/x86_64/compute/rootimg
archive method:cpio
compress method:gzip

[root@master compute]# makenetworks
Warning: [master]: The network entry '10_10_10_0-255_255_255_0' already exists in xCAT networks table. Cannot create a definition for '10_10_10_0-255_255_255_0'
Warning: [master]: The network entry '192_168_20_0-255_255_255_0' already exists in xCAT networks table. Cannot create a definition for '192_168_20_0-255_255_255_0'
[root@master compute]#  makedns -n
Warning: SELINUX is not disabled. The makedns command will not be able to generate a complete DNS setup. Disable SELINUX and run the command again.
Handling master in /etc/hosts.
Handling localhost in /etc/hosts.
Handling localhost in /etc/hosts.
Handling cn00 in /etc/hosts.
Getting reverse zones, this may take several minutes for a large cluster.
Completed getting reverse zones.
Updating zones.
Completed updating zones.
Restarting named
Restarting named complete
Updating DNS records, this may take several minutes for a large cluster.
Error: [master]: No reply received when sending DNS update to zone 10.10.10.IN-ADDR.ARPA.
^C[root@master compute]# 
[root@master compute]# 
[root@master compute]# sestatus
SELinux status:                 enabled
SELinuxfs mount:                /sys/fs/selinux
SELinux root directory:         /etc/selinux
Loaded policy name:             targeted
Current mode:                   permissive
Mode from config file:          disabled
Policy MLS status:              enabled
Policy deny_unknown status:     allowed
Max kernel policy version:      31
[root@master compute]# vim /etc/selinux/config 
[root@master compute]# setenforce 0
[root@master compute]# getenforce 
Permissive
[root@master compute]#  makedns -n
Warning: SELINUX is not disabled. The makedns command will not be able to generate a complete DNS setup. Disable SELINUX and run the command again.
Handling master in /etc/hosts.
Handling localhost in /etc/hosts.
Handling localhost in /etc/hosts.
Handling cn00 in /etc/hosts.
Getting reverse zones, this may take several minutes for a large cluster.
Completed getting reverse zones.
Updating zones.
Completed updating zones.
Restarting named
Restarting named complete
Updating DNS records, this may take several minutes for a large cluster.
Error: [master]: No reply received when sending DNS update to zone 10.10.10.IN-ADDR.ARPA.
Error: [master]: No reply received when sending DNS update to zone cdac.in.
Completed updating DNS records.
DNS setup is completed
[root@master compute]# 













