# MetricGAN

- 背景
    - adversarial loss
        - 並不是設計去直接優化目標任務的評價指標
        - 可能不會讓generator越來越好(improved metric scores)
- 解法
    - MetricGAN
        - 優化generator
        - 利用一或多個evaluation metrics
    - MetricGAN 的scores可以由user定義
- 實驗
    - speech enhancement task
        - 評價speech signals的指標相當複雜多樣
        - 可能沒辦法由Lp或常規的adversarial loss去優化

---

- DEM 
    - D用來識別真假的方法可能和我們關注的指標(metrics)並沒有完全關聯性