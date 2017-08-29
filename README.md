# 如何利用SSL FOR FREE架設HTTPS在XAMPP上

### 事前須知

> [XAMPP官網](https://www.apachefriends.org/zh_tw/index.html)

> [SSL For Free官網](https://github.com/hauserJr/PuseServer)

### 注意事項
> 確認主機防火牆有開啟443 port，且並無被占用狀況。
 
> 驗證SSL時請確認檔案路徑名稱都是正確的，否則將無法驗證成功。
 
> NO-IP所提供的DDNS並無法利用此方法取得SSL <font size="1">~~相信我 我跌過坑~~<font size="1">

>要驗證SSL是否有成功架設請輸入正確的網址。

>SSL For Free是有時效的，如要長期使用請以三個月為一周期重新申請SSL憑證。
            
            注意：請勿輸入https://localhost 或 https://127.0.0.1來驗證
            如果需要使用本地來驗證，請自行修改apache的httpd-vhosts.conf及httpd-ssl.conf


### SSL安裝步驟
1. 請先下載XAMPP並確認Apache可正常啟用。

2. 進入SSL For Free官網輸入你要設定SSL的網址。
    > 按下 `Create Free SSL Certificate` 會產生下圖資訊
    
    > 並依照順序點擊圖片中的步驟1跟2。
    > 點擊完後會產生編號3的檔案,下載後解壓縮並放到官方指定的路徑。
    	`http://your-Url/.well-known/acme-challenge/your-download-file-name`
    > 點擊步驟4的網址可驗證檔案是否有存在路徑內。
     
    > 驗證成功後可下載檔案，檔案內有三個檔案分別為。
    
        1.ca_bundle.crt   `存放路徑為：xampp/apache/conf.ssl.crt`
	
        2.certificate.crt `存放路徑為：xampp/apache/conf.ssl.crt`
	
        3.private.key     `存放路徑為：xampp/apache/conf.ssl.key`

    
### 放置完成後修改Apache的httpd-vhosts.conf及httpd-ssl.conf
#### httpd-vhosts.conf加入
``` conf
NameVirtualHost *:443
# https
<VirtualHost *:443>
    DocumentRoot "E:/xampp/htdocs/Your-Web-Folder"
    ServerName pwa-test.asuscomm.com
	
    SSLEngine on
    SSLCertificateFile "E:/your-file-path/ssl.crt/certificate.crt"
    SSLCertificateKeyFile "E:/your-file-path/ssl.key/private.key"
    SSLCertificateChainFile "E:/your-file-path/ca_bundle.crt"
    <Directory "E:/xampp/htdocs/Your-Web-Folder">
        Options All
    	AllowOverride All
    	Require all granted
    </Directory>
</VirtualHost>
```

#### httpd-ssl.conf加入
``` conf
NameVirtualHost *:443
<VirtualHost *:443>
    DocumentRoot "E:/xampp/htdocs/Your-Web-Folder"
    ServerName pwa-test.asuscomm.com
	
    SSLEngine on
    SSLCertificateFile "your-file-path/certificate.crt"
    SSLCertificateKeyFile "your-file-path/private.key"
    SSLCertificateChainFile "your-file-path/ca_bundle.crt"
</VirtualHost>    
```





