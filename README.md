see [reference](https://spring.io/blog/2023/11/07/ssl-hot-reload-in-spring-boot-3-2-0)

```
openssl req -x509 -subj "/CN=example-cert-1" \
-keyout example.key -out example.crt -days 365 -sha512 -nodes -newkey rsa
```

swap cert using command below (overwrites existing files, see `-subj`)

```
openssl req -x509 -subj "/CN=example-cert-2" \
-keyout example.key -out example.crt -days 365 -sha512 -nodes -newkey rsa
```

Application log below:
```
2024-08-14T16:51:35.018+09:00  INFO 45591 --- [-bundle-watcher] o.a.t.util.net.NioEndpoint.certificate   :
Connector [https-jsse-nio-8443], TLS virtual host [_default_],
certificate type [UNDEFINED] configured from keystore [/Users/donghoony/.keystore]
using alias [tomcat] with trust store [null]
```
