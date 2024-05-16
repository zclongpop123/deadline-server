- 生成CA私钥
```bash
openssl genrsa -aes256 -out ca.key 2048
```
- 自签发CA证书
```bash
openssl req -new -x509 -days 3650 -sha256 -subj "/C=CN/ST=BJ/O=Mongo/OU=CA/CN=Mongo/emailAddress=ca@mongo.com" -key ca.key -out ca.crt
```
- 生成服务端私钥
```bash
openssl genrsa -out server.key 2048
```
- 生成服务端签名请求
```bash
openssl req -new -subj "/C=CN/ST=BJ/O=Mongo/OU=Server/CN=Mongo/emailAddress=server@mongo.com" -key server.key -out server.csr
```
- 签发服务端证书
```bash
openssl x509 -req -in server.csr -CA ca.crt -CAkey ca.key -set_serial 01 -out server.crt -days 3650
```
- 合并服务端证书和私钥
```bash
cat server.crt server.key > server.pem
```
- 生成客户端私钥
```bash
openssl genrsa -out client.key 2048
```
- 生成客户端证书签名请求
```bash
openssl req -new -subj  "/C=CN/ST=BJ/O=Mongo/OU=Client/CN=Mongo/emailAddress=client@mongo.com" -key client.key -out client.csr
```
- 签发客户端证书
```bash
openssl x509 -req -in client.csr -CA ca.crt -CAkey ca.key -set_serial 01 -out client.crt -days 3650
```
- 合并客户端证书和私钥
```bash
cat client.crt client.key > client.pem
```
- 打包pfx证书
```bash
openssl pkcs12 -export -inkey client.key -in client.crt -certfile ca.crt -out client.pfx
```
