```bash
openssl genrsa -aes256 -out ca.key 2048
```
```bash
openssl req -new -x509 -days 3650 -sha256 -subj "/C=CN/ST=BJ/O=Mongo/OU=CA/CN=Mongo/emailAddress=ca@mongo.com" -key ca.key -out ca.crt
```
