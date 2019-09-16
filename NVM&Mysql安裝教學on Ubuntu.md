# NVM&Mysql安裝教學on Ubuntu

## NVM安裝

**更新ubuntu apt**
```
$ sudo apt-get update
```


**安裝NVM所需元件**

```
$ sudo apt-get install build-essential libssl-dev
```

**安裝NVM**

透過cURL
```
$ sudo curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.11/install.sh | bash
```
或者透過Wget
```
$ sudo wget -qO- https://raw.githubusercontent.com/creationix/nvm/v0.33.11/install.sh | bash
```
以上請依照個人喜好選擇

**修改bashrc**
此步驟目的是讓NVM指令可直接被呼叫
```
$ vim ~/.bashrc
```
移動到最下方貼入以下內容
```
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh" # This loads nvm
```
輸入:wq 存檔輸入
```
source ~/.bashrc
```
測試一下
```
nvm --version
```
**透過Nvm安裝NodeJS**

```
$ nvm install your_nodeJS_version 
```
實際安裝nodeJS v8.11.4
```
$ nvm install v8.11.4
```
安裝完畢 輸入下方指令驗證安裝完成
```
node -v  
```

其餘使用教學請參考 [NVM](https://github.com/creationix/nvm)

## 安裝Mysql
輸入下方指令，並依照後續操作輸入密碼
```
$ sudo apt-get install mysql-server
```

**登入Mysql** 
```
$ mysql -u root -p
```

**Mysql設定檔案位置**
/etc/mysql/my.cnf


**為使用者增加權限**
使用者權限變更
(1)新增帳號，並給予全部權限
mysql> GRANT ALL PRIVILEGES ON *.* TO user@host IDENTIFIED BY '密碼';
說明：將全部權限都設給從host連線上來的user這個人，並給定密碼為密碼。

(2)新增帳號，並指定某資料庫與特定權限給該帳號
mysql> GRANT SELECT,INSERT,UPDATE ON 資料庫名.* TO user@host IDENTIFIED BY '密碼';
說明：開放某資料庫給從host連線上來的user這個人，並給定密碼為密碼。 

* 若權限有變動記得執行此指令:FLUSH PRIVILEGES



## 安裝Mysql use docker
```
docker run --name my-mysql -e MYSQL_ROOT_PASSWORD=YOU_PASSWORD -d -p you_export_port:3306 mysql: 5.7.26
```