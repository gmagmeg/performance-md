---
marp: true
theme: custom
---

# Memcache有無によるパフォーマンス比較

Apache環境でのキャッシュ効果を測定

---

## レスポンスタイム比較

| 項目 | Memcache無し | Memcache有り | 改善率 |
| --- | --- | --- | --- |
| **平均CPU** | 290% | 48% | **83%削減** |
| **最大メモリ** | 2.175 GiB | 462.1 MiB | **79%削減** |
| **平均レスポンス** | 90.31ms | 18.46ms | **80%改善** |
| **P90レスポンス** | 119.35ms | 27.99ms | **77%改善** |
| **P95レスポンス** | 130.59ms | 36.91ms | **72%改善** |


---

## Memcacheの導入により大幅な性能改善

こんな簡単な設定でも効果<span style="font-size: 2em;">大</span>
```
- opcache.enable=1  // 有効にする
- opcache.enable_cli=1 // cliモードでも有効にする
- opcache.memory_consumption=128 // キャッシュサイズの指定
```
WebサーバーやDBのチューニングも重要だけれど
PHPのチューニングも忘れずに！

