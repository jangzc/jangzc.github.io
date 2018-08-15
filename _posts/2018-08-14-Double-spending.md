---
layout:     post
title:      Double-Spending
subtitle:   比特币要解决的问题
date:       2018-08-14
author:     Jang
header-img: img/post-bg-debug.png
catalog: true
tags:
    - BlockChain
---

来自Wiki

# 双重支付<br>
双重支付(又称一币多付、双花攻击、double-spending)是一种数字货币失败模式的构想，即同一个数字token可以被花用两次以上。不像具有实体的符号货币如硬币，电子文件可以被复制，所以花用这个行为并不会从原持有者身上移除拥有的状态，也就是"创建"已支付单未移除的货币，加上属于收款者的已支付的同金额货币，或是使收款者凭空多出多重支付的金额，犹如伪钞般，造成通过膨胀而导致货币贬值，从而不再让人信任并愿意持有及流通。防止双重支付需要其他的措施。<br>

## 受信任的第三方<br>
通常由线上受信任的第三方来验证一个数字token是否被花用过，这在信任和信息安全的角度看都是单点脆弱性.

## 去中心化<br>
在2007年，数个分布式的双重支付防范方法被提出<br>
于2009年开始运作的加密货币比特币使用了工作量证明来避免受信任第三方的需求。交易被记录于公开的区块链上，防止任何人双重支付，除非企图攻击者能控制全网络超过50%的运算能力<br>
在2018年5月，有恶意矿工通过至少51%的全网算力，对当时的全球第26大加密货币比特币黄金(Bitcoin Gold)进行双花攻击(双重支付)，造成了千万美元的损失。此次攻击引起了一些对于去中心化以及工作量证明机制的质疑。

# Double-spending<br>
Double-spending is a potential flaw in digital cash scheme in which the same single digital token can be spent more than once. This is possible because a digital token consists of a digital file that can be duplicated or falsified. As with counterfeit money, such double-spending leads to infilation by creating a new amount of fraudulent currency that did not previously exist. This devalues the currency relative to other monetary units, and disminished user trust as well as the circulation adn retantion of the currency. Fundametal cyptogrhic techniques to prevent double-spending while preserving anonymity in a trasaction are blind signatures and particalaly in offline systems, secrect splitting.<br>
