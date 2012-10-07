---
layout: post
title: "memcache_install_guide"
date: 2012-09-24 02:57
comments: true
categories: [memcache, php, linux]
---

memcache vs memcached

memcache memcached 都有 deamon 和 PHP Extension

memcached 比較新，功能多


memcache Extension 安裝方式
	$ wget http://pecl.php.net/get/memcache-2.2.4.tgz
	$ tar -zxvf memcached-2.2.4.tgz
	$ cd memcached-2.2.4
	$ phpize && ./configure --enable-memcache && make
	$ cp modules/memcache.so /usr/lib/php/modules/

	$ vi /etc/php.ini

關於 extension 的附近會看到下方的說明，這是新版的 php 已經改成如此 ( linux )

*Note: packaged extension modules are now loaded via the .ini files*
*found in the directory /etc/php.d*

	$ touch /etc/php.d/memcache.ini
*$ echo 'extension=memcache.so' > /etc/php.d/memcache.ini 如果不自行編 memcache.ini 的情況下，此行可以忽略*

	$ vi /etc/php.d/memcache.ini

貼上下方設定，主要是 *extension=memcache.so* 這行其他都是註解，方便以後修改。

	; Enable memcache extension module
	extension=memcache.so

	; Options for the memcache module

	; Whether to transparently failover to other servers on errors
	;memcache.allow_failover=1
	; Defines how many servers to try when setting and getting data.
	;memcache.max_failover_attempts=20
	; Data will be transferred in chunks of this size
	;memcache.chunk_size=8192
	; The default TCP port number to use when connecting to the memcached server
	;memcache.default_port=11211
	; Hash function {crc32, fnv}
	;memcache.hash_function=crc32
	; Hash strategy {standard, consistent}
	;memcache.hash_strategy=standard

	; Options to use the memcache session handler

	; Use memcache as a session handler
	;session.save_handler=memcache
	; Defines a comma separated of server urls to use for session storage
	;session.save_path="tcp://localhost:11211?persistent=1&weight=1&timeout=1&retry_interval=15"
	
最後當然一定要
	
	$ service httpd restart


