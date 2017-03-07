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
