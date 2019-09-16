# MongoDB

## Windows

### 安裝
到該[下載連結](https://www.mongodb.com/download-center/v2/community)選擇版本下載msi安裝

## Ubuntu

### 安裝
請依據安裝文件及ubuntu系統版本 進行安裝
[安裝文件](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-ubuntu/)

## Docker
```
docker run -d -p you_ip:export_port:27017 --name mongodb \
    -e MONGO_INITDB_ROOT_USERNAME=you_user_name \
    -e MONGO_INITDB_ROOT_PASSWORD=you_user_password \
    mongo:3.6.12
```

## 安全性教學

### 開啟帳號密碼登入(建立這步驟之前請先參考CreateUser)

修改mongod.conf文件，找到security，新增 authorization: enabled，並重新啟動mongoDB即可。
請參考note


### User&Role


#### CreateUser
```
$ use admin
$ db.createUser(
    {
        user: "YOURUSERNAME",
        pwd: "YOURPASSWORD",
        roles: [{ role: "root", db: "admin" }] //role請看下方說明
    })
```
#### Role
SuperUser
roles: [ { role: "userAdminAnyDatabase", db: "admin" } ]
該權限設定之後，理論上應該是可以存取任何DB的權限，但實際會發現，要做任何事情都會說權限不足，
需要特別登入SuperUser，這樣在co。de端，使用該User太過危險，所以依據需要再將各DB權限，加入到role中。

```
readAnyDatabase > 讀取所有資料庫

readWriteAnyDatabase > 讀寫所有資料庫

userAdminAnyDatabase > 管理所有資料庫使用者

dbAdminAnyDatabase > 所有資料庫的管理者

root > 最高權限,看文件應該是有用
```
[詳細參考](https://docs.mongodb.com/manual/reference/built-in-roles/index.html)


### 設定檔 
設定檔案範例(linux 檔名為mongod.conf,windows 檔名為mongod.cfg)
路徑、Port、IP等等，請依據需求與OS不同進行更改

#### Windows版本
```
# mongod.cfg

# for documentation of all options, see:
#   http://docs.mongodb.org/manual/reference/configuration-options/

# Where and how to store data.
storage:
  dbPath: "D:\\MongoDB\\data\\db"
  journal:
    enabled: true
#  engine:
#  mmapv1:
#  wiredTiger:

# where to write logging data.
systemLog:
  destination: file
  logAppend: true
  path: "D:\\MongoDB\\log\\mongod.log"

# network interfaces
net:
  port: 27017
  bindIp: 127.0.0.1


# how the process runs

security:
  authorization: enabled

#operationProfiling:

#replication:

#sharding:

## Enterprise-Only Options:

#auditLog:

#snmp:
```

#### Linux版本(ubuntu)
```
# mongod.conf

# for documentation of all options, see:
#   http://docs.mongodb.org/manual/reference/configuration-options/

# Where and how to store data.
storage:
  dbPath: /var/lib/mongodb
  journal:
    enabled: true
#  engine:
#  mmapv1:
#  wiredTiger:

# where to write logging data.
systemLog:
  destination: file
  logAppend: true
  path: /var/log/mongodb/mongod.log

# network interfaces
net:
  port: 27017
  bindIp: 127.0.0.1


# how the process runs
processManagement:
  timeZoneInfo: /usr/share/zoneinfo

security:
  authorization: enabled
#operationProfiling:

#replication:

#sharding:

## Enterprise-Only Options:

#auditLog:

#snmp:
```