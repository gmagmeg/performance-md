# Webパフォーマンス試験環境情報

## 概要
このプロジェクトは、同一のLaravelブログアプリケーションを4つの異なるサーバー構成で実行し、パフォーマンス特性を比較検証するためのテスト環境です。

## 共通環境情報

### アプリケーション基盤
- **Laravel Framework**: 12.0以上
- **PHP**: 8.3.20
- **Node.js**: Vite + npm
- **データベース**: MySQL 8.0
- **コンテナ**: Docker + Docker Compose
- **監視**: Jaeger (OpenTelemetry)

### 共通PHPライブラリ
- **フレームワーク**: Laravel Framework 12.0
- **OpenTelemetry**: 分散トレーシング機能
  - open-telemetry/api: ^1.4
  - open-telemetry/sdk: ^1.6
  - open-telemetry/exporter-otlp: ^1.3
  - open-telemetry/opentelemetry-auto-laravel: ^1.2

### 共通データベーススキーマ
- **ユーザー**: 100人
- **投稿**: 1,000件 (ユーザー1人あたり10件)
- **コメント**: 5,000件 (投稿1件あたり5件)
- **閲覧履歴**: 5,000件
- **いいね**: 5,000件
- **カテゴリ**: 30件 (親20件、子10件)
- **タグ**: 100件
- **多対多関係**: 投稿あたり5タグ・5カテゴリ

## サーバー別構成

### 1. Apache構成 (new-apache)
- **ベースイメージ**: php:8.3.20-apache
- **Webサーバー**: Apache 2.4
- **アーキテクチャ**: 伝統的なApache + PHP
- **ポート**: 9100 (HTTP)
- **DBポート**: 3309
- **Jaegerポート**: 16687
- **特徴**: 
  - mod_rewriteによるURL書き換え
  - 標準的なPHP処理モデル
  - OpenTelemetry手動実装

### 2. FrankenPHP構成 (new-frankenphp)
- **ベースイメージ**: dunglas/frankenphp:php8.3
- **Webサーバー**: FrankenPHP (Go + PHP)
- **アーキテクチャ**: Laravel Octane + FrankenPHP
- **ポート**: 9400 (HTTP), 9401 (HTTPS), 443 (HTTP/3)
- **DBポート**: 3306
- **Jaegerポート**: 16686
- **特徴**: 
  - HTTP/2, HTTP/3対応
  - Worker Mode (永続的アプリケーション)
  - ビルトインHTTPS
  - Laravel Octane統合

### 3. Nginx構成 (new-nginx)
- **ベースイメージ**: nginx:latest + php:8.3.20-fpm
- **Webサーバー**: Nginx
- **アーキテクチャ**: Nginx + PHP-FPM分離
- **ポート**: 9200 (HTTP)
- **DBポート**: 3310
- **Jaegerポート**: 16689
- **特徴**: 
  - Nginx/PHP-FPMの分離アーキテクチャ
  - 高い同時接続処理能力
  - カスタムNginx設定

### 4. Swoole構成 (new-swoole-php)
- **ベースイメージ**: phpswoole/swoole:php8.3-zts
- **Webサーバー**: Swoole
- **アーキテクチャ**: Laravel Octane + Swoole + Nginx
- **ポート**: 9300 (HTTP)
- **DBポート**: 3311
- **Jaegerポート**: 16690
- **特徴**: 
  - 高性能非同期処理
  - メモリ常駐アプリケーション
  - Swooleテーブル機能
  - Laravel Octane統合

## パフォーマンステストエンドポイント

### 重負荷読み取りテスト
- **URL**: `/api/read-weight?trace=1`
- **内容**: 複雑なクエリと全リレーション読み込み
- **対象**: データベース読み取り性能

### データ処理テスト
- **URL**: `/api/post-weight?trace=1`
- **内容**: バリデーション・データ処理（DB書き込みなし）
- **対象**: CPU集約的処理性能

### CSV処理テスト
- **URL**: `/api/csv-weight?trace=1`
- **内容**: ファイル処理性能
- **対象**: I/O処理性能

## 監視・トレーシング

### Jaeger UI
各環境でJaegerによる分散トレーシングが利用可能
- Apache: http://localhost:16687
- FrankenPHP: http://localhost:16686
- Nginx: http://localhost:16689
- Swoole: http://localhost:16690

### OpenTelemetry設定
- **サンプリング**: always_on
- **エクスポーター**: OTLP (HTTP/protobuf)
- **無効化**: 自動計測を無効化し手動実装を採用

## 開発・テスト環境

### 共通コマンド
```bash
# 開発環境起動
composer dev

# テスト実行
composer test

# データベース初期化
php artisan migrate:fresh --seed
```

### Docker操作
```bash
# サーバー起動
cd [サーバー名] && docker compose up -d

# 停止
docker compose down

# 再構築
docker compose up --build -d
```

## 比較検証のポイント

1. **レスポンス時間**: 同一負荷での応答速度比較
2. **スループット**: 単位時間あたりの処理能力
3. **メモリ使用量**: 各構成でのメモリ効率
4. **CPU使用率**: 処理負荷による CPU 消費
5. **同時接続数**: 最大同時接続処理能力
6. **エラー率**: 高負荷時のエラー発生率

各サーバー構成の特性を活かしたパフォーマンス検証により、用途に応じた最適なサーバー選択の指針を提供することを目的としています。