---
name: geoskill-few-shot-classification
description: '原型网络类中心距离+最近邻分类，输出分类栅格（离线numpy等价实现）'
---

# 小样本遥感分类 | Few-Shot Remote Sensing Classification

Classifies an entire image using very few labeled samples (1–5 per class): the feature mean of each class's support samples serves as the "prototype", each pixel is assigned to the nearest prototype, and a softmax(−distance) confidence is provided; few-shot episode accuracy evaluation is supported.

This skill is an **offline numpy-equivalent implementation** of Prototypical Networks few-shot learning: without depending on torch, it reproduces the metric-learning paradigm through "feature extraction → support-set standardization → prototype computation → nearest-prototype classification by Euclidean distance"; unit tests cover 1-shot and multi-shot episode accuracy, probability normalization, and errors for insufficient samples.

## Dependencies / 依赖

```bash
pip install numpy rasterio scipy scikit-learn geopandas shapely
```

## Usage / 使用方法

### Example 1 (synthetic data, offline)

```bash
python geoskill-few-shot-classification.py --bbox 116.0 39.0 117.0 40.0 --synthetic --output-dir ./out
```

### Example 2: synthetic 3-way 3-shot (offline)

```bash
python geoskill-few-shot-classification.py --bbox 116.0 39.0 117.0 40.0 --synthetic --n-shot 3 --output-dir ./out
```

### Example 3: extreme 1-shot few-sample case

```bash
python geoskill-few-shot-classification.py --bbox 116.0 39.0 117.0 40.0 --synthetic --n-shot 1 --output-dir ./out
```

### Example 4: pseudo few-shot on real imagery (support selected by KMeans)

```bash
python geoskill-few-shot-classification.py --input scene.tif --n-classes 4 --n-shot 5 --output-dir ./out
```

## Output / 输出

| File | Format | Description |
|---|---|---|
| `classification.tif` | GeoTIFF | Full-image nearest-prototype classification label map |
| `few_shot_report.json` | JSON | Episode accuracy/confidence/number of support samples |
| `output-manifest.json` | JSON | Run manifest (inputs/outputs/QA/exit code) |

## Data Source / 数据源 / Source

Local multi-band GeoTIFF, or --synthetic for a three-class spectrally separable scenario (ground truth used for episode evaluation).

## Privacy / 隐私声明 / Privacy

- Runs offline by default; `--synthetic` mode requires no network at all.
- All processing is done locally; no user data is ever uploaded.

## License / License

MIT

---

> 中文完整版：需要时再读 [references/SKILL.zh-CN.md](references/SKILL.zh-CN.md)，不要默认全量加载。
