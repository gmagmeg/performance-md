## 各PHP実行環境情報

# 共通環境情報

### アプリケーション基盤
共通項目
- **PHP**: 8.3.20
- **データベース**: MySQL 8.0
- **コンテナ**: Docker + Docker Compose
- **監視**: OpenTelemetry (Jaeger)

### Apache + mod_php, Nginx + php-fpm
Laravel 12

### Swoole + Nginx, FrankenPHP
Laravel Octone

# 計測項目
- CPU使用率
- メモリ使用量
- PHPプロセス
- スループット
- レスポンスタイム

## 比較検証のポイント

1. **レスポンス時間**: 同一負荷での応答速度比較
2. **スループット**: 単位時間あたりの処理能力
3. **メモリ使用量**: 各構成でのメモリ効率
4. **CPU使用率**: 処理負荷による CPU 消費
5. **同時接続数**: 最大同時接続処理能力
6. **エラー率**: 高負荷時のエラー発生率


# 計測ツール
OpenTelemetry
k6

OpenTelemetryを選んだ理由はこちら
https://zenn.dev/booost/articles/a691d0fe7aeae6
ZTS環境に対応したプロファイリングツールが少ない…


# 計測しない項目
- ブラウザレンダリング
PHPはWebAPIサーバーとして振る舞うことが多いため

# テストシナリオ
記事投稿 + 記事取得

ER図を挿入