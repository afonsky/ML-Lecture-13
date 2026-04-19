# Quality metrics

#### Two kinds of quality metrics for clustering:

<br>

* **Supervised** (external validation)
  * Require ground truth labels (rare in practice!)
  * Useful for benchmarking algorithms on labeled datasets
  * Invariant to cluster naming

<br>

* **Unsupervised** (internal validation)
  * No ground truth needed
  * Based on intuition about "good" clusters:
    * Objects within a cluster should be **close** to each other
    * Objects from different clusters should be **far** from each other

---

# Rand Index

#### Rand Index ($RI$) is supervised quality metric defined as:
$$RI = \frac{\textcolor{red}{TP} + \textcolor{blue}{TN}}{\textcolor{red}{TP} + \textcolor{blue}{TN} + \textcolor{orange}{FP} + \textcolor{green}{FN}}$$
where:
* $\textcolor{red}{TP}$ – number of pairs in the same cluster in predictions and the ground truth
* $\textcolor{blue}{TN}$ – number of pairs from different clusters in predictions and the ground truth
* $\textcolor{orange}{FP}$ – number of pairs in the same cluster in predictions, but from different clusters in the ground truth
* $\textcolor{green}{FN}$ – number of pairs in the same cluster in the ground truth, but from the different clusters in predictions

---

# Adjusted Rand Index

#### Adjusted Rand Index ($ARI$) corrects for chance:
$$ARI = \frac{RI - \mathbb{E}[RI]}{RI_{\max} - \mathbb{E}[RI]}$$
<br>

* $ARI \approx 0$ for **random** labeling (regardless of $K$ and $N$)
* $ARI = 1$ for **perfect** clustering
* $ARI < 0$ means worse than random
* **Most commonly used** supervised metric in practice

---
zoom: 0.9
---

# Silhouette score

#### Silhouette is the most popular **unsupervised** quality metric

For each object $i$:
* $s_i$ — mean distance to all objects in the **same** cluster ("cohesion")
* $d_i$ — mean distance to all objects in the **nearest other** cluster ("separation")

$$\mathrm{sil}(i) = \frac{d_i - s_i}{\max\{d_i, s_i\}} \in [-1, 1]$$

#### Interpretation:
* $\approx +1$: object is **well-matched** to its cluster, far from neighbors
* $\approx 0$: object is **on the border** between two clusters
* $\approx -1$: object is likely **misclassified** (closer to another cluster)

Overall: $\quad \mathrm{Silhouette} = \frac{1}{N}\sum\limits_{i=1}^N \mathrm{sil}(i)$

---

# Ex. of quality metrics for clustering

<br>
<br>
<div class="grid grid-cols-[1fr_1fr] gap-10">
<div>
  <figure>
    <img src="/clusters.png" style="width: 380px !important;">
  </figure>
</div>
<div>
  <figure>
    <img src="/quality_metrics.png" style="width: 500px !important;">
  </figure>
</div>
</div>

---

# K-Means limitations

<br>

* K-Means finds cluster centers, then assigns points to the **nearest** center
* This creates **Voronoi partitions** — always convex regions!
* Real clusters may have **complex shapes**: circles, moons, elongated regions

<br>

#### What can we do?
* **Hierarchical clustering** — merge nearby small clusters into larger ones
* **Density-based methods** (DBSCAN) — clusters are dense regions of any shape