# Image Color Extraction Tools

Two complementary tools for extracting color palettes from images.

---

## img-colors.com — Clustering-Based Extraction

**URL:** https://img-colors.com/
**Author:** mrmrs / mrmrs.cc
**Architecture:** Edge-computed (Cloudflare Workers), no server/database

### How It Works

1. **Upload** → resized to max 1,500px, converted to JPEG
2. **Sample** → ~5,000 random pixels (keeps payload tiny)
3. **Cluster** → 7 unsupervised algorithms find palette centroids
4. **Visualize** → 3D point cloud of sampled pixels + centroids
5. **Generate** → click any palette → instant mesh-blurred gradient background

### 7 Clustering Algorithms

### Seven Methods (with RGB / Lab variants)

| Method                 | What it does                                                                 | Trade-off                                                      |
| ---------------------- | ---------------------------------------------------------------------------- | -------------------------------------------------------------- |
| **K-Means**            | Lloyd-style iteration (`ml-kmeans`) to k centroids                           | Fast; favors round, similar-sized clusters in the color space  |
| **PCA + K-Means**      | One PCA axis orders pixels; quantile-spaced seeds, then K-Means              | Often better seeds than random init; still k-means assumptions   |
| **DBSCAN**             | Density-connected regions in RGB/Lab                                         | Arbitrary shapes; noise points can be dropped                  |
| **OPTICS**             | Ordering by reachability; clusters from density (`density-clustering`)       | Handles varying density better than a single DBSCAN ε           |
| **Agglomerative**      | Hierarchical clustering (average linkage / AGNES), cut to k groups           | Flexible tree cut; heavier on large samples                    |
| **Median-Cut**         | Recursively splits the box with the largest R/G/B range at the median pixel  | Classic quantization; very fast; builds eight buckets in code, then respects the global palette-size limit |
| **Random Sampling**    | k **distinct** random pixels from the subsample, equal weight                | Baseline / stress-test; not optimizing a cluster criterion      |

### 3 Color Spaces for Clustering

| Space                 | Pros                                                       | Cons                                                             |
| --------------------- | ---------------------------------------------------------- | ---------------------------------------------------------------- |
| **RGB**               | Raw screen values, easy math                               | Not perceptually uniform (yellow "farther" from white than blue) |
| **CIELab**            | Perceptually uniform — equal step = equal perceived change | Best for human-expectation clustering                            |
| **HSL (cylindrical)** | Separates hue from sat/lightness; good for creative UI     | Wonky distance near poles                                        |

**Tip:** Toggle color space buttons and watch the 3D point cloud morph — same data, different clustering results.

### Mesh Gradient Generation

Click any palette card → instantly generates a blurred mesh gradient background from those colors. Perfect for hero sections or wallpaper experiments.

---

## okpalette.color.pizza — OKLCH-Based Extraction

**URL:** https://okpalette.color.pizza/
**Author:** meodai / Elastiq.ch
**Privacy:** No cookies, no tracking, no uploads

### How It Works

Upload or paste an image → extracts palette in **OKLab/OKLCh** color space with analysis metrics.

### Analysis Metrics

| Metric                     | What it measures             |
| -------------------------- | ---------------------------- |
| **Avg Lightness**          | Overall brightness (%)       |
| **Avg Chroma**             | Color intensity              |
| **Colorfulness**           | Vibrancy quantification      |
| **Light/Dark Ratio**       | Brightness distribution      |
| **Sparse Color Detection** | Whether colors are dispersed |

### Controls

- **Muted ↔ Saturated** slider — bias extraction toward desaturated or vivid colors
- **Dark ↔ Light** slider — bias toward shadows or highlights
- **Auto-Detect Bias** — automatic adjustment

### Visualizations

- HSV Cylinder view
- HSV Cube view
- Debug view (⌘+I)

### Export

- SVG, PNG, statistics data

---

## When to Use Which

| Scenario                                  | Best tool                     |
| ----------------------------------------- | ----------------------------- |
| Compare clustering algorithms             | img-colors.com (7 algorithms) |
| See 3D point cloud of image colors        | img-colors.com                |
| Get mesh gradient from image              | img-colors.com                |
| OKLCH-native extraction                   | okpalette.color.pizza         |
| Bias toward muted/saturated or dark/light | okpalette.color.pizza         |
| Export palette stats                      | okpalette.color.pizza         |
| Privacy-first (no uploads)                | okpalette.color.pizza         |

## Links

- **img-colors.com:** https://img-colors.com/
- **okpalette.color.pizza:** https://okpalette.color.pizza/
