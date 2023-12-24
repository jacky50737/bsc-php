[English](./README.md) | 繁體中文 | [简体中文](./README-CN.md)

<h1 align="center">BSC-PHP</h1>

<p align="center">
  <a href="https://github.com/jacky50737/bsc-php/releases"><img src="https://poser.pugx.org/jacky50737/bsc-php/v/stable" alt="Stable Version"></a>
  <a href="https://www.php.net"><img src="https://img.shields.io/badge/php-%3E=8.1-brightgreen.svg?maxAge=2592000" alt="Php Version"></a>
  <a href="https://github.com/jacky50737/bsc-php/blob/master/LICENSE"><img src="https://img.shields.io/github/license/jacky50737/bsc-php.svg?maxAge=2592000" alt="bsc-php License"></a>
  <a href="https://packagist.org/packages/jacky50737/bsc-php"><img src="https://poser.pugx.org/jacky50737/bsc-php/downloads" alt="Total Downloads"></a>
</p>

## 概述

BSC-PHP 目前支援币安智能链的 BNB 和 BEP20 數位資產常用的生成地址，發起轉帳，查詢餘額，離線簽名等功能。

## 特點

1. 一套寫法兼容 TRON 網路中 TRX 貨幣和 TRC 系列所有通證
1. 介面方法可靈活增減

## 支援方法

### 錢包

- \*產生私鑰創建帳戶 `newAccountByPrivateKey()`
- \*產生助憶詞創建帳戶 `newAccountByMnemonic()`
- 使用助憶詞還原帳戶 `revertAccountByMnemonic(string $mnemonic)`
- 根據私鑰得到地址 `revertAccountByPrivateKey(string $privateKey)`

### Bnb & BEP20

- \*查詢餘額(BNB) `bnbBalance(string $address)`
- \*查詢餘額(BEP20) `balance(string $address)`
- \*交易轉帳(離線簽名) `transfer(string $from, string $to, float $amount)`
- 查詢最新區塊 `blockNumber()`
- 根據區塊鏈查詢資訊 `getBlockByNumber(int $blockID)`
- 根據交易雜湊返回交易的收據 `getTransactionReceipt(string $txHash)`
- \*根據交易雜湊返回關於所請求交易的資訊 `getTransactionByHash(string $txHash)`
- \*根據交易雜湊查詢交易狀態 `receiptStatus(string $txHash)`

## 快速開始

### 安裝

PHP8

```php
composer require jacky50737/bsc-php

```

or PHP7

```php
composer require jacky50737/bsc-php ~1.0
```

### 介面

#### Wallet

```php
$wallet = new \Binance\Wallet();

// 產生私鑰建立帳戶
$wallet->newAccountByPrivateKey();

// 產生助憶詞建立帳戶
$wallet->newAccountByMnemonic();

// 使用助憶詞還原帳戶
$mnemonic = 'elite link code extra twist autumn flower purse excuse harsh kitchen whip';
$wallet->revertAccountByMnemonic($mnemonic);

// 根據私鑰得到地址
$privateKey = '5e9340935f4c02628cec5d04cc281012537cafa8dae0e27ff56563b8dffab368';
$wallet->revertAccountByPrivateKey($privateKey);
```

#### Bnb & BEP20

```php
## 方法 1 : BSC RPC Nodes
$uri = 'https://bsc-dataseed1.defibit.io/';// Mainnet
// $uri = 'https://data-seed-prebsc-1-s1.binance.org:8545/';// Testnet
$api = new \Binance\NodeApi($uri);

## 方法 2 : Bscscan Api
$apiKey = 'QVG2GK41ASNSD21KJTXUAQ4JTRQ4XUQZCX';
$api = new \Binance\BscscanApi($apiKey);

$bnb = new \Binance\Bnb($api);

$config = [
    'contract_address' => '0x55d398326f99059fF775485246999027B3197955',// USDT BEP20
    'decimals' => 18,
];
$bep20 = new \Binance\BEP20($api, $config);

// 查詢餘額
$address = '0x1667ca2c72d8699f0c34c55ea00b60eef021be3a';
$bnb->bnbBalance($address);
$bep20->balance($address);

// 交易轉帳(離線簽名)
$from = '0x1667ca2c72d8699f0c34c55ea00b60eef021be3a';
$to = '0x1667ca2c72d8699f0c34c55ea00b60eef021****';
$amount = 0.1;
$bnb->transfer($from, $to, $amount);
$bep20->transfer($from, $to, $amount);

// 查詢最新區塊
$bnb->blockNumber();
$bep20->blockNumber();

// 根據區塊鏈查詢資訊
$blockID = 24631027;
$bnb->getBlockByNumber($blockID);
$bep20->getBlockByNumber($blockID);

// 根據交易雜湊返回交易的收據
$txHash = '0x4dd20d01af4c621d2fc293dff17a8fd8403ea3577988bfb245a18bfb6f50604b';
$bnb->getTransactionReceipt($txHash);
$bep20->getTransactionReceipt($txHash);

// 根據交易雜湊返回關於所請求交易的資訊
$txHash = '0x4dd20d01af4c621d2fc293dff17a8fd8403ea3577988bfb245a18bfb6f50604b';
$bnb->getTransactionByHash($txHash);
$bep20->getTransactionByHash($txHash);

// 根據交易雜湊查詢交易狀態
$txHash = '0x4dd20d01af4c621d2fc293dff17a8fd8403ea3577988bfb245a18bfb6f50604b';
$bnb->receiptStatus($txHash);
$bep20->receiptStatus($txHash);
```

## 计划

- 支持 ERC721|ERC-1155
- 智能合约

## 🌟🌟

[![Stargazers over time](https://starchart.cc/jacky50737/bsc-php.svg)](https://starchart.cc/jacky50737/bsc-php)