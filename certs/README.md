```bash
openssl genrsa -aes256 -out ca.key 2048
```
```bash
openssl req -new -x509 -days 3650 -sha256 -subj "/C=CN/ST=BJ/O=Mongo/OU=CA/CN=Mongo/emailAddress=ca@mongo.com" -key ca.key -out ca.crt
```
```bash
openssl genrsa -out server.key 2048
```
```bash
openssl req -new -subj "/C=CN/ST=BJ/O=Mongo/OU=Server/CN=Mongo/emailAddress=server@mongo.com" -key server.key -out server.csr
```
```bash
openssl x509 -req -in server.csr -CA ca.crt -CAkey ca.key -set_serial 01 -out server.crt -days 3650
```
