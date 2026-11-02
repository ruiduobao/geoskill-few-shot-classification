# Few-Shot Remote Sensing Classification (geoskill-few-shot-classification)

> Prototype-network class-center distance plus nearest-neighbor classification; outputs a classification raster (offline numpy-equivalent implementation).

---

## 1. Overview

Classifies an entire image with very few labeled samples (1–5 per class): the mean feature of each class's support samples serves as the "prototype", every pixel is assigned to the nearest prototype, and a softmax(−distance) confidence is produced; few-shot episode accuracy evaluation is also supported. This skill is an **offline numpy-equivalent implementation** of Prototypical Networks few-shot learning: it does not depend on torch and reproduces the metric-learning paradigm via "feature extraction → support-set normalization → prototype computation → nearest-prototype classification by Euclidean distance". Unit tests cover 1-shot and multi-shot episode accuracy, probability normalization, and errors for insufficient samples.

## 3. Quick Start

```bash
pip install -r requirements.txt
python geoskill-few-shot-classification.py --bbox 116 39 117 40 --synthetic --output-dir ./out
```

## 4. CLI Parameters

Run `python <skill>.py --help` for the full list. Common parameters:

| Parameter | Type | Description |
|---|---|---|
| `--bbox` | `float[4]` | WGS84 bounding box `min_lon min_lat max_lon max_lat` |
| `--input` | `path` | Local input file (GeoJSON/GeoTIFF/etc.) |
| `--output-dir` | `path` | Output directory (default `./output`) |
| `--synthetic` | `flag` | Use synthetic data instead of real input |
| `--quiet` | `flag` | Suppress non-essential stdout |

## 5. Input / Output

| File | Format | Description |
|---|---|---|
| `classification.tif` | GeoTIFF | Whole-image nearest-prototype classification label map |
| `few_shot_report.json` | JSON | Episode accuracy / confidence / number of support samples |
| `output-manifest.json` | JSON | Run manifest (inputs/outputs/QA/exit code) |

## 6. Technical Principle

(see SKILL.md for details)

## 8. License

MIT License. See [`LICENSE`](./LICENSE) for full text.

---

> 中文完整版：[references/SKILL.zh-CN.md](references/SKILL.zh-CN.md)
