# PM2 教學

## Install 
```
npm install pm2 -g
```
## 運行教學

### Start
1. 基本啟動
```
pm2 start xxx.js
```
2. 啟動服務與命名服務，並格式化log
```
pm2 start xxxx.js --name you_service_name --log-date-format 'DD-MM HH:mm:ss.SSS'
```
3. 啟動服務與命名服務，並格式化log以及cluster service (cluster 4個)
```
pm2 start xxxx.js -i 4 --name you_service_name --log-date-format 'DD-MM HH:mm:ss.SSS'
```
### Restart
```
pm2 restart you_service_name
```
### Stop
```
pm2 stop you_service_name
```
### Delete
```
pm2 delete you_service_name
```
## 監控

### 查詢運行中服務
1.  
```
pm2 list
```
2. 
```
pm2 ps
```
3. 
```
pm2 status
```
### 監控
#### 查看log
```
pm2 log
```
#### 監控server運行狀態
```
pm2 monit
```

### 開機自動啟動服務
1. 啟動服務
```
pm2 start xxxx.js --name you_service_name --log-date-format 'DD-MM HH:mm:ss.SSS'
```
2.儲存服務狀態
```
pm2 save
```
3.設定開機啟動
```
pm2 startup
```
並複製顯示出來的指令如(**下方指令只是的範例 請勿複製**)
```
sudo env PATH=$PATH:/home/ubuntu/.nvm/versions/node/v8.11.1/bin /home/ubuntu/.nvm/versions/node/v8.11.1/lib/node_modules/pm2/bin/pm2 startup
```
4.重新開機，等待三分鐘後服務就啟動了
 


###### tags: `NodeJS`、`Server`