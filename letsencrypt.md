# Lets Encrypt 透過 DNS 驗證

更新套件

```sh
sudo apt update
```

安裝軟體屬性套件，Certbot 使用 PPA 分發 Certbot，此套件可以讓PPA 更有效率

```sh
sudo apt install software-properties-common
```

更新 apt 儲存庫

```sh
sudo apt update -y
```

安裝 certbot

```sh
sudo apt install certbot -y
```

設定環境變數方便後續使用

```sh
DOMAIN=example.com
WILDCARD=*.$DOMAIN
```

測試變數是否正確

```sh
echo $DOMAIN && echo $WILDCARD
```

使用 certbot 手動授權搭配DNS查問驗證所有權

```sh
sudo certbot -d $DOMAIN -d $WILDCARD --manual --preferred-challenges dns certonly
```

接下來會提示輸入 email，這會用於續約跟安全性注意事項

最後 Lets Encrypt 會提供一至兩組字串用於確認 domain 所有權，請至網域提供商DNS設定對應的 TXT Record

設定完成後，請在回報Lets Encrypt 之前使用 TXTLookup 確認TXT Record 是否正確生效

回報後驗證完成，Lets Encrypt 訊息會提示憑證．金鑰放在哪，應類似/etc/letsencrypt/live/example.com/底下
