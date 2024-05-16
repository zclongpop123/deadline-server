## Deadline Server With Standalone Mongo

 - Hierarchy
```
mongo
    ├── mongod.conf
    ├── certs
    ├── data
    └── logs
```
- 查询Deadline证书的subject
```bash
openssl x509 -in client.pem -subject -nameopt RFC2253 | head -n 1
```
- 添加Deadline数据库账户
```bash
use $external
```
```bash
db.createUser(
    {
      user: "emailAddress=client@mongo.com,CN=Mongo,OU=Client,O=Mongo,ST=BJ,C=CN",
      roles: [
         { role: "readWrite", db: "deadline10db" }
      ]
    }
)
```
