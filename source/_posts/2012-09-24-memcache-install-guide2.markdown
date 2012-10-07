---
layout: post
title: "memcache 安裝紀錄 deamon"
date: 2012-09-24 02:57
comments: true
categories: [memcache, php, linux]
---

memcache vs memcached

memcache memcached 都有 deamon 和 PHP Extension

memcached 比較新，功能多

	
Memcached Server install guide

	$ yum install libevent 				
* 會出錯 [http://www.wangshun.org/?p=416](http://www.wangshun.org/?p=416) 所以不行!! 需要全部手動安裝 *

確認一下安裝環境，相關參考官方網站[http://memcached.org/](http://memcached.org/)
	$ uname -a							
	Linux localhost.localdomain 2.6.18-128.el5 #1 SMP Wed Jan 21 10:44:23 EST 2009 i686 i686 i386 GNU/Linux

	$ wget http://memcached.googlecode.com/files/memcached-1.4.10.tar.gz 	
	$ tar zxvf memcached-1.4.10.tar.gz 
	$ cd memcached-1.4.10
	$ ./configure
	# checking build system type... i686-pc-linux-gnu
	# checking host system type... i686-pc-linux-gnu
	# checking target system type... i686-pc-linux-gnu
	# checking for a BSD-compatible install... /usr/bin/install -c
	# checking whether build environment is sane... yes
	# checking for a thread-safe mkdir -p... /bin/mkdir -p
	# checking for gawk... gawk
	# checking whether make sets $(MAKE)... yes
	# checking for gcc... gcc
	# checking whether the C compiler works... yes
	# checking for C compiler default output file name... a.out
	# checking for suffix of executables... 
	# checking whether we are cross compiling... no
	# checking for suffix of object files... o
	# checking whether we are using the GNU C compiler... yes
	# checking whether gcc accepts -g... yes
	# checking for gcc option to accept ISO C89... none needed
	# checking for style of include used by make... GNU
	# checking dependency style of gcc... gcc3
	# checking how to run the C preprocessor... gcc -E
	# checking for grep that handles long lines and -e... /bin/grep
	# checking for egrep... /bin/grep -E
	# checking for icc in use... no
	# checking for ANSI C header files... yes
	# checking for sys/types.h... yes
	# checking for sys/stat.h... yes
	# checking for stdlib.h... yes
	# checking for string.h... yes
	# checking for memory.h... yes
	# checking for strings.h... yes
	# checking for inttypes.h... yes
	# checking for stdint.h... yes
	# checking for unistd.h... yes
	# checking whether __SUNPRO_C is declared... no
	# checking for gcc option to accept ISO C99... -std=gnu99
	# checking whether gcc -std=gnu99 and cc understand -c and -o together... yes
	# checking sasl/sasl.h usability... no
	# checking sasl/sasl.h presence... no
	# checking for sasl/sasl.h... no
	# checking for gcov... /usr/bin/gcov
	# checking for main in -lgcov... yes
	# checking for library containing clock_gettime... -lrt
	# checking for library containing socket... none required
	# checking for library containing gethostbyname... none required
	# checking for libevent directory... configure: error: libevent is required.  You can get it from http://www.monkey.org/~provos/libevent/

	# If it's already installed, specify its path using --with-libevent=/dir/

上面叭啦叭啦一堆，跟你說 libevent 沒有! 硍! yum install libevent 沒屁用!
直接從訊息說的網址抓 [http://www.monkey.org/~provos/libevent/](http://www.monkey.org/~provos/libevent/)

相關參考 官網 : [http://www.monkey.org/~provos/libevent/](http://www.monkey.org/~provos/libevent/)
	$ cd ..
	$ wget https://github.com/downloads/libevent/libevent/libevent-2.0.16-stable.tar.gz
	$ ./configure --prefix=/usr
	$ make
	$ make install
				
然後出現下面的安裝完畢說明

	Libraries have been installed in:
	   /usr/lib

	If you ever happen to want to link against installed libraries
	in a given directory, LIBDIR, you must either use libtool, and
	specify the full pathname of the library, or use the `-LLIBDIR'
	flag during linking and do at least one of the following:
	   - add LIBDIR to the `LD_LIBRARY_PATH' environment variable
		 during execution
	   - add LIBDIR to the `LD_RUN_PATH' environment variable
		 during linking
	   - use the `-Wl,-rpath -Wl,LIBDIR' linker flag
	   - have your system administrator add LIBDIR to `/etc/ld.so.conf'

	See any operating system documentation about shared libraries for
	more information, such as the ld(1) and ld.so(8) manual pages.
	----------------------------------------------------------------------
	
最後當然要檢查一下裝到了沒

	$ ls -al /usr/lib | grep libevent
		
		# lrwxrwxrwx   1 root root       21 Nov 26 00:38 libevent-2.0.so.5 -> libevent-2.0.so.5.1.4
		# -rwxr-xr-x   1 root root   762242 Nov 26 00:38 libevent-2.0.so.5.1.4
		# -rw-r--r--   1 root root   990968 Nov 26 00:38 libevent.a
		# lrwxrwxrwx   1 root root       26 Nov 26 00:38 libevent_core-2.0.so.5 -> libevent_core-2.0.so.5.1.4
		# -rwxr-xr-x   1 root root   453822 Nov 26 00:38 libevent_core-2.0.so.5.1.4
		# -rw-r--r--   1 root root   607858 Nov 26 00:38 libevent_core.a
		# -rwxr-xr-x   1 root root      968 Nov 26 00:38 libevent_core.la
		# lrwxrwxrwx   1 root root       26 Nov 26 00:38 libevent_core.so -> libevent_core-2.0.so.5.1.4
		# lrwxrwxrwx   1 root root       27 Nov 26 00:38 libevent_extra-2.0.so.5 -> libevent_extra-2.0.so.5.1.4
		# -rwxr-xr-x   1 root root   322768 Nov 26 00:38 libevent_extra-2.0.so.5.1.4
		# -rw-r--r--   1 root root   383182 Nov 26 00:38 libevent_extra.a
		# -rwxr-xr-x   1 root root      975 Nov 26 00:38 libevent_extra.la
		# lrwxrwxrwx   1 root root       27 Nov 26 00:38 libevent_extra.so -> libevent_extra-2.0.so.5.1.4
		# -rwxr-xr-x   1 root root      933 Nov 26 00:38 libevent.la
		# lrwxrwxrwx   1 root root       29 Nov 26 00:38 libevent_openssl-2.0.so.5 -> libevent_openssl-2.0.so.5.1.4
		# -rwxr-xr-x   1 root root    70919 Nov 26 00:38 libevent_openssl-2.0.so.5.1.4
		# -rw-r--r--   1 root root    79220 Nov 26 00:38 libevent_openssl.a
		# -rwxr-xr-x   1 root root     1004 Nov 26 00:38 libevent_openssl.la
		# lrwxrwxrwx   1 root root       29 Nov 26 00:38 libevent_openssl.so -> libevent_openssl-2.0.so.5.1.4
		# lrwxrwxrwx   1 root root       30 Nov 26 00:38 libevent_pthreads-2.0.so.5 -> libevent_pthreads-2.0.so.5.1.4
		# -rwxr-xr-x   1 root root    14289 Nov 26 00:38 libevent_pthreads-2.0.so.5.1.4
		# -rw-r--r--   1 root root    11814 Nov 26 00:38 libevent_pthreads.a
		# -rwxr-xr-x   1 root root      996 Nov 26 00:38 libevent_pthreads.la
		# lrwxrwxrwx   1 root root       30 Nov 26 00:38 libevent_pthreads.so -> libevent_pthreads-2.0.so.5.1.4
		# lrwxrwxrwx   1 root root       21 Nov 26 00:38 libevent.so -> libevent-2.0.so.5.1.4
	
	
切換到 memcached 資料夾，繼續之前的步驟

	$ cd memcached-1.4.10					
	$ ./configure 							// 一樣一堆checking for XXXX 之後，沒有錯誤啦!!
	$ make
	$ make install
	$ ls -al /usr/local/bin/mem* 			// 檢查一下裝到了沒

	$ /usr/local/bin/memcached -d -m 10 -u root -l 172.16.1.46 -p 11211 		
		-- another way
		-- $ /usr/local/bin/memcached -d -m 10 -u root -l 192.168.0.200 -p 12000 -c 256 -P /tmp/memcached.pid
		-- -d 背景服務
		-- -m 是分配 Memcache 使用的記憶體容量，單位是MB
		-- -u 
		-- -l 是設定 Memcached 監聽的 ip 位置
		-- -p 是設定 Memcached 監聽的 port
		-- -c 是最大同時進行的連接數量，預設是1024
		-- -P 
																					
																					
另外的安裝方式，超爽的方式，怎麼 CentOS 5.3 沒有
[http://www.webdeveloperjuice.com/2010/01/25/10-baby-steps-to-install-memcached-server-and-access-it-with-php/](http://www.webdeveloperjuice.com/2010/01/25/10-baby-steps-to-install-memcached-server-and-access-it-with-php/)

Step1: Install libevent ,libmemcached and libmemcached devel (dependency)
	$ yum install libevent
	$ yum install libmemcached libmemcached-devel

Step 2: Install Memcached Server
	$ yum install memcached

Step 3: Start Memcached server
	$ memcached -d -m 512 -l 127.0.0.1 -p 11211 -u nobody
*d = daemon, m = memory\(MB\), u = user, l = IP to listen to, p = port*

Step 4: Check your memcached server is running successfully
	$ ps -eaf | grep memcached

Step 5: Connect Memcached server via telnet
	$ telnet 127.0.0.1 11211

Step 6: Check current status of Memcached Server on telnet prompt
	$ stats

Step 7: Exit telnet
	$ quit

Step 8: Install PHP client to access Memcached Server
	$ pecl install memcache

It will make “memcache.so”, you have to just put it on your /etc/php.ini file.

Step 9: Restart your apache server
	$ service httpd restart


最後PHP memcache 程式碼範例
	[http://www.php.net/manual/en/memcache.set.php](http://www.php.net/manual/en/memcache.set.php)


最後相關參考

http://www.webdeveloperjuice.com/2010/01/25/10-baby-steps-to-install-memcached-server-and-access-it-with-php/
http://www.ccvita.com/257.html 
http://lwfirst.blogspot.com/2011/02/php-memcache.html
