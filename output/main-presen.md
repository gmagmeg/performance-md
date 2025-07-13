---
marp: true
theme: custom
---

<!-- paginate: true -->


## 目次

1. 導入
1. プロフィール・所属会社紹介
1. 各環境・用語・計測ツール紹介
1. 負荷シナリオ１ - アベレージロードテスト
1. 負荷シナリオ２ - スパイクテスト
1. 総評と選択指針
1. 環境を向上させるTips３選
1. まとめ

---

<h1 class="slide-section"> 導　　入

---

# 比較・検証する環境

<div>
<p>今回は４つのPHP実行環境のパフォーマンス検証</p>
</div>

<div class="tech-stack">
  <div class="tech-item">
    <img src="../images/logo/apache_logo.png" alt="Apache">
    <div class="tech-info">
      <div class="tech-name">Apache + mod_php</div>
      <div class="tech-version"></div>
    </div>
  </div>
  <div class="tech-item">
    <img src="../images/logo/nginx-1.svg" alt="Nginx">
    <div class="tech-info">
      <div class="tech-name">Nginx + PHP-FPM</div>
      <div class="tech-version"></div>
    </div>
  </div>
  <div class="tech-item">
    <img src="../images/logo/swoole.png" alt="Swoole">
    <div class="tech-info">
      <div class="tech-name">Swoole + Nginx</div>
      <div class="tech-version"></div>
    </div>
  </div>
  <div class="tech-item">
    <img src="../images/logo/frankenphp.png" alt="FrankenPHP">
    <div class="tech-info">
      <div class="tech-name">FrankenPHP</div>
      <div class="tech-version"></div>
    </div>
  </div>
</div>

---

# 実行シナリオ概要


**テストタイプ**：ストレステスト
**シナリオ概要**：ユーザーが記事を投稿して、
投稿した記事を複数のユーザーが閲覧しに来る

**テストタイプ**：スパイクテスト
**シナリオ概要**：セール予告後のような急激な閲覧者増によるトラフィック増加に対する

---

<p class="middle-text">ソースコードなどの詳細はGitHubで公開中<br>
urlをここに貼る
</p>


---

<p class="middle-text">それぞれの環境でどうなるか<br>想定しながらお愉しみください</p>

---

<ol class="table-content">
<li>導入</li>
<li class="active-text">プロフィール・所属会社紹介</li>
<li>各環境・用語・計測ツール紹介</li>
<li>負荷シナリオ１ - アベレージロードテスト</li>
<li>負荷シナリオ２ - スパイクテスト</li>
<li>総評と選択指針</li>
<li>環境を向上させるTips３選</li>
<li>まとめ</li>
</ol>


---

todo
プロフィール挟む
これまで発表した内容

---

<ol class="table-content">
<li>導入</li>
<li>プロフィール・所属会社紹介</li>
<li class="active-text">各環境・用語・計測ツール紹介</li>
<li>負荷シナリオ１ - アベレージロードテスト</li>
<li>負荷シナリオ２ - スパイクテスト</li>
<li>総評と選択指針</li>
<li>環境を向上させるTips３選</li>
<li>まとめ</li>
</ol>

---

# 各環境紹介

## Apache + mod_php 

- NTS（Non Thread Safe） プロセスベース
- ApacheのモジュールとしてPHPが直接組み込まれる形式
- リクエストごとにプロセスが処理されるため、<br>リクエスト数に伴ってメモリ使用量が大きくなりがち
- 設定がシンプルで歴史も長い。<br>レガシーシステムで採用されている定番構成

<img src="../images/logo/apache_logo.png" class="apache-logo">

---

## Nginx + PHP-FPM

- NTS（Non Thread Safe）、マルチプロセス形式
- NginxとPHP-FPM（FastCGI Process Manager）が別プロセスで動作する
- プロセスプールによるリソース管理で、<br>高トラフィック時の安定性とメモリ効率が優秀

<img src="../images/logo/nginx-1.svg" class="nginx-logo">

---

## Nginx + Swoole

- NTS版とZTS版の両方が存在（コルーチンはシングルスレッドで動作）
- PHPの非同期I/O拡張で、コルーチンベースの並行処理を実現
- 常駐プロセスでリクエストを処理するため高速

<img src="../images/logo/swoole.png" class="swoole-logo">

---

## Swooleの補足事項

Swoole自体組み込みWebサーバーを持っています
が、餅は餅屋。Webサーバーを立てることを公式も推奨。

<img src="../images/swoole_http_image.png">

---

## FrankenPHP

- ZTS（Zend Thread Safe）、マルチスレッド形式
- Go言語で実装されたPHPのSAPIで、Caddyサーバーに統合されている
- ワーカーモードによるアプリケーション常駐化で<br>起動オーバーヘッドを削減

<img src="../images/logo/frankenphp.png" class="frankenphp-logo">

---

## FrankenPHPの補足事項

2025年5月　PHP Foundationからのオフィシャルサポートを受けることが決定
<img src="../images/2025-05-15-frankenphp.png" width="60%" />

[FrankenPHP Is Now Officially Supported by The PHP Foundation — The PHP Foundation — Supporting, Advancing, and Developing the PHP Language](https://thephp.foundation/blog/2025/05/15/frankenphp/)

---

## より詳細な実行環境

より詳しい詳細はこちらのスライドで説明しています（宣伝）
https://www.docswell.com/s/1313108/ZP2QQ1-2025-03-21-123847
<img src="../images/mae_slide.png" width="60%">

---

# 用語紹介

1. NTS（Non Thread Safe）
1. ZTS（Zend Thread Safe）

PHPには2つのビルドバージョンがあります
それぞれ異なる実行環境に最適化されています


---

### 🧵ZTS（Zend Thread Safe）

<div class="columns">
  <div class="no-border">
    マルチスレッド環境で異なるスレッドが<br>同一リソース（同一メモリや同一変数）にアクセスしても問題ないように、排他機構を持つ<br>
    排他機構のオーバーヘッドで、そのまま扱うとNTSより処理速度が低下する
  </div>
  <div class="inline-img-block">
    <img src="../images/logo/swoole.png" width="180">
    <img src="../images/logo/frankenphp.png" width="180">
  </div>
</div>

### 🔗NTS（Non Thread Safe）

<div class="columns">
  <div class="no-border">
    現在のほとんどの本番環境で採用されている<br>
    シングルスレッド環境向けに最適化されたビルド<br>
    排他機構を持たなくていい分、オーバーヘッドなし
  </div>
  <div class="inline-img-block">
    <img src="../images/logo/apache_logo.png" width="80">
    <img src="../images/logo/nginx-1.svg" width="150">
  </div>
</div>


---

# 計測環境・計測ツール紹介

### 各環境共通アプリケーション基盤

<div class="tech-stack">
  <div class="tech-item">
    <img src="../images/logo/new-php-logo.png" alt="PHP">
    <div class="tech-info">
      <div class="tech-name">PHP</div>
      <div class="tech-version">8.3.20</div>
    </div>
  </div>
  <div class="tech-item">
    <img src="../images/logo/mysql.png" alt="MySQL">
    <div class="tech-info">
      <div class="tech-name">MySQL</div>
      <div class="tech-version">8.0</div>
    </div>
  </div>
  <div class="tech-item">
    <img src="../images/logo/laravel-2.svg" alt="Laravel">
    <div class="tech-info">
      <div class="tech-name">Laravel</div>
      <div class="tech-version">12.0</div>
    </div>
  </div>
  <div class="tech-item">
    <img src="../images/logo/Docker-logo.png" alt="Docker">
    <div class="tech-info">
      <div class="tech-name">Docker</div>
    </div>
  </div>

</div>

---

## 異なる構成部分

<div class="columns">
<div>

### 🧵ZTS構成
- Laravel 12 + **Octane<br>（ZTS向けに最適化するライブラリ）**
#### 対象実行環境
- Swoole + Nginx (Laravel Octane)
- FrankenPHP (Laravel Octane)

</div>

<div>

### 🔗NTS構成
- Laravel 12<br>&nbsp;
#### 対象実行環境
- Apache + mod_php 
- Nginx + php-fpm 

</div>

</div>

---

## 計測ツール

<div class="tech-stack">
  <div class="tech-item">
    <img src="../images/logo/K6-logo.svg.png" alt="PHP">
    <div class="tech-info">
      <div class="tech-name">k6</div>
      <div class="tech-version">負荷検証</div>
    </div>
  </div>

  <div class="tech-item">
    <img src="../images/logo/opentelemetry.png" alt="OpenTelemetry">
    <div class="tech-info">
      <div class="tech-name">OpenTelemetry</div>
      <div class="tech-version">プロファイリング</div>
    </div>
  </div>
</div>

### OpenTelemetryを選んだ理由
- そもそもZTS環境に対応したプロファイリングツールが少ない
詳細: https://zenn.dev/booost/articles/a691d0fe7aeae6

---

### 詳細はこちら

githubに挙げているので、そちらを参照してください
todo：

---

<ol class="table-content">
<li>導入</li>
<li>プロフィール・所属会社紹介</li>
<li>各環境・用語・計測ツール紹介</li>
<li class="active-text">負荷シナリオ１ - アベレージロードテスト</li>
<li>負荷シナリオ２ - スパイクテスト</li>
<li>総評と選択指針</li>
<li>環境を向上させるTips３選</li>
<li>まとめ</li>
</ol>

---

## 負荷試験シナリオ１ - アベレージロードテスト

<div class="columns ">
  <p class=""><img src="../images/chart-average-load-test-overview.png" width=500 /></p>
  <div class="three">
    <p><span class="bold-text">ℹ️概要</span><br>ユーザーが記事を投稿する<br>投稿した記事を複数のユーザーが閲覧しに来る</p>
    <p><span class="bold-text">🎯目的</span>　多数のユーザーによる同時アクセス時の レスポンス性能 と 安定性 を評価する</p>
  </div>
</div>

---

<h3 class="test-icon">試験概要</h3>

- **ユーザー行動**: 記事投稿 **1回**につき、記事閲覧が**10回**発生する
- **負荷増加**: 開始**60秒**で最大**80ユーザー/秒**まで増加させる
- **維持時間**: 最大負荷で**3分間**維持する<br>4分間でおおよそ**6500回**のリクエストが発生

<h3 class="check-icon"> 合格基準 (SLO)</h3>

- **記事投稿** (P90): **3秒**以内
- **記事閲覧** (P90): **1秒**以内
- **エラーレート**: **0.1%** 未満

---

## アプリ概要データベース
計：９テーブルを更新する

<div class="columns">
<div>

1. usersd
2. posts
3. categories
4. tags
5. comments

</div>
<div>

6. post_views
7. likes
8. post_tags
9. post_categories

</div>
</div>

---

## 計測結果発表

---

どの環境もエラーは無し！
素晴らしい！
👏

---

## リソース使用量比較

CPU使用率とメモリ使用量の比較

| 環境 | 平均CPU使用率 | 平均メモリ使用量 | CPU効率 | メモリ効率 |
| --- | --- | --- | --- | --- |
| Apache+PHP | 35.77% | 360.08MiB | 要改善 | 普通 |
| Nginx+PHP | 34.32% | **88.75MiB** | 普通 | **最優秀** |
| **Swoole** | **32.03%** | 962.9MiB | **良好** | 要注意 |
| **FrankenPHP** | **20.47%** | 288.4MiB | **最優秀** | 良好 |

---

## PHP実行環境比較結果

| 環境 | P95レスポンス | P90レスポンス | スループット |
| --- | --- | --- | --- |
| Apache+PHP | 36.91ms | 27.99ms | 28.49 RPS |
| Nginx+PHP | 33.77ms | 25.54ms | 28.06 RPS |
| Swoole | 27.15ms | 20.51ms | 28.58 RPS |
| **FrankenPHP** | **25.82ms** | **19.51ms** | **28.65 RPS** |

<!-- FrankenPHPが最高のレスポンス性能、Nginx+PHPが最少メモリ使用量 -->

---

## レスポンス時間詳細比較

各処理別のレスポンス時間（P90）

| 環境 | POST処理<br>（記事作成） | GET処理<br>（記事取得） |
| --- | --- | --- |
| Apache+PHP | 49.61ms | 22.45ms |
| Nginx+PHP | 50.53ms | 20.69ms |
| **Swoole** | **45.64ms** | **16.38ms** |
| **FrankenPHP** | **45.86ms** | **15.48ms** |

<!-- FrankenPHP、Swooleが高速。従来環境より30-40%高速 -->

---

## 計測結果総評

### リソース効率
- 全環境でエラー発生なし（**100%安定性**）
- **CPU効率**: FrankenPHP > Swoole > 従来構成
- **メモリ効率**: Nginx+PHP > FrankenPHP > Apache > Swoole

**補足**
- Nginxはサーバーとphp-fpmでメモリが分散
- Swooleはメモリにプロセスを常駐させるため、他と比べて消費率高

---

### パフォーマンス面
- **FrankenPHP**が総合的に最優秀（レスポンス・CPU効率）
- **Swoole**もFrankenPHPに匹敵する高性能
- 従来構成比で**30-40%の性能向上**を実現

とはいえ…

| 環境 | P95レスポンス | P90レスポンス | スループット |
| --- | --- | --- | --- |
| Apache+PHP | 36.91ms | 27.99ms | 28.49 RPS |
| **FrankenPHP** | **25.82ms** | **19.51ms** | **28.65 RPS** |

ここまで見て意外と大きな差がないように見えたのではないでしょうか

---

ここで影の立役者
### OPcache


---

## OPcacheの有無で比較

Apache+mod_php
同じ環境でもこれだけの違いが出ます

| 項目 | Memcache無し | Memcache有り | 改善率 |
| --- | --- | --- | --- |
| **平均使用CPU** | 290% | 48% | **83%削減** |
| **平均使用メモリ** | 2.175 **GiB** | 462.1 **MiB** | **79%削減** |
| **平均レスポンス** | 90.31ms | 18.46ms | **80%改善** |
| **P90レスポンス** | 119.35ms | 27.99ms | **77%改善** |
| **P95レスポンス** | 130.59ms | 36.91ms | **72%改善** |

---

opcacheありのApache+mod_php
opcacheなしのfrankenphp
そんなに変わらない

---

## opcacheの導入により大幅な性能改善

こんな簡単な設定でも効果<span class="font-size-large">大</span>
```
- opcache.enable=1  // 有効にする
- opcache.enable_cli=1 // cliモードでも有効にする
- opcache.memory_consumption=128 // キャッシュサイズの指定
```
WebサーバーやDBのチューニングも重要だけれど
PHPのチューニングも大切！

---

PHPのチューニングの話は一旦おしまい。
よりWebサーバーの性能差が出る検証を見ていきます

---

## 負荷シナリオ２

### 概要
セール予告後のような急激な閲覧者増によるトラフィック増加に対する

### 目的
Webアプリケーションの**レスポンス性能**と**安定性**を評価する。

**試験内容**:
* **開始**: 0ユーザーから10秒で10ユーザーに増加
* **スパイク**: 20秒で200ユーザーまで急激に増加
* **終了**: 10秒で0ユーザーに減少

<img src="../images/chart-spike-test-overview.png" />

---

**合格基準 (SLO)**:
* **レスポンスタイム (95パーセンタイル値)**: **2秒**未満
* **エラーレート**: **1%** 未満

---

<h1 class="slide-section">計測結果発表</h1>

---

## スパイクテスト結果比較

PHPアプリケーションサーバー性能比較
200VU・40秒間のスパイクテスト

---

## テスト概要

| 項目 | 値 |
| --- | --- |
| 最大VU数 | 200 |
| テスト時間 | 40秒 |
| 段階 | 3段階のスパイク |
| 閾値 | P95 < 2秒、失敗率 < 1% |

---


## テスト概要

- **テストタイプ**: スパイクテスト
- **最大VU数**: 200
- **テスト時間**: 40秒 (3段階)
- **閾値**: p(95) < 2秒, エラー率 < 1%

---

## レスポンス時間比較

| サーバー | p(90) | p(95) | スループット | エラー率 | 結果 |
|---------|-------|-------|-------------|---------|------|
| Apache | 68.92ms | 1.68s | 35.9 req/s | <span class="attention">2.19%</span> | ⚠️ |
| Nginx+FPM | 22.15ms | 24.72ms | 38.1 req/s | 0.00% | ✅ |
| Swoole | 18.38ms | 21.33ms | 38.1 req/s | 0.00% | ✅ |
| FrankenPHP | 18.9ms | 21.44ms | 39.5 req/s | 0.00% | ✅ |


---

## リソース使用量

| サーバー | 平均CPU使用率 | 平均メモリ使用率 | 効率 |
|---------|---------|-----------|------|
| Apache | 66.86% | 648.09MB | 低 |
| Nginx+FPM | 45.81% | 65.59MB | 高 |
| Swoole | 36.87% | 980.35MB | 中 |
| FrankenPHP | 37.16% | 288.75MB | 高 |

---

# 結果サマリー

**性能ランキング:**
1. **Swoole** - 最速レスポンス
2. **FrankenPHP** - 最高スループット
3. **Nginx+FPM** - バランス良好
4. **Apache** - 高負荷時に劣化

**リソース効率:**
- FrankenPHP・Nginx: 低メモリ
- Swoole: 低CPU使用率

---

## 負荷シナリオ1・2総評

### パフォーマンス面の発見

**通常負荷時（シナリオ1）**
- 全環境で安定動作、差は僅差
- FrankenPHPが総合的に最優秀
- OPcacheの効果が絶大（80%の性能向上）

**高負荷時（シナリオ2）**
- 環境間の性能差が顕著に現れる
- 従来のApache構成では限界が露呈
- ZTS・NTS環境が高負荷耐性で優位性を発揮

---

### 実運用での選択指針

**性能重視**: FrankenPHP・Swoole
**リソース効率**: Nginx+PHP-FPM
**安定性重視**: Nginx+PHP-FPM・FrankenPHP

### 重要な教訓
**OPcacheは必須設定**
どの環境でも80%の性能向上効果

---

## パフォーマンスがいい方に換えるのが正解か？
<div>&nbsp;<br>&nbsp;</div>
<div>
  <ul class="one font-size-large">
    <li>Swoole</li>
    <li>FrankenPHP</li>
  </ul>
  <div class="one">
    <img src="../images/thinking_face.png" width="20%" />
  </div>
</div>

---

# アプリケーションの状態で考える

## そもそも現状に課題がないないのなら<br>変える必要はない

<span class="normal-text">Apache + mod_php環境であっても
課題がないのなら変える必要はありません。
Apacheもバリバリ更新中</span>

---

# アプリケーションの利用用途で考える

## 読み取り主体か、書き込み主体か

### アプリケーションが読み取り主体
<span class="normal-text">Webサーバー・PHPのチューニングが効果的</span>

### アプリケーションが書き込み主体
<span class="normal-text">DBのチューニングが効果的</span>

---

### 大きな改善をしなくても<br>少しの改善で早くすることが出来ないのか？

---


<h1 class="slide-section"> 環境を向上させるTips３選

---

<ul class="ol-large">
<li>1. opcacheを使う</li>
<li>2. Apache, Nginx のearly hints(103)対応</li>
<li>3. Symfonyのドキュメントを参照する</li>
</ul>

---

## 1. opcacheを使う

### 再掲
```
- opcache.enable=1  // 有効にする
- opcache.enable_cli=1 // cliモードでも有効にする
- opcache.memory_consumption=128 // キャッシュサイズの指定
```

---


## 2. Apache, Nginxのearly hints(103)対応
<div class="columns">
  <p class="one"><img src="../images/logo/nginx-1.svg" width=50% /></p>
  <p class="three">ver：1.29.0<br>2025年6月24日リリース</p>
</div>

<div class="columns">
  <p class="one"><img src="../images/logo/apache_logo.png" width=30% /></p>
  <p class="three">モジュール：HTTP/2<br>https://httpd.apache.org/docs/current/howto/http2.html<br>#page-header</p>
</div>

このプレゼン中には間に合いませんでした...

---

## FrankenPHPの対応状況

<p>&nbsp;</p>
<div class="columns normal-text">
  <p class="one"><img src="../images/logo/frankenphp.png" /></p>
  <p class="three">early hints(103)は組み込み済み<br>
  PHPのコードに headers_send(103); と書くだけでOK<br>とても楽
  </p>
</div>

---

## 3. Symfonyのドキュメントを参照する
<img src="../images/logo/symphony-sample.png" width="70%" />

---

<p class="inline-img-block">
<img src="../images/logo/symphony.png" width="40%" /><span class="middle-text">に関わらず役立つ情報がたくさん</span>
</p>

<ul class="middle-text">
  <li>OPcacheの最適な設定値</li>
  <li>compsoer の最適なinstall時の設定<br>etc・・・</li>
</ul>

---

## 実行環境特性まとめ

---

## Apache + mod_php
<img src="../images/logo/apache_logo.png" class="apache-logo">

<ul class="middle-list-text">
  <li><strong>適用シーン</strong>: 既存継続運用。情報が豊富</li>
  <li><strong>主なメリット</strong>: 設定が簡単で、安定性している</li>
  <li><strong>注意点</strong>: １台で高負荷を受けると性能が劣化する<br>
  LBを設置してサーバー分散すれば、問題点も解消しやすい
</ul>

---

## Nginx+PHP-FPM
<img src="../images/logo/nginx-1.svg" class="nginx-logo">

<ul class="middle-list-text">
  <li><strong>適用シーン</strong>: バランス重視。現在最も普及している構成。</li>
  <li><strong>主なメリット</strong>: 低メモリで安定性が高い。</li>
  <li><strong>注意点</strong>: 中程度の性能だが、実用上は十分。<br>
  １台１台のリソース効率が最も良好だが、<br>PHP+Webサーバーでサーバ台数が増えがち</li>
</ul>

---

## Swoole
<img src="../images/logo/swoole.png" class="swoole-logo">

<ul class="middle-list-text">
  <li><strong>適用シーン</strong>: 高性能要求。リアルタイム性が重要なシステム</li>
  <li><strong>主なメリット</strong>: 最速レスポンス。コルーチンによる非同期処理</li>
  <li><strong>注意点</strong>: メモリ消費が大きい。<br>チューニング項目が多岐にわたる<br>
  常駐プロセスのため、<br>メモリリークに注意が必要</li>
</ul>

---

## FrankenPHP
<img src="../images/logo/frankenphp.png" class="frankenphp-logo">

<ul class="middle-list-text">
  <li><strong>適用シーン</strong>: 簡単に高性能要求を実現したい。</li>
  <li><strong>主なメリット</strong>: 簡単にいい性能を取りやすい<br>（Early Hints標準対応など）</li>
  <li><strong>注意点</strong>: 新しい技術のため情報が少ない<br>
  実運用例も少ない</li>
</ul>

---

<p class="middle-text">
皆さんの実行環境選択の助けになれば幸いです<br>
ご清聴ありがとうございました
</p>