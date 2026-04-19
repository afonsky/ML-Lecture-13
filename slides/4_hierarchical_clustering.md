# Intuition

<br>
<br>
<div class="grid grid-cols-[4fr_5fr] gap-10">
<div>
<br>
<br>

* Let’s ask K-Means to find many clusters
* Each found cluster will be inside a real cluster
* Now, let’s unite neighbor found clusters into one
* As a result, we will get clusters with more complex shapes
</div>
<div>
  <figure>
    <img src="/clusters_2.png" style="width: 500px !important;">
  </figure>
</div>
</div>

---

# Agglomerative clustering

<br>

<figure>
  <img src="/agglomerative_clustering.png" style="width: 900px !important;">
  <figcaption style="color:#b3b3b3ff; font-size: 11px; float: right;">Image source: <a href="https://www.brandidea.com/hierarchicalclustering.html">https://www.brandidea.com/hierarchicalclustering.html</a>
  </figcaption>
</figure>

---

# Dendrogram

<br>
<br>
<div class="grid grid-cols-[4fr_5fr] gap-10">
<div>
<br>

* A **tree diagram** showing the hierarchy of merges
* **Height** of each merge = distance between merged clusters
* **Cutting** the dendrogram at a chosen height → specific number of clusters
* Large **gaps** in merge heights suggest natural cluster boundaries
</div>
<div>
  <figure>
    <img src="/dendrogram_1.png" style="width: 500px !important;">
  </figure>
</div>
</div>

---

# Agglomerative clustering algorithm

<div class="bg-orange-100">

### Algorithm (bottom-up)
   1. Start: each object is its own cluster → $N$ clusters
   2. Compute distance matrix between all pairs of clusters
   3. Repeat until 1 cluster remains:
      1. Find the **two closest** clusters
      2. **Merge** them into one cluster
      3. Update the distance matrix
   4. Record the merge history → **dendrogram**
</div>

<br>

* No need to specify $K$ in advance!
* Choose $K$ later by "cutting" the dendrogram

---
zoom: 0.9
---

# Linkage: distance between clusters

#### **Linkage** defines how we compute distance between two clusters $A$ and $B$:
<br>

| Linkage | Formula | Behavior |
|---------|---------|----------|
| **Single** (min) | $\min\limits_{a \in A, b \in B} \rho(a, b)$ | Can find elongated clusters; sensitive to noise |
| **Complete** (max) | $\max\limits_{a \in A, b \in B} \rho(a, b)$ | Prefers compact, spherical clusters |
| **Average** | $\frac{1}{N_A N_B} \sum\limits_{a,b} \rho(a, b)$ | Compromise between single and complete |
| [**Ward**](https://en.wikipedia.org/wiki/Ward%27s_method) | Minimizes total within-cluster variance | Similar to K-Means; most commonly used |

---

# Linkage comparison

<div>
  <figure>
    <img src="/linkage.png" style="width: 1000px !important;">
  </figure>
</div>

---

# Two approaches to hierarchical clustering

<br>

<div>
  <figure>
    <img src="/agglomerative_vs_divisive.png" style="width: 800px !important;">
      <figcaption style="color:#b3b3b3ff; font-size: 11px; float: right;">Image source: <a href="https://education.yandex.ru/handbook/ml/article/klasterizaciya/">https://education.yandex.ru/handbook/ml/article/klasterizaciya/</a>
    </figcaption>
  </figure>
</div>

---

# Hierarchical clustering: pros and cons

<br>

<div class="grid grid-cols-[1fr_1fr] gap-10">
<div>

### Advantages
* **No need** to specify $K$ upfront
* Dendrogram gives **rich information** about data structure
* Can find **non-spherical** clusters (with single linkage)
* **Deterministic** — no random initialization
</div>
<div>

### Disadvantages
* **Slow**: $O(N^2)$ memory, $O(N^3)$ time
* Not practical for **large datasets** (> 10K points)
* Merges are **irreversible** — early mistakes propagate
* Sensitive to **noise** (especially single linkage)
</div>
</div>
