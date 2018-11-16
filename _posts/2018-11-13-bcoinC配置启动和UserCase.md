---
layout:     post
title:      bcoin配置及启动项
subtitle:   javascript
date:       2018-11-05
author:     Jang
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
    - Javascript
    - BlockChain
---

# 启动项
```
bcoin --network=testnet 
      --http-host=0.0.0.0 
      --http-port=xxxx 
      --api-key=xxxx 
      --wallet-http-host=0.0.0.0 
      --wallet-http-port=xxxx 
      --wallet-api-key=xxxx 
      --daemon
```

# User Case
## 1. 获取node信息
```
curl http://x:xxx@ip:port/
```

```
curl http://x:xxx@ip:port/wallet/
```

# User Case
## 1. Create Wallet -> Create Account -> Geneate Address(?)
```
id='newWallet'
passphrase='secret456'
witness=false
watchOnly=true
accountKey='rpubKBAoFrCN1HzSEDye7jcQaycA8L7MjFGmJD1uuvUZ21d9srAmAxmB7o1tCZRyXmTRuy5ZDQDV6uxtcxfHAadNFtdK7J6RV9QTcHTCEoY5FtQD'

curl $walleturl/$id \
  -X PUT \
  --data '{"witness":'$witness', "passphrase":"'$passphrase'", "watchOnly": '$watchOnly', "accountKey":"'$accountKey'"}'
```

```
id='primary'
passphrase='secret123'
name='menace'
type='multisig'
curl $walleturl/$id/account/$name \
    -X PUT \
    --data '{"type": "'$type'", "passphrase": "'$passphrase'"}'
```

```
id="primary"
account="default"
curl $walleturl/$id/address -X POST --data '{"account":"'$account'"}'
```
## 2. Send btcoin from A to B
```
id="primary"
passphrase="secret123"
rate=1000
value=20000
address="RPipJ9yeeQxHn6YcBXd9WPy2V6cezzAuY8"

curl $walleturl/$id/send \
  -X POST \
  --data '{
    "passphrase":"'$passphrase'",
    "rate":'$rate',
    "outputs":[
      {"address":"'$address'", "value":'$value'}
    ]
  }'
```
## 3. Delete Account

## 4. Delete Wallet

## 5. Query Balance, etc
```
id='primary'
account='default'
curl $walleturl/$id/balance?account=$account
```
## 6. Get Wallet account info(include address info)
```
id='primary'
account='default'
curl $walleturl/$id/account/$account
```
