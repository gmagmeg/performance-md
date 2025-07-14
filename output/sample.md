---
marp: true
theme: custom
---

<!-- paginate: true -->

<!-- _class: center -->

## リソース使用量比較

<span class="normal-text">CPU使用率とメモリ使用量の比較</span>

| 環境 | 平均CPU使用率 | 平均メモリ使用量 |
| --- | --- | --- | 
| Apache+PHP | 35.77% | 360.08MiB |
| Nginx+PHP | 34.32% |  <span class="good-value">88.75MiB</span> |
| Swoole | 32.03% | 962.9MiB |
| FrankenPHP |  <span class="good-value">20.47%</span> | 288.4MiB |


---


## PHP実行環境比較結果

<span class="normal-text">レスポンス時間とスループットの比較</span>

| 環境 | P95レスポンス | P90レスポンス | スループット |
| --- | --- | --- | --- |
| Apache+PHP | 36.91ms | 27.99ms | 28.49 RPS |
| Nginx+PHP | 33.77ms | 25.54ms | 28.06 RPS |
| Swoole | <span class="good-value">27.15ms</span> | <span class="good-value">20.51ms</span> | 28.58 RPS |
| FrankenPHP | <span class="good-value">25.82ms</span> | <span class="good-value">19.51ms</span> | <span class="good-value">28.65 RPS</span> |

---


## レスポンス時間詳細比較

<span class="normal-text">各処理別のレスポンス時間（P90）</span>

| 環境 | POST処理<br>（記事作成） | GET処理<br>（記事取得） |
| --- | --- | --- |
| Apache+PHP | 49.61ms | 22.45ms |
| Nginx+PHP | 50.53ms | 20.69ms |
| Swoole | <span class="good-value">45.64ms</span> | <span class="good-value">16.38ms</span> |
| FrankenPHP | <span class="good-value">45.86ms</span> | <span class="good-value">15.48ms</span> |