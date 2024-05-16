## Deadline Server With Standalone Mongo

 - Hierarchy
```
mongo
    ├── mongod.conf
    ├── certs
    ├── data
    └── logs
```
- 添加客户端用户
```bash
use $external
```
```bash
openssl x509 -in client.pem -inform PEM -subject -nameopt RFC2253
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
