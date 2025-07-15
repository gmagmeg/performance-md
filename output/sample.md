---
marp: true
theme: custom
---

<h1> <span class="inline-img">⚡</span>スパイクテスト 計測結果発表</h1>

---

<h2><span class="inline-img">⏱️</span> レスポンス時間比較</h2>

単一サーバーで受けようとすると、Apacheは厳しい結果に

| サーバー | p(90) | p(95) | スループット | エラー率 |
|---------|-------|-------|-------------|---------|
| Apache+mod_php | 68.92ms | 1.68s | 35.9 req/s | <span class="attention">×2.19%</span> |
| Nginx+FPM | 22.15ms | 24.72ms | 38.1 req/s | <span class="good-value-small">0.00%</span> |
| Swoole | <span class="good-value-small">18.38ms</span> | <span class="good-value-small">21.33ms</span> | <span class="good-value-small">39.1 req/s</span> | <span class="good-value-small">0.00%</span> |
| FrankenPHP | <span class="good-value-small">18.9ms</span> | <span class="good-value-small">21.44ms</span> | <span class="good-value-small">39.5 req/s</span> | <span class="good-value-small">0.00%</span> |


---

<h2><span class="inline-img">🖥️</span> リソース使用量比較</h2>

<span class="normal-text">CPU使用率とメモリ使用量の比較</span>

| サーバー | 平均CPU使用率 | 平均メモリ使用量 |
| --- | --- | --- |
| Apache+mod_php | 66.86% | 648.09MB |
| Nginx+PHP-FPM | 45.81% | <span class="good-value">165.59MB</span> |
| Nginx+Swoole | <span class="good-value">36.87%</span> | 980.35MB |
| FrankenPHP | <span class="good-value">37.16%</span> | 288.75MB |

* swooleとphp-fpmはNginxサーバーとの合算値

---

<h2><span class="inline-img">📊</span> 性能ランキング</h2>

<span class="normal-text">スパイクテスト総合評価</span>

<div class="ranking">

**<span class="good-value">🥇 FrankenPHP</span>**
- レスポンス: p(90) 18.9ms、p(95) 21.44ms
- スループット: 39.5 req/s（最高）
- エラー率: 0.00%、CPU: 37.16%

**<span class="good-value">🥈 Swoole</span>**
- レスポンス: p(90) 18.38ms（最速）
- スループット: 39.1 req/s
- エラー率: 0.00%、CPU: 36.87%（最低）

</div>

---

<h2><span class="inline-img">🎯</span> 技術的考察</h2>

<span class="normal-text">高負荷耐性とリソース効率の分析</span>

**高負荷耐性**
- **非同期処理系**（Swoole、FrankenPHP）は安定した低レイテンシーを維持
- **従来プロセス管理**（Apache mod_php）は性能劣化とエラー発生

**リソース効率**
- **メモリ効率**: PHP-FPM > FrankenPHP > Apache > Swoole
- **CPU効率**: Swoole ≈ FrankenPHP > PHP-FPM > Apache

<span class="attention">Apache+mod_phpは高負荷時に2.19%のエラー発生</span>

---

<h2><span class="inline-img">💡</span> 推奨事項</h2>

<span class="normal-text">環境別の最適な選択</span>

| 環境 | 推奨サーバー | 理由 |
|------|-------------|------|
| **本番環境** | <span class="good-value">FrankenPHP</span> | バランス型・高安定性 |
| **高性能重視** | <span class="good-value">Swoole</span> | 最速レスポンス・低CPU |
| **リソース制約** | <span class="good-value">Nginx+PHP-FPM</span> | 最少メモリ使用量 |
| **レガシー** | <span class="attention">Apache+mod_php</span> | 高負荷環境では非推奨 |

**結論**: 現代的なPHPサーバーの優位性が明確に実証

---