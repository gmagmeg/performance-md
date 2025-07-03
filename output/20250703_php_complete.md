---
marp: true
theme: custom
---

<!-- paginate: true -->

## PHPビルドバージョンと実行環境の比較

---

## 概要

PHPには2つのビルドバージョンがあります
それぞれ異なる実行環境に最適化されています

1. NTS（Non Thread Safe）
1. ZTS（Zend Thread Safe）

---

## NTS（Non Thread Safe）

シングルスレッド環境向けに最適化されたビルド
スレッド間の排他制御が不要

## ZTS（Zend Thread Safe）

マルチスレッド環境で安全に動作する
メモリやリソースへのアクセスを同期化する仕組みを持つ

---

|  | NTS (Non Thread Safe) | ZTS (Zend Thread Safe) |
| --- | --- | --- |
| 対象環境 | シングルスレッド<br>（プロセスベース） | マルチスレッド環境 |
| メモリ使用量 | プロセスごとに全体を複製<br>（非効率） | スレッド間でコード共有<br>（効率的） |
| 適用環境 | <p><img src="../images/logo/apache_logo.png" width="80"></p><p><img src="../images/logo/nginx-1.svg" width="180"></p> | <p><img src="../images/logo/frankenphp.png" width="200"></p><p><img src="../images/logo/swoole.png" width="300"></p>|

---

## 各実行環境の概要紹介

---

# Apache + mod_php 

- NTS（Non Thread Safe）、プロセスベース
- ApacheのモジュールとしてPHPが直接組み込まれる形式
- リクエストごとにプロセスが処理されるため、メモリ使用量が大きくなりがち
- 設定がシンプルで歴史も長い。レガシーシステムで採用されている定番構成

<img src="../images/logo/apache_logo.png" class="apache-logo">

---

# Nginx + PHP-FPM

- NTS（Non Thread Safe）、マルチプロセス形式
- NginxとPHP-FPM（FastCGI Process Manager）が別プロセスで動作する
- プロセスプールによるリソース管理で、高トラフィック時の安定性とメモリ効率が優秀

<img src="../images/logo/nginx-1.svg" class="nginx-logo">

---

# Nginx + Swoole

- NTS版とZTS版の両方が存在（コルーチンはシングルスレッドで動作）
- PHPの非同期I/O拡張で、コルーチンベースの並行処理を実現
- HTTPサーバー機能を内蔵し、常駐プロセスでリクエストを処理するため高速

<img src="../images/logo/swoole.png" class="swoole-logo">

---

# Swooleの補足事項

Swoole自体組み込みWebサーバーを持っています
が、餅は餅屋。Webサーバーを立てることを公式も推奨。

<img src="../images/swoole_http_image.png">

---

# FrankenPHP

- ZTS（Zend Thread Safe）、マルチスレッド形式
- Go言語で実装されたPHPのSAPIで、Caddyサーバーに統合されている
- ワーカーモードによるアプリケーション常駐化で、起動オーバーヘッドを削減

<img src="../images/logo/frankenphp.png" class="frankenphp-logo">

---

# FrankenPHPの補足事項

2025年5月に**PHP Foundation**からのオフィシャルサポートを受けることが決定。
積極的にサポートされることが公式に発表されました。

[FrankenPHP Is Now Officially Supported by The PHP Foundation — The PHP Foundation — Supporting, Advancing, and Developing the PHP Language](https://thephp.foundation/blog/2025/05/15/frankenphp/)

---

各実行環境の詳細はこちらのスライドで説明しています（宣伝）
https://www.docswell.com/s/1313108/ZP2QQ1-2025-03-21-123847
<img src="../images/mae_slide.png" width="80%">


---

負荷試験環境の話をここから書いていく