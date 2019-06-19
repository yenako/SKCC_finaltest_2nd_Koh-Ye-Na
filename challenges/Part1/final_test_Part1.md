# Part 1
### 1. Create a CDH Cluster on AWS
#### 1.a linux setup
<pre><code>
Using username "centos".
Authenticating with public key "imported-openssh-key"
Last login: Mon Jun 17 16:55:57 2019 from 125.252.39.29
[centos@ip-172-31-7-255 ~]$ sudo useradd -u 3800 training
[centos@ip-172-31-7-255 ~]$ sudo passwd training
Changing password for user training.
New password:
BAD PASSWORD: The password contains the user name in some form
Retype new password:
passwd: all authentication tokens updated successfully.
[centos@ip-172-31-7-255 ~]$ tail /etc/group
rpcuser:x:29:
nfsnobody:x:65534:
sshd:x:74:
postdrop:x:90:
postfix:x:89:
chrony:x:995:
centos:x:1000:
nscd:x:28:
ntp:x:38:
training:x:3800:
[centos@ip-172-31-7-255 ~]$ sudo groupadd skcc
[centos@ip-172-31-7-255 ~]$ sudo usermod -a -G skcc training
[centos@ip-172-31-7-255 ~]$ tail /etc/group
nfsnobody:x:65534:
sshd:x:74:
postdrop:x:90:
postfix:x:89:
chrony:x:995:
centos:x:1000:
nscd:x:28:
ntp:x:38:
training:x:3800:
skcc:x:3801:training
[centos@ip-172-31-7-255 ~]$ sudo vi /etc/sudoers
[centos@ip-172-31-7-255 ~]$ sudo vi /etc/sudoers
[centos@ip-172-31-7-255 ~]$ sudo ip-172-31-7-255
sudo: ip-172-31-7-255: command not found
[centos@ip-172-31-7-255 ~]$ host ip-172-31-7-255
-bash: host: command not found
[centos@ip-172-31-7-255 ~]$ cat /etc/os-release
NAME="CentOS Linux"
VERSION="7 (Core)"
ID="centos"
ID_LIKE="rhel fedora"
VERSION_ID="7"
PRETTY_NAME="CentOS Linux 7 (Core)"
ANSI_COLOR="0;31"
CPE_NAME="cpe:/o:centos:centos:7"
HOME_URL="https://www.centos.org/"
BUG_REPORT_URL="https://bugs.centos.org/"

CENTOS_MANTISBT_PROJECT="CentOS-7"
CENTOS_MANTISBT_PROJECT_VERSION="7"
REDHAT_SUPPORT_PRODUCT="centos"
REDHAT_SUPPORT_PRODUCT_VERSION="7"

[centos@ip-172-31-7-255 ~]$ sudo yum repolist enabled
Loaded plugins: fastestmirror
Loading mirror speeds from cached hostfile
 * base: ftp.neowiz.com
 * extras: mirror.kakao.com
 * updates: mirror.kakao.com
repo id                             repo name                             status
!base/7/x86_64                      CentOS-7 - Base                       10,019
!extras/7/x86_64                    CentOS-7 - Extras                        409
!updates/7/x86_64                   CentOS-7 - Updates                     2,076
repolist: 12,504
[centos@ip-172-31-7-255 ~]$ grep "training" /etc/passwd
training:x:3800:3800::/home/training:/bin/bash
[centos@ip-172-31-7-255 ~]$ grep "skcc" /etc/group
skcc:x:3801:training
[centos@ip-172-31-7-255 ~]$ getent group skcc
skcc:x:3801:training
[centos@ip-172-31-7-255 ~]$ getent passwd training
training:x:3800:3800::/home/training:/bin/bash
</code></pre>

#### 1.b  Install a MySQL Server
<pre><code>
[centos@ip-172-31-7-255 ~]$ sudo yum install -y mariadb-server
Loaded plugins: fastestmirror
Loading mirror speeds from cached hostfile
 * base: ftp.neowiz.com
 * extras: mirror.kakao.com
 * updates: mirror.kakao.com
base                                                     | 3.6 kB     00:00
extras                                                   | 3.4 kB     00:00
updates                                                  | 3.4 kB     00:00
(1/2): extras/7/x86_64/primary_db                          | 204 kB   00:00
(2/2): updates/7/x86_64/primary_db                         | 6.4 MB   00:00
Resolving Dependencies
--> Running transaction check
---> Package mariadb-server.x86_64 1:5.5.60-1.el7_5 will be installed
--> Processing Dependency: mariadb(x86-64) = 1:5.5.60-1.el7_5 for package: 1:mariadb-server-5.5.60-1.el7_5.x86_64
--> Processing Dependency: perl-DBI for package: 1:mariadb-server-5.5.60-1.el7_5.x86_64
--> Processing Dependency: perl-DBD-MySQL for package: 1:mariadb-server-5.5.60-1.el7_5.x86_64
--> Processing Dependency: perl(vars) for package: 1:mariadb-server-5.5.60-1.el7_5.x86_64
--> Processing Dependency: perl(strict) for package: 1:mariadb-server-5.5.60-1.el7_5.x86_64
--> Processing Dependency: perl(Sys::Hostname) for package: 1:mariadb-server-5.5.60-1.el7_5.x86_64
--> Processing Dependency: perl(POSIX) for package: 1:mariadb-server-5.5.60-1.el7_5.x86_64
--> Processing Dependency: perl(Getopt::Long) for package: 1:mariadb-server-5.5.60-1.el7_5.x86_64
--> Processing Dependency: perl(File::Temp) for package: 1:mariadb-server-5.5.60-1.el7_5.x86_64
--> Processing Dependency: perl(File::Path) for package: 1:mariadb-server-5.5.60-1.el7_5.x86_64
--> Processing Dependency: perl(File::Copy) for package: 1:mariadb-server-5.5.60-1.el7_5.x86_64
--> Processing Dependency: perl(File::Basename) for package: 1:mariadb-server-5.5.60-1.el7_5.x86_64
--> Processing Dependency: perl(Data::Dumper) for package: 1:mariadb-server-5.5.60-1.el7_5.x86_64
--> Processing Dependency: perl(DBI) for package: 1:mariadb-server-5.5.60-1.el7_5.x86_64
--> Processing Dependency: libaio.so.1(LIBAIO_0.4)(64bit) for package: 1:mariadb-server-5.5.60-1.el7_5.x86_64
--> Processing Dependency: libaio.so.1(LIBAIO_0.1)(64bit) for package: 1:mariadb-server-5.5.60-1.el7_5.x86_64
--> Processing Dependency: /usr/bin/perl for package: 1:mariadb-server-5.5.60-1.el7_5.x86_64
--> Processing Dependency: libaio.so.1()(64bit) for package: 1:mariadb-server-5.5.60-1.el7_5.x86_64
--> Running transaction check
---> Package libaio.x86_64 0:0.3.109-13.el7 will be installed
---> Package mariadb.x86_64 1:5.5.60-1.el7_5 will be installed
--> Processing Dependency: perl(Exporter) for package: 1:mariadb-5.5.60-1.el7_5.x86_64
---> Package perl.x86_64 4:5.16.3-294.el7_6 will be installed
--> Processing Dependency: perl-libs = 4:5.16.3-294.el7_6 for package: 4:perl-5.16.3-294.el7_6.x86_64
--> Processing Dependency: perl(Socket) >= 1.3 for package: 4:perl-5.16.3-294.el7_6.x86_64
--> Processing Dependency: perl(Scalar::Util) >= 1.10 for package: 4:perl-5.16.3-294.el7_6.x86_64
--> Processing Dependency: perl-macros for package: 4:perl-5.16.3-294.el7_6.x86_64
--> Processing Dependency: perl-libs for package: 4:perl-5.16.3-294.el7_6.x86_64
--> Processing Dependency: perl(threads::shared) for package: 4:perl-5.16.3-294.el7_6.x86_64
--> Processing Dependency: perl(threads) for package: 4:perl-5.16.3-294.el7_6.x86_64
--> Processing Dependency: perl(constant) for package: 4:perl-5.16.3-294.el7_6.x86_64
--> Processing Dependency: perl(Time::Local) for package: 4:perl-5.16.3-294.el7_6.x86_64
--> Processing Dependency: perl(Time::HiRes) for package: 4:perl-5.16.3-294.el7_6.x86_64
--> Processing Dependency: perl(Storable) for package: 4:perl-5.16.3-294.el7_6.x86_64
--> Processing Dependency: perl(Socket) for package: 4:perl-5.16.3-294.el7_6.x86_64
--> Processing Dependency: perl(Scalar::Util) for package: 4:perl-5.16.3-294.el7_6.x86_64
--> Processing Dependency: perl(Pod::Simple::XHTML) for package: 4:perl-5.16.3-294.el7_6.x86_64
--> Processing Dependency: perl(Pod::Simple::Search) for package: 4:perl-5.16.3-294.el7_6.x86_64
--> Processing Dependency: perl(Filter::Util::Call) for package: 4:perl-5.16.3-294.el7_6.x86_64
--> Processing Dependency: perl(File::Spec::Unix) for package: 4:perl-5.16.3-294.el7_6.x86_64
--> Processing Dependency: perl(File::Spec::Functions) for package: 4:perl-5.16.3-294.el7_6.x86_64
--> Processing Dependency: perl(File::Spec) for package: 4:perl-5.16.3-294.el7_6.x86_64
--> Processing Dependency: perl(Cwd) for package: 4:perl-5.16.3-294.el7_6.x86_64
--> Processing Dependency: perl(Carp) for package: 4:perl-5.16.3-294.el7_6.x86_64
--> Processing Dependency: libperl.so()(64bit) for package: 4:perl-5.16.3-294.el7_6.x86_64
---> Package perl-DBD-MySQL.x86_64 0:4.023-6.el7 will be installed
---> Package perl-DBI.x86_64 0:1.627-4.el7 will be installed
--> Processing Dependency: perl(RPC::PlServer) >= 0.2001 for package: perl-DBI-1.627-4.el7.x86_64
--> Processing Dependency: perl(RPC::PlClient) >= 0.2000 for package: perl-DBI-1.627-4.el7.x86_64
---> Package perl-Data-Dumper.x86_64 0:2.145-3.el7 will be installed
---> Package perl-File-Path.noarch 0:2.09-2.el7 will be installed
---> Package perl-File-Temp.noarch 0:0.23.01-3.el7 will be installed
---> Package perl-Getopt-Long.noarch 0:2.40-3.el7 will be installed
--> Processing Dependency: perl(Pod::Usage) >= 1.14 for package: perl-Getopt-Long-2.40-3.el7.noarch
--> Processing Dependency: perl(Text::ParseWords) for package: perl-Getopt-Long-2.40-3.el7.noarch
--> Running transaction check
---> Package perl-Carp.noarch 0:1.26-244.el7 will be installed
---> Package perl-Exporter.noarch 0:5.68-3.el7 will be installed
---> Package perl-Filter.x86_64 0:1.49-3.el7 will be installed
---> Package perl-PathTools.x86_64 0:3.40-5.el7 will be installed
---> Package perl-PlRPC.noarch 0:0.2020-14.el7 will be installed
--> Processing Dependency: perl(Net::Daemon) >= 0.13 for package: perl-PlRPC-0.2020-14.el7.noarch
--> Processing Dependency: perl(Net::Daemon::Test) for package: perl-PlRPC-0.2020-14.el7.noarch
--> Processing Dependency: perl(Net::Daemon::Log) for package: perl-PlRPC-0.2020-14.el7.noarch
--> Processing Dependency: perl(Compress::Zlib) for package: perl-PlRPC-0.2020-14.el7.noarch
---> Package perl-Pod-Simple.noarch 1:3.28-4.el7 will be installed
--> Processing Dependency: perl(Pod::Escapes) >= 1.04 for package: 1:perl-Pod-Simple-3.28-4.el7.noarch
--> Processing Dependency: perl(Encode) for package: 1:perl-Pod-Simple-3.28-4.el7.noarch
---> Package perl-Pod-Usage.noarch 0:1.63-3.el7 will be installed
--> Processing Dependency: perl(Pod::Text) >= 3.15 for package: perl-Pod-Usage-1.63-3.el7.noarch
--> Processing Dependency: perl-Pod-Perldoc for package: perl-Pod-Usage-1.63-3.el7.noarch
---> Package perl-Scalar-List-Utils.x86_64 0:1.27-248.el7 will be installed
---> Package perl-Socket.x86_64 0:2.010-4.el7 will be installed
---> Package perl-Storable.x86_64 0:2.45-3.el7 will be installed
---> Package perl-Text-ParseWords.noarch 0:3.29-4.el7 will be installed
---> Package perl-Time-HiRes.x86_64 4:1.9725-3.el7 will be installed
---> Package perl-Time-Local.noarch 0:1.2300-2.el7 will be installed
---> Package perl-constant.noarch 0:1.27-2.el7 will be installed
---> Package perl-libs.x86_64 4:5.16.3-294.el7_6 will be installed
---> Package perl-macros.x86_64 4:5.16.3-294.el7_6 will be installed
---> Package perl-threads.x86_64 0:1.87-4.el7 will be installed
---> Package perl-threads-shared.x86_64 0:1.43-6.el7 will be installed
--> Running transaction check
---> Package perl-Encode.x86_64 0:2.51-7.el7 will be installed
---> Package perl-IO-Compress.noarch 0:2.061-2.el7 will be installed
--> Processing Dependency: perl(Compress::Raw::Zlib) >= 2.061 for package: perl-IO-Compress-2.061-2.el7.noarch
--> Processing Dependency: perl(Compress::Raw::Bzip2) >= 2.061 for package: perl-IO-Compress-2.061-2.el7.noarch
---> Package perl-Net-Daemon.noarch 0:0.48-5.el7 will be installed
---> Package perl-Pod-Escapes.noarch 1:1.04-294.el7_6 will be installed
---> Package perl-Pod-Perldoc.noarch 0:3.20-4.el7 will be installed
--> Processing Dependency: perl(parent) for package: perl-Pod-Perldoc-3.20-4.el7.noarch
--> Processing Dependency: perl(HTTP::Tiny) for package: perl-Pod-Perldoc-3.20-4.el7.noarch
---> Package perl-podlators.noarch 0:2.5.1-3.el7 will be installed
--> Running transaction check
---> Package perl-Compress-Raw-Bzip2.x86_64 0:2.061-3.el7 will be installed
---> Package perl-Compress-Raw-Zlib.x86_64 1:2.061-4.el7 will be installed
---> Package perl-HTTP-Tiny.noarch 0:0.033-3.el7 will be installed
---> Package perl-parent.noarch 1:0.225-244.el7 will be installed
--> Finished Dependency Resolution

Dependencies Resolved

================================================================================
 Package                    Arch      Version                  Repository  Size
================================================================================
Installing:
 mariadb-server             x86_64    1:5.5.60-1.el7_5         base        11 M
Installing for dependencies:
 libaio                     x86_64    0.3.109-13.el7           base        24 k
 mariadb                    x86_64    1:5.5.60-1.el7_5         base       8.9 M
 perl                       x86_64    4:5.16.3-294.el7_6       updates    8.0 M
 perl-Carp                  noarch    1.26-244.el7             base        19 k
 perl-Compress-Raw-Bzip2    x86_64    2.061-3.el7              base        32 k
 perl-Compress-Raw-Zlib     x86_64    1:2.061-4.el7            base        57 k
 perl-DBD-MySQL             x86_64    4.023-6.el7              base       140 k
 perl-DBI                   x86_64    1.627-4.el7              base       802 k
 perl-Data-Dumper           x86_64    2.145-3.el7              base        47 k
 perl-Encode                x86_64    2.51-7.el7               base       1.5 M
 perl-Exporter              noarch    5.68-3.el7               base        28 k
 perl-File-Path             noarch    2.09-2.el7               base        26 k
 perl-File-Temp             noarch    0.23.01-3.el7            base        56 k
 perl-Filter                x86_64    1.49-3.el7               base        76 k
 perl-Getopt-Long           noarch    2.40-3.el7               base        56 k
 perl-HTTP-Tiny             noarch    0.033-3.el7              base        38 k
 perl-IO-Compress           noarch    2.061-2.el7              base       260 k
 perl-Net-Daemon            noarch    0.48-5.el7               base        51 k
 perl-PathTools             x86_64    3.40-5.el7               base        82 k
 perl-PlRPC                 noarch    0.2020-14.el7            base        36 k
 perl-Pod-Escapes           noarch    1:1.04-294.el7_6         updates     51 k
 perl-Pod-Perldoc           noarch    3.20-4.el7               base        87 k
 perl-Pod-Simple            noarch    1:3.28-4.el7             base       216 k
 perl-Pod-Usage             noarch    1.63-3.el7               base        27 k
 perl-Scalar-List-Utils     x86_64    1.27-248.el7             base        36 k
 perl-Socket                x86_64    2.010-4.el7              base        49 k
 perl-Storable              x86_64    2.45-3.el7               base        77 k
 perl-Text-ParseWords       noarch    3.29-4.el7               base        14 k
 perl-Time-HiRes            x86_64    4:1.9725-3.el7           base        45 k
 perl-Time-Local            noarch    1.2300-2.el7             base        24 k
 perl-constant              noarch    1.27-2.el7               base        19 k
 perl-libs                  x86_64    4:5.16.3-294.el7_6       updates    688 k
 perl-macros                x86_64    4:5.16.3-294.el7_6       updates     44 k
 perl-parent                noarch    1:0.225-244.el7          base        12 k
 perl-podlators             noarch    2.5.1-3.el7              base       112 k
 perl-threads               x86_64    1.87-4.el7               base        49 k
 perl-threads-shared        x86_64    1.43-6.el7               base        39 k

Transaction Summary
================================================================================
Install  1 Package (+37 Dependent packages)

Total download size: 33 M
Installed size: 147 M
Downloading packages:
(1/38): libaio-0.3.109-13.el7.x86_64.rpm                   |  24 kB   00:00
(2/38): mariadb-5.5.60-1.el7_5.x86_64.rpm                  | 8.9 MB   00:00
(3/38): perl-Carp-1.26-244.el7.noarch.rpm                  |  19 kB   00:00
(4/38): perl-Compress-Raw-Bzip2-2.061-3.el7.x86_64.rpm     |  32 kB   00:00
(5/38): perl-Compress-Raw-Zlib-2.061-4.el7.x86_64.rpm      |  57 kB   00:00
(6/38): perl-DBD-MySQL-4.023-6.el7.x86_64.rpm              | 140 kB   00:00
(7/38): mariadb-server-5.5.60-1.el7_5.x86_64.rpm           |  11 MB   00:00
(8/38): perl-DBI-1.627-4.el7.x86_64.rpm                    | 802 kB   00:00
(9/38): perl-5.16.3-294.el7_6.x86_64.rpm                   | 8.0 MB   00:00
(10/38): perl-Data-Dumper-2.145-3.el7.x86_64.rpm           |  47 kB   00:00
(11/38): perl-Exporter-5.68-3.el7.noarch.rpm               |  28 kB   00:00
(12/38): perl-File-Path-2.09-2.el7.noarch.rpm              |  26 kB   00:00
(13/38): perl-File-Temp-0.23.01-3.el7.noarch.rpm           |  56 kB   00:00
(14/38): perl-Encode-2.51-7.el7.x86_64.rpm                 | 1.5 MB   00:00
(15/38): perl-Filter-1.49-3.el7.x86_64.rpm                 |  76 kB   00:00
(16/38): perl-Getopt-Long-2.40-3.el7.noarch.rpm            |  56 kB   00:00
(17/38): perl-HTTP-Tiny-0.033-3.el7.noarch.rpm             |  38 kB   00:00
(18/38): perl-Net-Daemon-0.48-5.el7.noarch.rpm             |  51 kB   00:00
(19/38): perl-IO-Compress-2.061-2.el7.noarch.rpm           | 260 kB   00:00
(20/38): perl-PathTools-3.40-5.el7.x86_64.rpm              |  82 kB   00:00
(21/38): perl-PlRPC-0.2020-14.el7.noarch.rpm               |  36 kB   00:00
(22/38): perl-Pod-Perldoc-3.20-4.el7.noarch.rpm            |  87 kB   00:00
(23/38): perl-Pod-Usage-1.63-3.el7.noarch.rpm              |  27 kB   00:00
(24/38): perl-Scalar-List-Utils-1.27-248.el7.x86_64.rpm    |  36 kB   00:00
(25/38): perl-Socket-2.010-4.el7.x86_64.rpm                |  49 kB   00:00
(26/38): perl-Storable-2.45-3.el7.x86_64.rpm               |  77 kB   00:00
(27/38): perl-Text-ParseWords-3.29-4.el7.noarch.rpm        |  14 kB   00:00
(28/38): perl-Time-HiRes-1.9725-3.el7.x86_64.rpm           |  45 kB   00:00
(29/38): perl-Time-Local-1.2300-2.el7.noarch.rpm           |  24 kB   00:00
(30/38): perl-constant-1.27-2.el7.noarch.rpm               |  19 kB   00:00
(31/38): perl-Pod-Escapes-1.04-294.el7_6.noarch.rpm        |  51 kB   00:00
(32/38): perl-macros-5.16.3-294.el7_6.x86_64.rpm           |  44 kB   00:00
(33/38): perl-Pod-Simple-3.28-4.el7.noarch.rpm             | 216 kB   00:00
(34/38): perl-podlators-2.5.1-3.el7.noarch.rpm             | 112 kB   00:00
(35/38): perl-parent-0.225-244.el7.noarch.rpm              |  12 kB   00:00
(36/38): perl-threads-shared-1.43-6.el7.x86_64.rpm         |  39 kB   00:00
(37/38): perl-threads-1.87-4.el7.x86_64.rpm                |  49 kB   00:00
(38/38): perl-libs-5.16.3-294.el7_6.x86_64.rpm             | 688 kB   00:00
--------------------------------------------------------------------------------
Total                                               74 MB/s |  33 MB  00:00
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  Installing : 1:perl-parent-0.225-244.el7.noarch                          1/38
  Installing : perl-HTTP-Tiny-0.033-3.el7.noarch                           2/38
  Installing : perl-podlators-2.5.1-3.el7.noarch                           3/38
  Installing : perl-Pod-Perldoc-3.20-4.el7.noarch                          4/38
  Installing : 1:perl-Pod-Escapes-1.04-294.el7_6.noarch                    5/38
  Installing : perl-Text-ParseWords-3.29-4.el7.noarch                      6/38
  Installing : perl-Encode-2.51-7.el7.x86_64                               7/38
  Installing : perl-Pod-Usage-1.63-3.el7.noarch                            8/38
  Installing : 4:perl-libs-5.16.3-294.el7_6.x86_64                         9/38
  Installing : 4:perl-macros-5.16.3-294.el7_6.x86_64                      10/38
  Installing : perl-Storable-2.45-3.el7.x86_64                            11/38
  Installing : perl-Exporter-5.68-3.el7.noarch                            12/38
  Installing : perl-constant-1.27-2.el7.noarch                            13/38
  Installing : perl-Time-Local-1.2300-2.el7.noarch                        14/38
  Installing : perl-Socket-2.010-4.el7.x86_64                             15/38
  Installing : perl-Carp-1.26-244.el7.noarch                              16/38
  Installing : 4:perl-Time-HiRes-1.9725-3.el7.x86_64                      17/38
  Installing : perl-PathTools-3.40-5.el7.x86_64                           18/38
  Installing : perl-Scalar-List-Utils-1.27-248.el7.x86_64                 19/38
  Installing : perl-File-Temp-0.23.01-3.el7.noarch                        20/38
  Installing : perl-File-Path-2.09-2.el7.noarch                           21/38
  Installing : perl-threads-shared-1.43-6.el7.x86_64                      22/38
  Installing : perl-threads-1.87-4.el7.x86_64                             23/38
  Installing : perl-Filter-1.49-3.el7.x86_64                              24/38
  Installing : 1:perl-Pod-Simple-3.28-4.el7.noarch                        25/38
  Installing : perl-Getopt-Long-2.40-3.el7.noarch                         26/38
  Installing : 4:perl-5.16.3-294.el7_6.x86_64                             27/38
  Installing : perl-Data-Dumper-2.145-3.el7.x86_64                        28/38
  Installing : perl-Compress-Raw-Bzip2-2.061-3.el7.x86_64                 29/38
  Installing : perl-Net-Daemon-0.48-5.el7.noarch                          30/38
  Installing : 1:perl-Compress-Raw-Zlib-2.061-4.el7.x86_64                31/38
  Installing : perl-IO-Compress-2.061-2.el7.noarch                        32/38
  Installing : perl-PlRPC-0.2020-14.el7.noarch                            33/38
  Installing : perl-DBI-1.627-4.el7.x86_64                                34/38
  Installing : perl-DBD-MySQL-4.023-6.el7.x86_64                          35/38
  Installing : 1:mariadb-5.5.60-1.el7_5.x86_64                            36/38
  Installing : libaio-0.3.109-13.el7.x86_64                               37/38
  Installing : 1:mariadb-server-5.5.60-1.el7_5.x86_64                     38/38
  Verifying  : perl-HTTP-Tiny-0.033-3.el7.noarch                           1/38
  Verifying  : perl-threads-shared-1.43-6.el7.x86_64                       2/38
  Verifying  : perl-Storable-2.45-3.el7.x86_64                             3/38
  Verifying  : 1:perl-Pod-Escapes-1.04-294.el7_6.noarch                    4/38
  Verifying  : perl-DBD-MySQL-4.023-6.el7.x86_64                           5/38
  Verifying  : perl-Exporter-5.68-3.el7.noarch                             6/38
  Verifying  : perl-constant-1.27-2.el7.noarch                             7/38
  Verifying  : perl-PathTools-3.40-5.el7.x86_64                            8/38
  Verifying  : perl-Compress-Raw-Bzip2-2.061-3.el7.x86_64                  9/38
  Verifying  : 1:perl-parent-0.225-244.el7.noarch                         10/38
  Verifying  : 4:perl-5.16.3-294.el7_6.x86_64                             11/38
  Verifying  : perl-Net-Daemon-0.48-5.el7.noarch                          12/38
  Verifying  : 4:perl-libs-5.16.3-294.el7_6.x86_64                        13/38
  Verifying  : perl-File-Temp-0.23.01-3.el7.noarch                        14/38
  Verifying  : 1:perl-Pod-Simple-3.28-4.el7.noarch                        15/38
  Verifying  : perl-Time-Local-1.2300-2.el7.noarch                        16/38
  Verifying  : perl-DBI-1.627-4.el7.x86_64                                17/38
  Verifying  : libaio-0.3.109-13.el7.x86_64                               18/38
  Verifying  : 4:perl-macros-5.16.3-294.el7_6.x86_64                      19/38
  Verifying  : perl-Socket-2.010-4.el7.x86_64                             20/38
  Verifying  : perl-Encode-2.51-7.el7.x86_64                              21/38
  Verifying  : perl-Carp-1.26-244.el7.noarch                              22/38
  Verifying  : perl-Data-Dumper-2.145-3.el7.x86_64                        23/38
  Verifying  : 4:perl-Time-HiRes-1.9725-3.el7.x86_64                      24/38
  Verifying  : perl-Scalar-List-Utils-1.27-248.el7.x86_64                 25/38
  Verifying  : 1:perl-Compress-Raw-Zlib-2.061-4.el7.x86_64                26/38
  Verifying  : perl-IO-Compress-2.061-2.el7.noarch                        27/38
  Verifying  : perl-Pod-Usage-1.63-3.el7.noarch                           28/38
  Verifying  : perl-PlRPC-0.2020-14.el7.noarch                            29/38
  Verifying  : 1:mariadb-server-5.5.60-1.el7_5.x86_64                     30/38
  Verifying  : perl-Pod-Perldoc-3.20-4.el7.noarch                         31/38
  Verifying  : perl-podlators-2.5.1-3.el7.noarch                          32/38
  Verifying  : perl-File-Path-2.09-2.el7.noarch                           33/38
  Verifying  : perl-threads-1.87-4.el7.x86_64                             34/38
  Verifying  : perl-Filter-1.49-3.el7.x86_64                              35/38
  Verifying  : perl-Getopt-Long-2.40-3.el7.noarch                         36/38
  Verifying  : perl-Text-ParseWords-3.29-4.el7.noarch                     37/38
  Verifying  : 1:mariadb-5.5.60-1.el7_5.x86_64                            38/38

Installed:
  mariadb-server.x86_64 1:5.5.60-1.el7_5

Dependency Installed:
  libaio.x86_64 0:0.3.109-13.el7
  mariadb.x86_64 1:5.5.60-1.el7_5
  perl.x86_64 4:5.16.3-294.el7_6
  perl-Carp.noarch 0:1.26-244.el7
  perl-Compress-Raw-Bzip2.x86_64 0:2.061-3.el7
  perl-Compress-Raw-Zlib.x86_64 1:2.061-4.el7
  perl-DBD-MySQL.x86_64 0:4.023-6.el7
  perl-DBI.x86_64 0:1.627-4.el7
  perl-Data-Dumper.x86_64 0:2.145-3.el7
  perl-Encode.x86_64 0:2.51-7.el7
  perl-Exporter.noarch 0:5.68-3.el7
  perl-File-Path.noarch 0:2.09-2.el7
  perl-File-Temp.noarch 0:0.23.01-3.el7
  perl-Filter.x86_64 0:1.49-3.el7
  perl-Getopt-Long.noarch 0:2.40-3.el7
  perl-HTTP-Tiny.noarch 0:0.033-3.el7
  perl-IO-Compress.noarch 0:2.061-2.el7
  perl-Net-Daemon.noarch 0:0.48-5.el7
  perl-PathTools.x86_64 0:3.40-5.el7
  perl-PlRPC.noarch 0:0.2020-14.el7
  perl-Pod-Escapes.noarch 1:1.04-294.el7_6
  perl-Pod-Perldoc.noarch 0:3.20-4.el7
  perl-Pod-Simple.noarch 1:3.28-4.el7
  perl-Pod-Usage.noarch 0:1.63-3.el7
  perl-Scalar-List-Utils.x86_64 0:1.27-248.el7
  perl-Socket.x86_64 0:2.010-4.el7
  perl-Storable.x86_64 0:2.45-3.el7
  perl-Text-ParseWords.noarch 0:3.29-4.el7
  perl-Time-HiRes.x86_64 4:1.9725-3.el7
  perl-Time-Local.noarch 0:1.2300-2.el7
  perl-constant.noarch 0:1.27-2.el7
  perl-libs.x86_64 4:5.16.3-294.el7_6
  perl-macros.x86_64 4:5.16.3-294.el7_6
  perl-parent.noarch 1:0.225-244.el7
  perl-podlators.noarch 0:2.5.1-3.el7
  perl-threads.x86_64 0:1.87-4.el7
  perl-threads-shared.x86_64 0:1.43-6.el7

Complete!
[centos@ip-172-31-7-255 ~]$ sudo systemctl stop mariadb
[centos@ip-172-31-7-255 ~]$ sudo vi /etc/my.cnf
[centos@ip-172-31-7-255 ~]$ sudo vi /etc/my.cnf
[centos@ip-172-31-7-255 ~]$ sudo systemctl enable mariadb
Created symlink from /etc/systemd/system/multi-user.target.wants/mariadb.service to /usr/lib/systemd/system/mariadb.service.
[centos@ip-172-31-7-255 ~]$ sudo systemctl start mariadb
[centos@ip-172-31-7-255 ~]$ sudo /usr/bin/mysql_secure_installation

NOTE: RUNNING ALL PARTS OF THIS SCRIPT IS RECOMMENDED FOR ALL MariaDB
      SERVERS IN PRODUCTION USE!  PLEASE READ EACH STEP CAREFULLY!

In order to log into MariaDB to secure it, we'll need the current
password for the root user.  If you've just installed MariaDB, and
you haven't set the root password yet, the password will be blank,
so you should just press enter here.

Enter current password for root (enter for none):
OK, successfully used password, moving on...

Setting the root password ensures that nobody can log into the MariaDB
root user without the proper authorisation.

Set root password? [Y/n] y
New password:
Re-enter new password:
Password updated successfully!
Reloading privilege tables..
 ... Success!


By default, a MariaDB installation has an anonymous user, allowing anyone
to log into MariaDB without having to have a user account created for
them.  This is intended only for testing, and to make the installation
go a bit smoother.  You should remove them before moving into a
production environment.

Remove anonymous users? [Y/n] y
 ... Success!

Normally, root should only be allowed to connect from 'localhost'.  This
ensures that someone cannot guess at the root password from the network.

Disallow root login remotely? [Y/n] n
 ... skipping.

By default, MariaDB comes with a database named 'test' that anyone can
access.  This is also intended only for testing, and should be removed
before moving into a production environment.

Remove test database and access to it? [Y/n] y
 - Dropping test database...
 ... Success!
 - Removing privileges on test database...
 ... Success!

Reloading the privilege tables will ensure that all changes made so far
will take effect immediately.

Reload privilege tables now? [Y/n] y
 ... Success!

Cleaning up...

All done!  If you've completed all of the above steps, your MariaDB
installation should now be secure.

Thanks for using MariaDB!

[centos@ip-172-31-7-255 ~]$ sudo yum install -y wget
Loaded plugins: fastestmirror
Loading mirror speeds from cached hostfile
 * base: ftp.neowiz.com
 * extras: mirror.kakao.com
 * updates: mirror.kakao.com
Package wget-1.14-18.el7_6.1.x86_64 already installed and latest version
Nothing to do
[centos@ip-172-31-7-255 ~]$ sudo wget "https://dev.mysql.com/get/Downloads/Connector-J/mysql-connector-java-5.1.46.tar.gz"
--2019-06-19 04:35:32--  https://dev.mysql.com/get/Downloads/Connector-J/mysql-connector-java-5.1.46.tar.gz
Resolving dev.mysql.com (dev.mysql.com)... 137.254.60.11
Connecting to dev.mysql.com (dev.mysql.com)|137.254.60.11|:443... connected.
HTTP request sent, awaiting response... 302 Found
Location: https://cdn.mysql.com//Downloads/Connector-J/mysql-connector-java-5.1.46.tar.gz [following]
--2019-06-19 04:35:33--  https://cdn.mysql.com//Downloads/Connector-J/mysql-connector-java-5.1.46.tar.gz
Resolving cdn.mysql.com (cdn.mysql.com)... 23.212.13.170
Connecting to cdn.mysql.com (cdn.mysql.com)|23.212.13.170|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 4434926 (4.2M) [application/x-tar-gz]
Saving to: ‘mysql-connector-java-5.1.46.tar.gz’

100%[======================================>] 4,434,926   --.-K/s   in 0.03s

2019-06-19 04:35:34 (142 MB/s) - ‘mysql-connector-java-5.1.46.tar.gz’ saved [4434926/4434926]

[centos@ip-172-31-7-255 ~]$ tar zxvf mysql-connector-java-5.1.46.tar.gz
mysql-connector-java-5.1.46/
mysql-connector-java-5.1.46/src/
mysql-connector-java-5.1.46/src/com/
mysql-connector-java-5.1.46/src/com/mysql/
  (... 생략)
mysql-connector-java-5.1.46/src/testsuite/ssl-test-certs/mykey.pem
mysql-connector-java-5.1.46/src/testsuite/ssl-test-certs/mykey.pub
mysql-connector-java-5.1.46/src/testsuite/ssl-test-certs/server-cert.pem
mysql-connector-java-5.1.46/src/testsuite/ssl-test-certs/server-key.pem
[centos@ip-172-31-7-255 ~]$ sudo mkdir -p /usr/share/java/
[centos@ip-172-31-7-255 ~]$ cd mysql-connector-java-5.1.46
[centos@ip-172-31-7-255 mysql-connector-java-5.1.46]$ sudo cp mysql-connector-java-5.1.46-bin.jar /usr/share/java/mysql-connector-java.jar
[centos@ip-172-31-7-255 mysql-connector-java-5.1.46]$ mysql -u root -p
Enter password:
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 9
Server version: 5.5.60-MariaDB MariaDB Server

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]> drop database if exists amon;
Query OK, 0 rows affected, 1 warning (0.00 sec)

MariaDB [(none)]> create database amon character set utf8;
Query OK, 1 row affected (0.00 sec)

MariaDB [(none)]> grant all privileges on amon.* to amon@'%' identified by 'amon_password';
Query OK, 0 rows affected (0.00 sec)

MariaDB [(none)]>
MariaDB [(none)]> drop database if exists rman;
Query OK, 0 rows affected, 1 warning (0.00 sec)

MariaDB [(none)]> create database rman character set utf8;
Query OK, 1 row affected (0.00 sec)

MariaDB [(none)]> grant all privileges on rman.* to rman@'%' identified by 'rman_password';
Query OK, 0 rows affected (0.00 sec)

MariaDB [(none)]>
MariaDB [(none)]> drop database if exists metastore;
Query OK, 0 rows affected, 1 warning (0.00 sec)

MariaDB [(none)]> create database metastore character set utf8;
Query OK, 1 row affected (0.00 sec)

MariaDB [(none)]> grant all privileges on metastore.* to hive@'%' identified by 'hive_password';
Query OK, 0 rows affected (0.00 sec)

MariaDB [(none)]>
MariaDB [(none)]> drop database if exists sentry;
Query OK, 0 rows affected, 1 warning (0.00 sec)

MariaDB [(none)]> create database sentry character set utf8;
Query OK, 1 row affected (0.00 sec)

MariaDB [(none)]> grant all privileges on sentry.* to sentry@'%' identified by 'sentry_password';
Query OK, 0 rows affected (0.00 sec)

MariaDB [(none)]>
MariaDB [(none)]> drop database if exists nav;
Query OK, 0 rows affected, 1 warning (0.00 sec)

MariaDB [(none)]> create database nav character set utf8;

Query OK, 1 row affected (0.00 sec)

MariaDB [(none)]> grant all privileges on nav.* to nav@'%' identified by 'nav_password';
Query OK, 0 rows affected (0.00 sec)

MariaDB [(none)]>
MariaDB [(none)]> drop database if exists navms;
Query OK, 0 rows affected, 1 warning (0.00 sec)

MariaDB [(none)]> create database navms character set utf8;
Query OK, 1 row affected (0.00 sec)

MariaDB [(none)]> grant all privileges on navms.* to navms@'%' identified by 'navms_password';
Query OK, 0 rows affected (0.00 sec)

MariaDB [(none)]>
MariaDB [(none)]> drop database if exists cdh;
Query OK, 0 rows affected, 1 warning (0.00 sec)

MariaDB [(none)]> create database cdh character set utf8;
Query OK, 1 row affected (0.00 sec)

MariaDB [(none)]> grant all privileges on cdh.* to cdh@'%' identified by 'cdh';
drop database if exists hue;
Query OK, 0 rows affected (0.00 sec)

MariaDB [(none)]>
MariaDB [(none)]> drop database if exists hue;
Query OK, 0 rows affected, 1 warning (0.00 sec)

MariaDB [(none)]> create database hue character set utf8;
Query OK, 1 row affected (0.00 sec)

MariaDB [(none)]> grant all privileges on hue.* to hue@'%' identified by 'hue';
Query OK, 0 rows affected (0.00 sec)

MariaDB [(none)]>
MariaDB [(none)]> drop database if exists oozie;
Query OK, 0 rows affected, 1 warning (0.00 sec)

MariaDB [(none)]> create database oozie character set utf8;
Query OK, 1 row affected (0.00 sec)

MariaDB [(none)]> grant all privileges on oozie.* to oozie@'%' identified by 'oozie';
Query OK, 0 rows affected (0.00 sec)

MariaDB [(none)]>
MariaDB [(none)]> drop database if exists hive;
Query OK, 0 rows affected, 1 warning (0.00 sec)

MariaDB [(none)]> create database hive character set utf8;
Query OK, 1 row affected (0.00 sec)

MariaDB [(none)]> grant all privileges on hive.* to hive@'%' identified by 'hive';
Query OK, 0 rows affected (0.00 sec)

MariaDB [(none)]>
MariaDB [(none)]> drop database if exists scm;
Query OK, 0 rows affected, 1 warning (0.00 sec)

MariaDB [(none)]> create database scm character set utf8;
Query OK, 1 row affected (0.00 sec)

MariaDB [(none)]> grant all privileges on scm.* to scm@'%' identified by 'scm';
Query OK, 0 rows affected (0.00 sec)

MariaDB [(none)]> show database;
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MariaDB server version for the right syntax to use near 'database' at line 1
MariaDB [(none)]> flush privileges;
Query OK, 0 rows affected (0.00 sec)

MariaDB [(none)]> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| amon               |
| cdh                |
| hive               |
| hue                |
| metastore          |
| mysql              |
| nav                |
| navms              |
| oozie              |
| performance_schema |
| rman               |
| scm                |
| sentry             |
+--------------------+
14 rows in set (0.00 sec)

MariaDB [(none)]> exit;
Bye
[centos@ip-172-31-7-255 mysql-connector-java-5.1.46]$ cd ~
[centos@ip-172-31-7-255 ~]$ mysql --version
mysql  Ver 15.1 Distrib 5.5.60-MariaDB, for Linux (x86_64) using readline 5.1
</cdoe></pre>

### 1.c Install Cloudera Manager
<pre><code>
[centos@ip-172-31-7-255 ~]$ sudo vi /etc/hosts
[centos@ip-172-31-7-255 ~]$ sudo hostnamectl set-hostname ts1.test.com
[centos@ip-172-31-7-255 ~]$ hostname -f
ts1.test.com
[centos@ip-172-31-7-255 ~]$ yum list java*jdk-devel
Loaded plugins: fastestmirror
Determining fastest mirrors
 * base: mirror.kakao.com
 * extras: mirror.kakao.com
 * updates: mirror.kakao.com
Available Packages
java-1.6.0-openjdk-devel.x86_64        1:1.6.0.41-1.13.13.1.el7_3        base
java-1.7.0-openjdk-devel.x86_64        1:1.7.0.221-2.6.18.0.el7_6        updates
java-1.8.0-openjdk-devel.i686          1:1.8.0.212.b04-0.el7_6           updates
java-1.8.0-openjdk-devel.x86_64        1:1.8.0.212.b04-0.el7_6           updates
java-11-openjdk-devel.i686             1:11.0.3.7-0.el7_6                updates
java-11-openjdk-devel.x86_64           1:11.0.3.7-0.el7_6                updates
[centos@ip-172-31-7-255 ~]$ sudo yum install java-1.8.0-openjdk-devel.x86_64
Loaded plugins: fastestmirror
Loading mirror speeds from cached hostfile
 * base: ftp.neowiz.com
 * extras: mirror.kakao.com
 * updates: mirror.kakao.com
Resolving Dependencies
--> Running transaction check
---> Package java-1.8.0-openjdk-devel.x86_64 1:1.8.0.212.b04-0.el7_6 will be installed
--> Processing Dependency: java-1.8.0-openjdk(x86-64) = 1:1.8.0.212.b04-0.el7_6 for package: 1:java-1.8.0-openjdk-devel-1.8.0.212.b04-0.el7_6.x86_64
--> Processing Dependency: libjvm.so()(64bit) for package: 1:java-1.8.0-openjdk-devel-1.8.0.212.b04-0.el7_6.x86_64
--> Processing Dependency: libjava.so()(64bit) for package: 1:java-1.8.0-openjdk-devel-1.8.0.212.b04-0.el7_6.x86_64
      (... 생략)
---> Package mesa-libGL.x86_64 0:18.0.5-4.el7_6 will be installed
--> Processing Dependency: libXxf86vm.so.1()(64bit) for package: mesa-libGL-18.0.5-4.el7_6.x86_64
--> Running transaction check
---> Package libXxf86vm.x86_64 0:1.1.4-1.el7 will be installed
---> Package libdrm.x86_64 0:2.4.91-3.el7 will be installed
--> Processing Dependency: libpciaccess.so.0()(64bit) for package: libdrm-2.4.91-3.el7.x86_64
---> Package libwayland-client.x86_64 0:1.15.0-1.el7 will be installed
---> Package libwayland-server.x86_64 0:1.15.0-1.el7 will be installed
---> Package libxshmfence.x86_64 0:1.2-1.el7 will be installed
---> Package mesa-libgbm.x86_64 0:18.0.5-4.el7_6 will be installed
---> Package mesa-libglapi.x86_64 0:18.0.5-4.el7_6 will be installed
--> Running transaction check
---> Package libpciaccess.x86_64 0:0.14-1.el7 will be installed
--> Finished Dependency Resolution

Dependencies Resolved

================================================================================
 Package                     Arch   Version                       Repository
                                                                           Size
================================================================================
Installing:
 java-1.8.0-openjdk-devel    x86_64 1:1.8.0.212.b04-0.el7_6       updates 9.8 M
Installing for dependencies:
 alsa-lib                    x86_64 1.1.6-2.el7                   base    424 k
 atk                         x86_64 2.28.1-1.el7                  base    263 k
 avahi-libs                  x86_64 0.6.31-19.el7                 base     61 k
 cairo                       x86_64 1.15.12-3.el7                 base    741 k
 copy-jdk-configs            noarch 3.3-10.el7_5                  base     21 k
 cups-libs                   x86_64 1:1.6.3-35.el7                base    357 k
 dejavu-fonts-common         noarch 2.33-6.el7                    base     64 k
 dejavu-sans-fonts           noarch 2.33-6.el7                    base    1.4 M
 fontconfig                  x86_64 2.13.0-4.3.el7                base    254 k
 fontpackages-filesystem     noarch 1.44-8.el7                    base    9.9 k
 fribidi                     x86_64 1.0.2-1.el7                   base     79 k
 gdk-pixbuf2                 x86_64 2.36.12-3.el7                 base    570 k
 giflib                      x86_64 4.1.6-9.el7                   base     40 k
 graphite2                   x86_64 1.3.10-1.el7_3                base    115 k
 gtk-update-icon-cache       x86_64 3.22.30-3.el7                 base     28 k
 gtk2                        x86_64 2.24.31-1.el7                 base    3.4 M
 harfbuzz                    x86_64 1.7.5-2.el7                   base    267 k
 hicolor-icon-theme          noarch 0.12-7.el7                    base     42 k
 jasper-libs                 x86_64 1.900.1-33.el7                base    150 k
 java-1.8.0-openjdk          x86_64 1:1.8.0.212.b04-0.el7_6       updates 270 k
 java-1.8.0-openjdk-headless x86_64 1:1.8.0.212.b04-0.el7_6       updates  32 M
 javapackages-tools          noarch 3.4.1-11.el7                  base     73 k
 jbigkit-libs                x86_64 2.0-11.el7                    base     46 k
 libICE                      x86_64 1.0.9-9.el7                   base     66 k
 libSM                       x86_64 1.2.2-2.el7                   base     39 k
 libX11                      x86_64 1.6.5-2.el7                   base    606 k
 libX11-common               noarch 1.6.5-2.el7                   base    164 k
 libXau                      x86_64 1.0.8-2.1.el7                 base     29 k
 libXcomposite               x86_64 0.4.4-4.1.el7                 base     22 k
 libXcursor                  x86_64 1.1.15-1.el7                  base     30 k
 libXdamage                  x86_64 1.1.4-4.1.el7                 base     20 k
 libXext                     x86_64 1.3.3-3.el7                   base     39 k
 libXfixes                   x86_64 5.0.3-1.el7                   base     18 k
 libXft                      x86_64 2.3.2-2.el7                   base     58 k
 libXi                       x86_64 1.7.9-1.el7                   base     40 k
 libXinerama                 x86_64 1.1.3-2.1.el7                 base     14 k
 libXrandr                   x86_64 1.5.1-2.el7                   base     27 k
 libXrender                  x86_64 0.9.10-1.el7                  base     26 k
 libXtst                     x86_64 1.2.3-1.el7                   base     20 k
 libXxf86vm                  x86_64 1.1.4-1.el7                   base     18 k
 libdrm                      x86_64 2.4.91-3.el7                  base    153 k
 libfontenc                  x86_64 1.1.3-3.el7                   base     31 k
 libglvnd                    x86_64 1:1.0.1-0.8.git5baa1e5.el7    base     89 k
 libglvnd-egl                x86_64 1:1.0.1-0.8.git5baa1e5.el7    base     44 k
 libglvnd-glx                x86_64 1:1.0.1-0.8.git5baa1e5.el7    base    125 k
 libjpeg-turbo               x86_64 1.2.90-6.el7                  base    134 k
 libpciaccess                x86_64 0.14-1.el7                    base     26 k
 libthai                     x86_64 0.1.14-9.el7                  base    187 k
 libtiff                     x86_64 4.0.3-27.el7_3                base    170 k
 libwayland-client           x86_64 1.15.0-1.el7                  base     33 k
 libwayland-server           x86_64 1.15.0-1.el7                  base     39 k
 libxcb                      x86_64 1.13-1.el7                    base    214 k
 libxshmfence                x86_64 1.2-1.el7                     base    7.2 k
 libxslt                     x86_64 1.1.28-5.el7                  base    242 k
 lksctp-tools                x86_64 1.0.17-2.el7                  base     88 k
 mesa-libEGL                 x86_64 18.0.5-4.el7_6                updates 102 k
 mesa-libGL                  x86_64 18.0.5-4.el7_6                updates 162 k
 mesa-libgbm                 x86_64 18.0.5-4.el7_6                updates  38 k
 mesa-libglapi               x86_64 18.0.5-4.el7_6                updates  44 k
 pango                       x86_64 1.42.4-2.el7_6                updates 280 k
 pcsc-lite-libs              x86_64 1.8.8-8.el7                   base     34 k
 pixman                      x86_64 0.34.0-1.el7                  base    248 k
 python-javapackages         noarch 3.4.1-11.el7                  base     31 k
 python-lxml                 x86_64 3.2.1-4.el7                   base    758 k
 ttmkfdir                    x86_64 3.0.9-42.el7                  base     48 k
 tzdata-java                 noarch 2019a-1.el7                   updates 187 k
 xorg-x11-font-utils         x86_64 1:7.5-21.el7                  base    104 k
 xorg-x11-fonts-Type1        noarch 7.5-9.el7                     base    521 k

Transaction Summary
================================================================================
Install  1 Package (+68 Dependent packages)

Total download size: 55 M
Installed size: 188 M
Is this ok [y/d/N]: y
Is this ok [y/d/N]: y
Downloading packages:
(1/69): alsa-lib-1.1.6-2.el7.x86_64.rpm                    | 424 kB   00:00
(2/69): avahi-libs-0.6.31-19.el7.x86_64.rpm                |  61 kB   00:00
(3/69): atk-2.28.1-1.el7.x86_64.rpm                        | 263 kB   00:00
(4/69): copy-jdk-configs-3.3-10.el7_5.noarch.rpm           |  21 kB   00:00
(5/69): cairo-1.15.12-3.el7.x86_64.rpm                     | 741 kB   00:00
(6/69): dejavu-fonts-common-2.33-6.el7.noarch.rpm          |  64 kB   00:00
(7/69): cups-libs-1.6.3-35.el7.x86_64.rpm                  | 357 kB   00:00
(8/69): fontconfig-2.13.0-4.3.el7.x86_64.rpm               | 254 kB   00:00
(9/69): fontpackages-filesystem-1.44-8.el7.noarch.rpm      | 9.9 kB   00:00
(10/69): dejavu-sans-fonts-2.33-6.el7.noarch.rpm           | 1.4 MB   00:00
(11/69): fribidi-1.0.2-1.el7.x86_64.rpm                    |  79 kB   00:00
(12/69): giflib-4.1.6-9.el7.x86_64.rpm                     |  40 kB   00:00
(13/69): gdk-pixbuf2-2.36.12-3.el7.x86_64.rpm              | 570 kB   00:00
(14/69): graphite2-1.3.10-1.el7_3.x86_64.rpm               | 115 kB   00:00
(15/69): gtk-update-icon-cache-3.22.30-3.el7.x86_64.rpm    |  28 kB   00:00
(16/69): harfbuzz-1.7.5-2.el7.x86_64.rpm                   | 267 kB   00:00
(17/69): hicolor-icon-theme-0.12-7.el7.noarch.rpm          |  42 kB   00:00
(18/69): jasper-libs-1.900.1-33.el7.x86_64.rpm             | 150 kB   00:00
(19/69): gtk2-2.24.31-1.el7.x86_64.rpm                     | 3.4 MB   00:00
(20/69): java-1.8.0-openjdk-1.8.0.212.b04-0.el7_6.x86_64.r | 270 kB   00:00
(21/69): javapackages-tools-3.4.1-11.el7.noarch.rpm        |  73 kB   00:00
(22/69): libICE-1.0.9-9.el7.x86_64.rpm                     |  66 kB   00:00
(23/69): jbigkit-libs-2.0-11.el7.x86_64.rpm                |  46 kB   00:00
(24/69): libSM-1.2.2-2.el7.x86_64.rpm                      |  39 kB   00:00
(25/69): libX11-common-1.6.5-2.el7.noarch.rpm              | 164 kB   00:00
(26/69): libXau-1.0.8-2.1.el7.x86_64.rpm                   |  29 kB   00:00
(27/69): libXcomposite-0.4.4-4.1.el7.x86_64.rpm            |  22 kB   00:00
(28/69): libX11-1.6.5-2.el7.x86_64.rpm                     | 606 kB   00:00
(29/69): libXcursor-1.1.15-1.el7.x86_64.rpm                |  30 kB   00:00
(30/69): libXdamage-1.1.4-4.1.el7.x86_64.rpm               |  20 kB   00:00
(31/69): libXext-1.3.3-3.el7.x86_64.rpm                    |  39 kB   00:00
(32/69): libXfixes-5.0.3-1.el7.x86_64.rpm                  |  18 kB   00:00
(33/69): libXft-2.3.2-2.el7.x86_64.rpm                     |  58 kB   00:00
(34/69): libXi-1.7.9-1.el7.x86_64.rpm                      |  40 kB   00:00
(35/69): libXinerama-1.1.3-2.1.el7.x86_64.rpm              |  14 kB   00:00
(36/69): libXrandr-1.5.1-2.el7.x86_64.rpm                  |  27 kB   00:00
(37/69): libXrender-0.9.10-1.el7.x86_64.rpm                |  26 kB   00:00
(38/69): libXtst-1.2.3-1.el7.x86_64.rpm                    |  20 kB   00:00
(39/69): libXxf86vm-1.1.4-1.el7.x86_64.rpm                 |  18 kB   00:00
(40/69): libfontenc-1.1.3-3.el7.x86_64.rpm                 |  31 kB   00:00
(41/69): libdrm-2.4.91-3.el7.x86_64.rpm                    | 153 kB   00:00
(42/69): libglvnd-egl-1.0.1-0.8.git5baa1e5.el7.x86_64.rpm  |  44 kB   00:00
(43/69): libglvnd-1.0.1-0.8.git5baa1e5.el7.x86_64.rpm      |  89 kB   00:00
(44/69): libglvnd-glx-1.0.1-0.8.git5baa1e5.el7.x86_64.rpm  | 125 kB   00:00
(45/69): java-1.8.0-openjdk-devel-1.8.0.212.b04-0.el7_6.x8 | 9.8 MB   00:00
(46/69): libjpeg-turbo-1.2.90-6.el7.x86_64.rpm             | 134 kB   00:00
(47/69): libpciaccess-0.14-1.el7.x86_64.rpm                |  26 kB   00:00
(48/69): libthai-0.1.14-9.el7.x86_64.rpm                   | 187 kB   00:00
(49/69): libtiff-4.0.3-27.el7_3.x86_64.rpm                 | 170 kB   00:00
(50/69): libwayland-client-1.15.0-1.el7.x86_64.rpm         |  33 kB   00:00
(51/69): libwayland-server-1.15.0-1.el7.x86_64.rpm         |  39 kB   00:00
(52/69): libxshmfence-1.2-1.el7.x86_64.rpm                 | 7.2 kB   00:00
(53/69): libxcb-1.13-1.el7.x86_64.rpm                      | 214 kB   00:00
(54/69): libxslt-1.1.28-5.el7.x86_64.rpm                   | 242 kB   00:00
(55/69): lksctp-tools-1.0.17-2.el7.x86_64.rpm              |  88 kB   00:00
(56/69): java-1.8.0-openjdk-headless-1.8.0.212.b04-0.el7_6 |  32 MB   00:00
(57/69): mesa-libEGL-18.0.5-4.el7_6.x86_64.rpm             | 102 kB   00:00
(58/69): mesa-libGL-18.0.5-4.el7_6.x86_64.rpm              | 162 kB   00:00
(59/69): mesa-libgbm-18.0.5-4.el7_6.x86_64.rpm             |  38 kB   00:00
(60/69): mesa-libglapi-18.0.5-4.el7_6.x86_64.rpm           |  44 kB   00:00
(61/69): pango-1.42.4-2.el7_6.x86_64.rpm                   | 280 kB   00:00
(62/69): pcsc-lite-libs-1.8.8-8.el7.x86_64.rpm             |  34 kB   00:00
(63/69): python-javapackages-3.4.1-11.el7.noarch.rpm       |  31 kB   00:00
(64/69): pixman-0.34.0-1.el7.x86_64.rpm                    | 248 kB   00:00
(65/69): python-lxml-3.2.1-4.el7.x86_64.rpm                | 758 kB   00:00
(66/69): ttmkfdir-3.0.9-42.el7.x86_64.rpm                  |  48 kB   00:00
(67/69): xorg-x11-font-utils-7.5-21.el7.x86_64.rpm         | 104 kB   00:00
(68/69): xorg-x11-fonts-Type1-7.5-9.el7.noarch.rpm         | 521 kB   00:00
(69/69): tzdata-java-2019a-1.el7.noarch.rpm                | 187 kB   00:00
--------------------------------------------------------------------------------
Total                                               67 MB/s |  55 MB  00:00
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  Installing : libjpeg-turbo-1.2.90-6.el7.x86_64                           1/69
  Installing : mesa-libglapi-18.0.5-4.el7_6.x86_64                         2/69
  Installing : libxshmfence-1.2-1.el7.x86_64                               3/69
  Installing : libxslt-1.1.28-5.el7.x86_64                                 4/69
  Installing : 1:libglvnd-1.0.1-0.8.git5baa1e5.el7.x86_64                  5/69
  Installing : fontpackages-filesystem-1.44-8.el7.noarch                   6/69
  Installing : libICE-1.0.9-9.el7.x86_64                                   7/69
  Installing : libwayland-server-1.15.0-1.el7.x86_64                       8/69
  Installing : libSM-1.2.2-2.el7.x86_64                                    9/69
  Installing : dejavu-fonts-common-2.33-6.el7.noarch                      10/69
  Installing : dejavu-sans-fonts-2.33-6.el7.noarch                        11/69
  Installing : fontconfig-2.13.0-4.3.el7.x86_64                           12/69
  Installing : python-lxml-3.2.1-4.el7.x86_64                             13/69
  Installing : python-javapackages-3.4.1-11.el7.noarch                    14/69
  Installing : javapackages-tools-3.4.1-11.el7.noarch                     15/69
  Installing : jasper-libs-1.900.1-33.el7.x86_64                          16/69
  Installing : pixman-0.34.0-1.el7.x86_64                                 17/69
  Installing : libfontenc-1.1.3-3.el7.x86_64                              18/69
  Installing : 1:xorg-x11-font-utils-7.5-21.el7.x86_64                    19/69
  Installing : libthai-0.1.14-9.el7.x86_64                                20/69
  Installing : libX11-common-1.6.5-2.el7.noarch                           21/69
  Installing : libXau-1.0.8-2.1.el7.x86_64                                22/69
  Installing : libxcb-1.13-1.el7.x86_64                                   23/69
  Installing : libX11-1.6.5-2.el7.x86_64                                  24/69
  Installing : libXext-1.3.3-3.el7.x86_64                                 25/69
  Installing : libXrender-0.9.10-1.el7.x86_64                             26/69
  Installing : libXfixes-5.0.3-1.el7.x86_64                               27/69
  Installing : libXi-1.7.9-1.el7.x86_64                                   28/69
  Installing : libXdamage-1.1.4-4.1.el7.x86_64                            29/69
  Installing : libXcomposite-0.4.4-4.1.el7.x86_64                         30/69
  Installing : libXtst-1.2.3-1.el7.x86_64                                 31/69
  Installing : libXcursor-1.1.15-1.el7.x86_64                             32/69
  Installing : libXft-2.3.2-2.el7.x86_64                                  33/69
  Installing : libXrandr-1.5.1-2.el7.x86_64                               34/69
  Installing : libXinerama-1.1.3-2.1.el7.x86_64                           35/69
  Installing : libXxf86vm-1.1.4-1.el7.x86_64                              36/69
  Installing : giflib-4.1.6-9.el7.x86_64                                  37/69
  Installing : jbigkit-libs-2.0-11.el7.x86_64                             38/69
  Installing : libtiff-4.0.3-27.el7_3.x86_64                              39/69
  Installing : gdk-pixbuf2-2.36.12-3.el7.x86_64                           40/69
  Installing : gtk-update-icon-cache-3.22.30-3.el7.x86_64                 41/69
  Installing : pcsc-lite-libs-1.8.8-8.el7.x86_64                          42/69
  Installing : tzdata-java-2019a-1.el7.noarch                             43/69
  Installing : fribidi-1.0.2-1.el7.x86_64                                 44/69
  Installing : hicolor-icon-theme-0.12-7.el7.noarch                       45/69
  Installing : lksctp-tools-1.0.17-2.el7.x86_64                           46/69
  Installing : alsa-lib-1.1.6-2.el7.x86_64                                47/69
  Installing : ttmkfdir-3.0.9-42.el7.x86_64                               48/69
  Installing : xorg-x11-fonts-Type1-7.5-9.el7.noarch                      49/69
  Installing : copy-jdk-configs-3.3-10.el7_5.noarch                       50/69
  Installing : avahi-libs-0.6.31-19.el7.x86_64                            51/69
  Installing : 1:cups-libs-1.6.3-35.el7.x86_64                            52/69
  Installing : 1:java-1.8.0-openjdk-headless-1.8.0.212.b04-0.el7_6.x86_   53/69
  Installing : libwayland-client-1.15.0-1.el7.x86_64                      54/69
  Installing : graphite2-1.3.10-1.el7_3.x86_64                            55/69
  Installing : harfbuzz-1.7.5-2.el7.x86_64                                56/69
  Installing : atk-2.28.1-1.el7.x86_64                                    57/69
  Installing : libpciaccess-0.14-1.el7.x86_64                             58/69
  Installing : libdrm-2.4.91-3.el7.x86_64                                 59/69
  Installing : mesa-libgbm-18.0.5-4.el7_6.x86_64                          60/69
  Installing : 1:libglvnd-egl-1.0.1-0.8.git5baa1e5.el7.x86_64             61/69
  Installing : mesa-libEGL-18.0.5-4.el7_6.x86_64                          62/69
  Installing : mesa-libGL-18.0.5-4.el7_6.x86_64                           63/69
  Installing : 1:libglvnd-glx-1.0.1-0.8.git5baa1e5.el7.x86_64             64/69
  Installing : cairo-1.15.12-3.el7.x86_64                                 65/69
  Installing : pango-1.42.4-2.el7_6.x86_64                                66/69
  Installing : gtk2-2.24.31-1.el7.x86_64                                  67/69
  Installing : 1:java-1.8.0-openjdk-1.8.0.212.b04-0.el7_6.x86_64          68/69
  Installing : 1:java-1.8.0-openjdk-devel-1.8.0.212.b04-0.el7_6.x86_64    69/69
  Verifying  : libXext-1.3.3-3.el7.x86_64                                  1/69
  Verifying  : libpciaccess-0.14-1.el7.x86_64                              2/69
  Verifying  : libXi-1.7.9-1.el7.x86_64                                    3/69
  Verifying  : libtiff-4.0.3-27.el7_3.x86_64                               4/69
  Verifying  : fontconfig-2.13.0-4.3.el7.x86_64                            5/69
  Verifying  : giflib-4.1.6-9.el7.x86_64                                   6/69
  Verifying  : libXinerama-1.1.3-2.1.el7.x86_64                            7/69
  Verifying  : libXrender-0.9.10-1.el7.x86_64                              8/69
  Verifying  : atk-2.28.1-1.el7.x86_64                                     9/69
  Verifying  : 1:xorg-x11-font-utils-7.5-21.el7.x86_64                    10/69
  Verifying  : libXxf86vm-1.1.4-1.el7.x86_64                              11/69
  Verifying  : graphite2-1.3.10-1.el7_3.x86_64                            12/69
  Verifying  : libwayland-server-1.15.0-1.el7.x86_64                      13/69
  Verifying  : libXcursor-1.1.15-1.el7.x86_64                             14/69
  Verifying  : libICE-1.0.9-9.el7.x86_64                                  15/69
  Verifying  : 1:java-1.8.0-openjdk-headless-1.8.0.212.b04-0.el7_6.x86_   16/69
  Verifying  : dejavu-fonts-common-2.33-6.el7.noarch                      17/69
  Verifying  : gtk2-2.24.31-1.el7.x86_64                                  18/69
  Verifying  : pango-1.42.4-2.el7_6.x86_64                                19/69
  Verifying  : libjpeg-turbo-1.2.90-6.el7.x86_64                          20/69
  Verifying  : 1:java-1.8.0-openjdk-devel-1.8.0.212.b04-0.el7_6.x86_64    21/69
  Verifying  : libwayland-client-1.15.0-1.el7.x86_64                      22/69
  Verifying  : avahi-libs-0.6.31-19.el7.x86_64                            23/69
  Verifying  : gdk-pixbuf2-2.36.12-3.el7.x86_64                           24/69
  Verifying  : fontpackages-filesystem-1.44-8.el7.noarch                  25/69
  Verifying  : copy-jdk-configs-3.3-10.el7_5.noarch                       26/69
  Verifying  : python-javapackages-3.4.1-11.el7.noarch                    27/69
  Verifying  : libdrm-2.4.91-3.el7.x86_64                                 28/69
  Verifying  : mesa-libgbm-18.0.5-4.el7_6.x86_64                          29/69
  Verifying  : ttmkfdir-3.0.9-42.el7.x86_64                               30/69
  Verifying  : alsa-lib-1.1.6-2.el7.x86_64                                31/69
  Verifying  : libXcomposite-0.4.4-4.1.el7.x86_64                         32/69
  Verifying  : libXtst-1.2.3-1.el7.x86_64                                 33/69
  Verifying  : 1:libglvnd-1.0.1-0.8.git5baa1e5.el7.x86_64                 34/69
  Verifying  : libxcb-1.13-1.el7.x86_64                                   35/69
  Verifying  : libXft-2.3.2-2.el7.x86_64                                  36/69
  Verifying  : 1:libglvnd-egl-1.0.1-0.8.git5baa1e5.el7.x86_64             37/69
  Verifying  : 1:java-1.8.0-openjdk-1.8.0.212.b04-0.el7_6.x86_64          38/69
  Verifying  : lksctp-tools-1.0.17-2.el7.x86_64                           39/69
  Verifying  : hicolor-icon-theme-0.12-7.el7.noarch                       40/69
  Verifying  : mesa-libEGL-18.0.5-4.el7_6.x86_64                          41/69
  Verifying  : mesa-libGL-18.0.5-4.el7_6.x86_64                           42/69
  Verifying  : xorg-x11-fonts-Type1-7.5-9.el7.noarch                      43/69
  Verifying  : harfbuzz-1.7.5-2.el7.x86_64                                44/69
  Verifying  : libxslt-1.1.28-5.el7.x86_64                                45/69
  Verifying  : fribidi-1.0.2-1.el7.x86_64                                 46/69
  Verifying  : libX11-1.6.5-2.el7.x86_64                                  47/69
  Verifying  : 1:libglvnd-glx-1.0.1-0.8.git5baa1e5.el7.x86_64             48/69
  Verifying  : dejavu-sans-fonts-2.33-6.el7.noarch                        49/69
  Verifying  : tzdata-java-2019a-1.el7.noarch                             50/69
  Verifying  : pcsc-lite-libs-1.8.8-8.el7.x86_64                          51/69
  Verifying  : javapackages-tools-3.4.1-11.el7.noarch                     52/69
  Verifying  : jbigkit-libs-2.0-11.el7.x86_64                             53/69
  Verifying  : cairo-1.15.12-3.el7.x86_64                                 54/69
  Verifying  : 1:cups-libs-1.6.3-35.el7.x86_64                            55/69
  Verifying  : libxshmfence-1.2-1.el7.x86_64                              56/69
  Verifying  : libXau-1.0.8-2.1.el7.x86_64                                57/69
  Verifying  : libSM-1.2.2-2.el7.x86_64                                   58/69
  Verifying  : jasper-libs-1.900.1-33.el7.x86_64                          59/69
  Verifying  : python-lxml-3.2.1-4.el7.x86_64                             60/69
  Verifying  : libX11-common-1.6.5-2.el7.noarch                           61/69
  Verifying  : libXrandr-1.5.1-2.el7.x86_64                               62/69
  Verifying  : libthai-0.1.14-9.el7.x86_64                                63/69
  Verifying  : libXdamage-1.1.4-4.1.el7.x86_64                            64/69
  Verifying  : libXfixes-5.0.3-1.el7.x86_64                               65/69
  Verifying  : libfontenc-1.1.3-3.el7.x86_64                              66/69
  Verifying  : mesa-libglapi-18.0.5-4.el7_6.x86_64                        67/69
  Verifying  : gtk-update-icon-cache-3.22.30-3.el7.x86_64                 68/69
  Verifying  : pixman-0.34.0-1.el7.x86_64                                 69/69

Installed:
  java-1.8.0-openjdk-devel.x86_64 1:1.8.0.212.b04-0.el7_6

Dependency Installed:
  alsa-lib.x86_64 0:1.1.6-2.el7
  atk.x86_64 0:2.28.1-1.el7
  avahi-libs.x86_64 0:0.6.31-19.el7
  cairo.x86_64 0:1.15.12-3.el7
  copy-jdk-configs.noarch 0:3.3-10.el7_5
  cups-libs.x86_64 1:1.6.3-35.el7
  dejavu-fonts-common.noarch 0:2.33-6.el7
  dejavu-sans-fonts.noarch 0:2.33-6.el7
  fontconfig.x86_64 0:2.13.0-4.3.el7
  fontpackages-filesystem.noarch 0:1.44-8.el7
  fribidi.x86_64 0:1.0.2-1.el7
  gdk-pixbuf2.x86_64 0:2.36.12-3.el7
  giflib.x86_64 0:4.1.6-9.el7
  graphite2.x86_64 0:1.3.10-1.el7_3
  gtk-update-icon-cache.x86_64 0:3.22.30-3.el7
  gtk2.x86_64 0:2.24.31-1.el7
  harfbuzz.x86_64 0:1.7.5-2.el7
  hicolor-icon-theme.noarch 0:0.12-7.el7
  jasper-libs.x86_64 0:1.900.1-33.el7
  java-1.8.0-openjdk.x86_64 1:1.8.0.212.b04-0.el7_6
  java-1.8.0-openjdk-headless.x86_64 1:1.8.0.212.b04-0.el7_6
  javapackages-tools.noarch 0:3.4.1-11.el7
  jbigkit-libs.x86_64 0:2.0-11.el7
  libICE.x86_64 0:1.0.9-9.el7
  libSM.x86_64 0:1.2.2-2.el7
  libX11.x86_64 0:1.6.5-2.el7
  libX11-common.noarch 0:1.6.5-2.el7
  libXau.x86_64 0:1.0.8-2.1.el7
  libXcomposite.x86_64 0:0.4.4-4.1.el7
  libXcursor.x86_64 0:1.1.15-1.el7
  libXdamage.x86_64 0:1.1.4-4.1.el7
  libXext.x86_64 0:1.3.3-3.el7
  libXfixes.x86_64 0:5.0.3-1.el7
  libXft.x86_64 0:2.3.2-2.el7
  libXi.x86_64 0:1.7.9-1.el7
  libXinerama.x86_64 0:1.1.3-2.1.el7
  libXrandr.x86_64 0:1.5.1-2.el7
  libXrender.x86_64 0:0.9.10-1.el7
  libXtst.x86_64 0:1.2.3-1.el7
  libXxf86vm.x86_64 0:1.1.4-1.el7
  libdrm.x86_64 0:2.4.91-3.el7
  libfontenc.x86_64 0:1.1.3-3.el7
  libglvnd.x86_64 1:1.0.1-0.8.git5baa1e5.el7
  libglvnd-egl.x86_64 1:1.0.1-0.8.git5baa1e5.el7
  libglvnd-glx.x86_64 1:1.0.1-0.8.git5baa1e5.el7
  libjpeg-turbo.x86_64 0:1.2.90-6.el7
  libpciaccess.x86_64 0:0.14-1.el7
  libthai.x86_64 0:0.1.14-9.el7
  libtiff.x86_64 0:4.0.3-27.el7_3
  libwayland-client.x86_64 0:1.15.0-1.el7
  libwayland-server.x86_64 0:1.15.0-1.el7
  libxcb.x86_64 0:1.13-1.el7
  libxshmfence.x86_64 0:1.2-1.el7
  libxslt.x86_64 0:1.1.28-5.el7
  lksctp-tools.x86_64 0:1.0.17-2.el7
  mesa-libEGL.x86_64 0:18.0.5-4.el7_6
  mesa-libGL.x86_64 0:18.0.5-4.el7_6
  mesa-libgbm.x86_64 0:18.0.5-4.el7_6
  mesa-libglapi.x86_64 0:18.0.5-4.el7_6
  pango.x86_64 0:1.42.4-2.el7_6
  pcsc-lite-libs.x86_64 0:1.8.8-8.el7
  pixman.x86_64 0:0.34.0-1.el7
  python-javapackages.noarch 0:3.4.1-11.el7
  python-lxml.x86_64 0:3.2.1-4.el7
  ttmkfdir.x86_64 0:3.0.9-42.el7
  tzdata-java.noarch 0:2019a-1.el7
  xorg-x11-font-utils.x86_64 1:7.5-21.el7
  xorg-x11-fonts-Type1.noarch 0:7.5-9.el7

Complete!
[centos@ip-172-31-7-255 ~]$ java -version
openjdk version "1.8.0_212"
OpenJDK Runtime Environment (build 1.8.0_212-b04)
OpenJDK 64-Bit Server VM (build 25.212-b04, mixed mode)
[centos@ip-172-31-7-255 ~]$ sudo wget https://archive.cloudera.com/cm5/redhat/7/x86_64/cm/cloudera-manager.repo -P /etc/yum.repos.d/
--2019-06-19 04:46:45--  https://archive.cloudera.com/cm5/redhat/7/x86_64/cm/cloudera-manager.repo
Resolving archive.cloudera.com (archive.cloudera.com)... 151.101.108.167
Connecting to archive.cloudera.com (archive.cloudera.com)|151.101.108.167|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 290 [binary/octet-stream]
Saving to: ‘/etc/yum.repos.d/cloudera-manager.repo’

100%[======================================>] 290         --.-K/s   in 0s

2019-06-19 04:46:45 (64.9 MB/s) - ‘/etc/yum.repos.d/cloudera-manager.repo’ saved [290/290]

[centos@ip-172-31-7-255 ~]$ sudo vi /etc/yum.repos.d/cloudera-manager.repo
[centos@ip-172-31-7-255 ~]$ sudo vi /etc/yum.repos.d/cloudera-manager.repo
[centos@ip-172-31-7-255 ~]$ sudo vi /etc/yum.repos.d/cloudera-manager.repo
[centos@ip-172-31-7-255 ~]$ sudo rpm --import https://archive.cloudera.com/cm5/redhat/7/x86_64/cm/RPM-GPG-KEY-cloudera
[centos@ip-172-31-7-255 ~]$ sudo yum install -y cloudera-manager-daemons cloudera-manager-server
Loaded plugins: fastestmirror
Loading mirror speeds from cached hostfile
 * base: ftp.neowiz.com
 * extras: mirror.kakao.com
 * updates: mirror.kakao.com
cloudera-manager                                         |  951 B     00:00
cloudera-manager/primary                                   | 4.3 kB   00:00
cloudera-manager                                                            7/7
Resolving Dependencies
--> Running transaction check
---> Package cloudera-manager-daemons.x86_64 0:5.15.2-1.cm5152.p0.2.el7 will be installed
---> Package cloudera-manager-server.x86_64 0:5.15.2-1.cm5152.p0.2.el7 will be installed
--> Finished Dependency Resolution

Dependencies Resolved

================================================================================
 Package                 Arch   Version                  Repository        Size
================================================================================
Installing:
 cloudera-manager-daemons
                         x86_64 5.15.2-1.cm5152.p0.2.el7 cloudera-manager 752 M
 cloudera-manager-server x86_64 5.15.2-1.cm5152.p0.2.el7 cloudera-manager 8.5 k

Transaction Summary
================================================================================
Install  2 Packages

Total download size: 752 M
Installed size: 933 M
Downloading packages:
(1/2): cloudera-manager-server-5.15.2-1.cm5152.p0.2.el7.x8 | 8.5 kB   00:00
(2/2): cloudera-manager-daemons-5.15.2-1.cm5152.p0.2.el7.x | 752 MB   00:17
--------------------------------------------------------------------------------
Total                                               43 MB/s | 752 MB  00:17
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  Installing : cloudera-manager-daemons-5.15.2-1.cm5152.p0.2.el7.x86_64     1/2
  Installing : cloudera-manager-server-5.15.2-1.cm5152.p0.2.el7.x86_64      2/2
  Verifying  : cloudera-manager-daemons-5.15.2-1.cm5152.p0.2.el7.x86_64     1/2
  Verifying  : cloudera-manager-server-5.15.2-1.cm5152.p0.2.el7.x86_64      2/2

Installed:
  cloudera-manager-daemons.x86_64 0:5.15.2-1.cm5152.p0.2.el7
  cloudera-manager-server.x86_64 0:5.15.2-1.cm5152.p0.2.el7

Complete!
[centos@ip-172-31-7-255 ~]$ sudo /usr/share/cmf/schema/scm_prepare_database.sh mysql scm scm
Enter SCM password:
JAVA_HOME=/usr/lib/jvm/java-openjdk
Verifying that we can write to /etc/cloudera-scm-server
Creating SCM configuration file in /etc/cloudera-scm-server
Executing:  /usr/lib/jvm/java-openjdk/bin/java -cp /usr/share/java/mysql-connector-java.jar:/usr/share/java/oracle-connector-java.jar:/usr/share/java/postgresql-connector-java.jar:/usr/share/cmf/schema/../lib/* com.cloudera.enterprise.dbutil.DbCommandExecutor /etc/cloudera-scm-server/db.properties com.cloudera.cmf.db.
[                          main] DbCommandExecutor              INFO  Successfully connected to database.
All done, your SCM database is configured correctly!
[centos@ip-172-31-7-255 ~]$ sudo systemctl stop cloudera-scm-server
[centos@ip-172-31-7-255 ~]$ sudo vi /etc/cloudera-scm-server/db.mgmt.properties
[centos@ip-172-31-7-255 ~]$ sudo systemctl start cloudera-scm-server
[centos@ip-172-31-7-255 ~]$ sudo passwd centos
Changing password for user centos.
New password:
BAD PASSWORD: The password is shorter than 8 characters
Retype new password:
passwd: all authentication tokens updated successfully.
[centos@ip-172-31-7-255 ~]$ sudo vi /etc/ssh/sshd_config
[centos@ip-172-31-7-255 ~]$ sudo systemctl restart sshd.service
[centos@ip-172-31-7-255 ~]$ sudo vi /etc/ssh/sshd_config
[centos@ip-172-31-7-255 ~]$ hostname -f
ts1.test.com
[centos@ip-172-31-7-255 ~]$ sudo tail -f /var/log/cloudera-scm-server/cloudera-scm-server.log
        at org.mortbay.jetty.HttpConnection.handleRequest(HttpConnection.java:542)
        at org.mortbay.jetty.HttpConnection$RequestHandler.content(HttpConnection.java:945)
        at org.mortbay.jetty.HttpParser.parseNext(HttpParser.java:756)
        at org.mortbay.jetty.HttpParser.parseAvailable(HttpParser.java:212)
        at org.mortbay.jetty.HttpConnection.handle(HttpConnection.java:404)
        at org.mortbay.io.nio.SelectChannelEndPoint.run(SelectChannelEndPoint.java:410)
        at org.mortbay.thread.QueuedThreadPool$PoolThread.run(QueuedThreadPool.java:582)
2019-06-19 05:47:22,882 INFO avro-servlet-hb-processor-0:com.cloudera.server.common.AgentAvroServlet: (8 skipped) AgentAvroServlet: heartbeat processing stats: average=3ms, min=2ms, max=66ms.
2019-06-19 05:48:22,927 INFO avro-servlet-hb-processor-0:com.cloudera.server.common.AgentAvroServlet: (7 skipped) AgentAvroServlet: heartbeat processing stats: average=3ms, min=2ms, max=66ms.
2019-06-19 05:49:22,985 INFO avro-servlet-hb-processor-0:com.cloudera.server.common.AgentAvroServlet: (7 skipped) AgentAvroServlet: heartbeat processing stats: average=3ms, min=2ms, max=66ms.
^C
[centos@ip-172-31-7-255 ~]$
</code></pre>


## 2. In MySQL create the sample tables that will be used for the rest of the tests

<pre><code>
Using username "centos".
Authenticating with public key "imported-openssh-key"
Last login: Wed Jun 19 05:08:41 2019 from ts1.test.com
[centos@ts1 ~]$ mysql -u root -p
Enter password:
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 510
Server version: 5.5.60-MariaDB MariaDB Server

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]> create database test;
Query OK, 1 row affected (0.00 sec)

MariaDB [(none)]> use test;
Database changed
MariaDB [test]>
</code></pre>

## 3. Extract tables authors and posts from the database and create Hive tables
<pre><code>
[centos@ts1 ~]$ sqoop import --connect jdbc:mysql://172.31.7.255:3306/test --username training --password training --table authors --target-dir /user/authors
Warning: /opt/cloudera/parcels/CDH-5.15.2-1.cdh5.15.2.p0.3/bin/../lib/sqoop/../accumulo does not exist! Accumulo imports will fail.
Please set $ACCUMULO_HOME to the root of your Accumulo installation.
19/06/19 08:07:12 INFO sqoop.Sqoop: Running Sqoop version: 1.4.6-cdh5.15.2
19/06/19 08:07:12 WARN tool.BaseSqoopTool: Setting your password on the command-line is insecure. Consider using -P instead.
19/06/19 08:07:12 INFO manager.MySQLManager: Preparing to use a MySQL streaming resultset.
19/06/19 08:07:12 INFO tool.CodeGenTool: Beginning code generation
19/06/19 08:07:13 INFO manager.SqlManager: Executing SQL statement: SELECT t.* FROM `authors` AS t LIMIT 1
19/06/19 08:07:13 INFO manager.SqlManager: Executing SQL statement: SELECT t.* FROM `authors` AS t LIMIT 1
19/06/19 08:07:13 INFO orm.CompilationManager: HADOOP_MAPRED_HOME is /opt/cloudera/parcels/CDH-5.15.2-1.cdh5.15.2.p0.3/bin/../lib/sqoop/../hadoop-mapreduce
Note: /tmp/sqoop-centos/compile/e27a9b2563cbce6ae0e15eb2dd6973d3/authors.java uses or overrides a deprecated API.
Note: Recompile with -Xlint:deprecation for details.
19/06/19 08:07:14 INFO orm.CompilationManager: Writing jar file: /tmp/sqoop-centos/compile/e27a9b2563cbce6ae0e15eb2dd6973d3/authors.jar
19/06/19 08:07:14 WARN manager.MySQLManager: It looks like you are importing from mysql.
19/06/19 08:07:14 WARN manager.MySQLManager: This transfer can be faster! Use the --direct
19/06/19 08:07:14 WARN manager.MySQLManager: option to exercise a MySQL-specific fast path.
19/06/19 08:07:14 INFO manager.MySQLManager: Setting zero DATETIME behavior to convertToNull (mysql)
19/06/19 08:07:14 INFO mapreduce.ImportJobBase: Beginning import of authors
19/06/19 08:07:14 INFO Configuration.deprecation: mapred.jar is deprecated. Instead, use mapreduce.job.jar
19/06/19 08:07:15 INFO Configuration.deprecation: mapred.map.tasks is deprecated. Instead, use mapreduce.job.maps
19/06/19 08:07:15 INFO client.RMProxy: Connecting to ResourceManager at ts2.test.com/172.31.14.43:8032
19/06/19 08:07:16 INFO db.DBInputFormat: Using read commited transaction isolation
19/06/19 08:07:16 INFO db.DataDrivenDBInputFormat: BoundingValsQuery: SELECT MIN(`id`), MAX(`id`) FROM `authors`
19/06/19 08:07:16 INFO db.IntegerSplitter: Split size: 1; Num splits: 4 from: 1 to: 8
19/06/19 08:07:16 INFO mapreduce.JobSubmitter: number of splits:4
19/06/19 08:07:16 INFO mapreduce.JobSubmitter: Submitting tokens for job: job_1560926023741_0005
19/06/19 08:07:16 INFO impl.YarnClientImpl: Submitted application application_1560926023741_0005
19/06/19 08:07:16 INFO mapreduce.Job: The url to track the job: http://ts2.test.com:8088/proxy/application_1560926023741_0005/
19/06/19 08:07:16 INFO mapreduce.Job: Running job: job_1560926023741_0005
19/06/19 08:07:23 INFO mapreduce.Job: Job job_1560926023741_0005 running in uber mode : false
19/06/19 08:07:23 INFO mapreduce.Job:  map 0% reduce 0%
19/06/19 08:07:30 INFO mapreduce.Job:  map 100% reduce 0%
19/06/19 08:07:30 INFO mapreduce.Job: Job job_1560926023741_0005 completed successfully
19/06/19 08:07:30 INFO mapreduce.Job: Counters: 30
        File System Counters
                FILE: Number of bytes read=0
                FILE: Number of bytes written=701840
                FILE: Number of read operations=0
                FILE: Number of large read operations=0
                FILE: Number of write operations=0
                HDFS: Number of bytes read=393
                HDFS: Number of bytes written=603
                HDFS: Number of read operations=16
                HDFS: Number of large read operations=0
                HDFS: Number of write operations=8
        Job Counters
                Launched map tasks=4
                Other local map tasks=4
                Total time spent by all maps in occupied slots (ms)=17788
                Total time spent by all reduces in occupied slots (ms)=0
                Total time spent by all map tasks (ms)=17788
                Total vcore-milliseconds taken by all map tasks=17788
                Total megabyte-milliseconds taken by all map tasks=18214912
        Map-Reduce Framework
                Map input records=8
                Map output records=8
                Input split bytes=393
                Spilled Records=0
                Failed Shuffles=0
                Merged Map outputs=0
                GC time elapsed (ms)=298
                CPU time spent (ms)=4050
                Physical memory (bytes) snapshot=880451584
                Virtual memory (bytes) snapshot=11285938176
                Total committed heap usage (bytes)=878182400
        File Input Format Counters
                Bytes Read=0
        File Output Format Counters
                Bytes Written=603
19/06/19 08:07:30 INFO mapreduce.ImportJobBase: Transferred 603 bytes in 14.8375 seconds (40.6403 bytes/sec)
19/06/19 08:07:30 INFO mapreduce.ImportJobBase: Retrieved 8 records.
[centos@ts1 ~]$

[centos@ts1 ~]$ sqoop import --connect jdbc:mysql://172.31.7.255:3306/test --username training --password training --table posts --target-dir /user/posts
Warning: /opt/cloudera/parcels/CDH-5.15.2-1.cdh5.15.2.p0.3/bin/../lib/sqoop/../accumulo does not exist! Accumulo imports will fail.
Please set $ACCUMULO_HOME to the root of your Accumulo installation.
19/06/19 08:13:09 INFO sqoop.Sqoop: Running Sqoop version: 1.4.6-cdh5.15.2
19/06/19 08:13:09 WARN tool.BaseSqoopTool: Setting your password on the command-line is insecure. Consider using -P instead.
19/06/19 08:13:09 INFO manager.MySQLManager: Preparing to use a MySQL streaming resultset.
19/06/19 08:13:09 INFO tool.CodeGenTool: Beginning code generation
19/06/19 08:13:09 INFO manager.SqlManager: Executing SQL statement: SELECT t.* FROM `posts` AS t LIMIT 1
19/06/19 08:13:09 INFO manager.SqlManager: Executing SQL statement: SELECT t.* FROM `posts` AS t LIMIT 1
19/06/19 08:13:09 INFO orm.CompilationManager: HADOOP_MAPRED_HOME is /opt/cloudera/parcels/CDH-5.15.2-1.cdh5.15.2.p0.3/bin/../lib/sqoop/../hadoop-mapreduce
Note: /tmp/sqoop-centos/compile/0817ab08003547d8458a1646c5fd4916/posts.java uses or overrides a deprecated API.
Note: Recompile with -Xlint:deprecation for details.
19/06/19 08:13:10 INFO orm.CompilationManager: Writing jar file: /tmp/sqoop-centos/compile/0817ab08003547d8458a1646c5fd4916/posts.jar
19/06/19 08:13:10 WARN manager.MySQLManager: It looks like you are importing from mysql.
19/06/19 08:13:10 WARN manager.MySQLManager: This transfer can be faster! Use the --direct
19/06/19 08:13:10 WARN manager.MySQLManager: option to exercise a MySQL-specific fast path.
19/06/19 08:13:10 INFO manager.MySQLManager: Setting zero DATETIME behavior to convertToNull (mysql)
19/06/19 08:13:10 INFO mapreduce.ImportJobBase: Beginning import of posts
19/06/19 08:13:11 INFO Configuration.deprecation: mapred.jar is deprecated. Instead, use mapreduce.job.jar
19/06/19 08:13:11 INFO Configuration.deprecation: mapred.map.tasks is deprecated. Instead, use mapreduce.job.maps
19/06/19 08:13:11 INFO client.RMProxy: Connecting to ResourceManager at ts2.test.com/172.31.14.43:8032
19/06/19 08:13:13 INFO db.DBInputFormat: Using read commited transaction isolation
19/06/19 08:13:13 INFO db.DataDrivenDBInputFormat: BoundingValsQuery: SELECT MIN(`id`), MAX(`id`) FROM `posts`
19/06/19 08:13:13 INFO db.IntegerSplitter: Split size: 2; Num splits: 4 from: 1 to: 9
19/06/19 08:13:13 INFO mapreduce.JobSubmitter: number of splits:4
19/06/19 08:13:13 INFO mapreduce.JobSubmitter: Submitting tokens for job: job_1560926023741_0006
19/06/19 08:13:13 INFO impl.YarnClientImpl: Submitted application application_1560926023741_0006
19/06/19 08:13:13 INFO mapreduce.Job: The url to track the job: http://ts2.test.com:8088/proxy/application_1560926023741_0006/
19/06/19 08:13:13 INFO mapreduce.Job: Running job: job_1560926023741_0006
19/06/19 08:13:18 INFO mapreduce.Job: Job job_1560926023741_0006 running in uber mode : false
19/06/19 08:13:18 INFO mapreduce.Job:  map 0% reduce 0%
19/06/19 08:13:24 INFO mapreduce.Job:  map 100% reduce 0%
19/06/19 08:13:24 INFO mapreduce.Job: Job job_1560926023741_0006 completed successfully
19/06/19 08:13:24 INFO mapreduce.Job: Counters: 30
        File System Counters
                FILE: Number of bytes read=0
                FILE: Number of bytes written=701768
                FILE: Number of read operations=0
                FILE: Number of large read operations=0
                FILE: Number of write operations=0
                HDFS: Number of bytes read=393
                HDFS: Number of bytes written=3292
                HDFS: Number of read operations=16
                HDFS: Number of large read operations=0
                HDFS: Number of write operations=8
        Job Counters
                Launched map tasks=4
                Other local map tasks=4
                Total time spent by all maps in occupied slots (ms)=14536
                Total time spent by all reduces in occupied slots (ms)=0
                Total time spent by all map tasks (ms)=14536
                Total vcore-milliseconds taken by all map tasks=14536
                Total megabyte-milliseconds taken by all map tasks=14884864
        Map-Reduce Framework
                Map input records=9
                Map output records=9
                Input split bytes=393
                Spilled Records=0
                Failed Shuffles=0
                Merged Map outputs=0
                GC time elapsed (ms)=298
                CPU time spent (ms)=3850
                Physical memory (bytes) snapshot=823017472
                Virtual memory (bytes) snapshot=11286245376
                Total committed heap usage (bytes)=840957952
        File Input Format Counters
                Bytes Read=0
        File Output Format Counters
                Bytes Written=3292
19/06/19 08:13:24 INFO mapreduce.ImportJobBase: Transferred 3.2148 KB in 12.8976 seconds (255.2419 bytes/sec)
19/06/19 08:13:24 INFO mapreduce.ImportJobBase: Retrieved 9 records.


create external table authors (
id int,
first_name string,
last_name string,
email string,
birthdate string,
added string
)
row format delimited
fields terminated by ','
location 'hdfs://ts1.test.com:8020/user/authors'
;

create table posts (
id int,
author_id int,
title string,
description string,
content string,
date string
)
row format delimited
fields terminated by ','
location 'hdfs://ts1.test.com:8020/user/posts'
;

</code></pre>


## 5.
<pre><code>
[centos@ts1 ~]$ mysql -u training -p
Enter password:
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 919
Server version: 5.5.60-MariaDB MariaDB Server

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]> use test;
Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A

Database changed
MariaDB [test]> cREATE TABLE `results` (
    -> `id` int(10) NOT NULL AUTO_INCREMENT,
    -> `first_name` varchar(100) COLLATE utf8_unicode_ci NOT NULL,
    -> `last_name` varchar(100) COLLATE utf8_unicode_ci NOT NULL,
    -> `num_posts` int(10)  NOT NULL,
    ->  PRIMARY KEY (`id`)
    ->  )
    -> ;
Query OK, 0 rows affected (0.00 sec)

MariaDB [test]>
</code></pre>
