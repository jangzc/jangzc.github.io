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

# 测试
```
curl http://x:xxx@ip:port/
```

```
curl http://x:xxx@ip:port/wallet/
```

# User Case
## 1. Create Wallet -> Create Account -> Geneate Address(?)

## 2. Send btcoin from A to B

## 3. Delete Account

## 4. Delete Wallet

## 5. Query Balance, etc
