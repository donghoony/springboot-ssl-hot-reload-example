see [reference](https://spring.io/blog/2023/11/07/ssl-hot-reload-in-spring-boot-3-2-0)

```
mkdir certs & cd certs
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
2024-08-14T16:51:35.018+09:00  INFO 45591 --- [-bundle-watcher] o.a.t.util.net.NioEndpoint.certificate :
Connector [https-jsse-nio-8443], TLS virtual host [_default_],
certificate type [UNDEFINED] configured from keystore [/Users/donghoony/.keystore]
using alias [tomcat] with trust store [null]
```

to check the certificate has changed, use command below:
```
curl -v --insecure https://localhost:8443/ping
```

see `Server certificate` field:
```
* Server certificate:
*  subject: CN=example-cert-1
*  start date: Aug 14 07:49:25 2024 GMT
*  expire date: Aug 14 07:49:25 2025 GMT
*  issuer: CN=example-cert-1
```

after overwritting certificates:
```
* Server certificate:
*  subject: CN=example-cert-2
*  start date: Aug 14 07:51:23 2024 GMT
*  expire date: Aug 14 07:51:23 2025 GMT
*  issuer: CN=example-cert-2
```
