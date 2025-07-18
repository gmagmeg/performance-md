---
marp: true
theme: custom
---

| サーバー | p(90) | p(95) | スループット | エラー率 |
|---------|-------|-------|-------------|---------|
| Apache+mod_php | 68.92 ms | 1.68 s | 35.90 RPS | <span class="attention">×2.19%</span> |
| Nginx+FPM | 22.15 ms | 24.72 ms | 38.10 RPS | <span class="good-value-small">0.00%</span> |
| Swoole | <span class="good-value-small">18.38 ms</span> | <span class="good-value-small">21.33 ms</span> | <span class="good-value-small">39.10 RPS</span> | <span class="good-value-small">0.00%</span> |
| FrankenPHP | <span class="good-value-small">18.90 ms</span> | <span class="good-value-small">21.44 ms</span> | <span class="good-value-small">39.50 RPS</span> | <span class="good-value-small">0.00%</span> |