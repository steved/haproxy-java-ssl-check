This is an example of how TLS checks from HAProxy to Java are broken.

Run:

```
MAVEN_OPTS="-Djavax.net.debug=all" mvn clean compile exec:java
```

and
```
haproxy -f ./haproxy.cfg
```

You should see:
```
qtp1952751122-12, fatal error: 80: Inbound closed before receiving peer's close_notify: possible truncation attack?
javax.net.ssl.SSLException: Inbound closed before receiving peer's close_notify: possible truncation attack?
%% Invalidated:  [Session-2, TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384]
```

Versions:

```
$ mvn -v
Apache Maven 3.3.9 (bb52d8502b132ec0a5a3f4c09453c07478323dc5; 2015-11-10T08:41:47-08:00)
Maven home: /usr/local/Cellar/maven/3.3.9/libexec
Java version: 1.8.0_92, vendor: Oracle Corporation
Java home: /Library/Java/JavaVirtualMachines/jdk1.8.0_92.jdk/Contents/Home/jre
Default locale: en_US, platform encoding: UTF-8
OS name: "mac os x", version: "10.12.3", arch: "x86_64", family: "mac"
$ haproxy -vvv
HA-Proxy version 1.8-dev0-f6b37c-194 2017/03/07
Copyright 2000-2016 Willy Tarreau <willy@haproxy.org>

Build options :
  TARGET  = generic
  CPU     = generic
  CC      = gcc
  CFLAGS  = -O0 -g -fno-strict-aliasing -Wdeclaration-after-statement
  OPTIONS = USE_KQUEUE=1 USE_OPENSSL=1

Default settings :
  maxconn = 2000, bufsize = 16384, maxrewrite = 1024, maxpollevents = 200

Built with OpenSSL version : OpenSSL 1.0.2k  26 Jan 2017
Running on OpenSSL version : OpenSSL 1.0.2k  26 Jan 2017
OpenSSL library supports TLS extensions : yes
OpenSSL library supports SNI : yes
Built with transparent proxy support using:
Built with network namespace support.
Built without compression support (neither USE_ZLIB nor USE_SLZ are set).
Compression algorithms supported : identity("identity")
Encrypted password support via crypt(3): yes
Built without PCRE or PCRE2 support (using libc's regex instead)

Available polling systems :
     kqueue : pref=300,  test result OK
       poll : pref=200,  test result OK
     select : pref=150,  test result OK
Total: 3 (3 usable), will use kqueue.

Available filters :
	[SPOE] spoe
	[COMP] compression
	[TRACE] trace
```
