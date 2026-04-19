# Clustering intuition
<br>
<br>
<div class="grid grid-cols-[5fr_4fr] gap-10">
<div>
<br>
<br>

* Each cluster is represented by its
center
* All objects are assigned to the
closest center
* The goal is to find such centers that
form the most compact clusters
</div>
<div>
  <figure>
    <img src="/basics K-Means clustering algorithm.png" style="width: 500px !important;">
    <figcaption style="color:#b3b3b3ff; font-size: 11px; float: right;">Image source: <a href="https://medium.com/@msdasila90/basics-k-means-clustering-algorithm-a77c539c9e00">https://medium.com/@msdasila90/basics-k-means-clustering-algorithm-a77c539c9e00</a>
    </figcaption>
  </figure>
</div>
</div>

---

# K-Means: The Big Idea

<br>

#### Two simple alternating steps:

<div class="grid grid-cols-[1fr_1fr] gap-10">
<div>

### Step 1: Assign
* For each data point, find the **nearest center**
* Assign the point to that cluster
</div>
<div>

### Step 2: Update
* For each cluster, compute the **mean** of all assigned points
* Move the center to this mean
</div>
</div>

<br>

> Repeat until cluster assignments **stop changing**

<br>

*This is an instance of the Expectation-Maximization (EM) algorithm — Andrew Ng, CS229*

---
zoom: 0.9
---

# K-Means algorithm

<div class="bg-orange-100">

### Algorithm
   1. Choose the number of clusters $K$
   2. Randomly initialize $K$ cluster centers $\mu_1, ..., \mu_K$ from training data
   3. Repeat until convergence:
      * **Assign** each object to the nearest center:<br>
         $z_i = \argmin\limits_{k \in \{1, ..., K\}} \lVert x_i - \mu_k \rVert^2$
      * **Update** each center as the mean of its cluster:<br>
         $\mu_k = \frac{1}{|C_k|} \sum\limits_{x_i \in C_k} x_i$
   4. Return cluster assignments $z_1, ..., z_N$
</div>

<br>

* The objective (within-cluster sum of squares, **WCSS**) **decreases** at every step
* K-Means is **guaranteed to converge**, but may find a **local** minimum

---

# Feature scaling matters!

<br>

<div class="grid grid-cols-[1fr_1fr] gap-10">
<div>

### Without scaling
* Feature with **large range dominates** the distance
* Ex: income `0-100K` vs age `0-80`
* Clusters are determined mainly by income
</div>
<div>

### With scaling
* All features contribute **equally** to distance
* **Standardize**: $x' = \frac{x - \bar{x}}{s}$
* Or **normalize** to `[0, 1]` range
</div>
</div>

<br>

> **Always scale your features before running K-Means!**<br>
> This applies to all distance-based methods (kNN, SVM with RBF, etc.)

---
layout: section
---

# K-Means demo

[https://cartography-playground.gitlab.io/playgrounds/clustering-comparison/](https://cartography-playground.gitlab.io/playgrounds/clustering-comparison/)

---
layout: iframe

# K-Means demo
url: https://cartography-playground.gitlab.io/playgrounds/clustering-comparison/
---

---

# The initialization problem

<br>

<div class="grid grid-cols-[3fr_4fr] gap-10">
<div>

### Random initialization
* Different starting centers → **different results**
* Can get stuck in **bad local minima**
* Standard practice: run K-Means **multiple times** with different random seeds, pick result with lowest WCSS
</div>
<div>

### K-Means++ ([Arthur & Vassilvitskii, 2007](https://dl.acm.org/doi/10.5555/1283383.1283494))
* **Smart initialization** that spreads centers apart
* Algorithm:
  1. Pick first center **randomly** from data
  2. For each remaining center: pick a point with probability **proportional to squared distance** from nearest existing center
  3. Run standard K-Means from these seeds
</div>
</div>

<br>

> K-Means++ is the **default** in `scikit-learn` and virtually always preferred

---
zoom: 0.98
---

# Properties of K-Means

* **Hyperparameters:**
   * Number of clusters $K$ must be specified in advance
   * Number of random restarts
* **Convergence:**
   * Guaranteed to converge (WCSS decreases monotonically)
   * Typically converges in **few iterations** — fast!
   * Time complexity: $O(N \cdot K \cdot d \cdot T)$ per restart
* **Limitations:**
   * Finds only **convex**, roughly **spherical** clusters
   * Sensitive to **outliers** — they pull centroids away
   * Result depends on **initialization** (use K-Means++)
   * Must choose $K$ in advance


---

# Choosing K: Elbow method

* How to estimate optimal number of clusters $K$?
* Plot within-cluster sum of squares (WCSS) against $K$
* Look for the **"elbow"** — point where adding more clusters gives **diminishing returns**

<div>
<figure>
 <img src="/elbow_1.png" style="width: 1000px !important;">
</figure>
</div>

---

# Elbow method

<br>
<br>
<div class="grid grid-cols-[4fr_5fr] gap-10">
<div>

* Within-cluster distances $Q^{(K)}$ decreases with increasing $K$
* At some point, the **rate of decrease** slows down sharply
* This "elbow" suggests the optimal $K$
* Here: $K = 5$ is the elbow
</div>
<div>
  <figure>
    <img src="/elbow_2.png" style="width: 500px !important;">
  </figure>
</div>
</div>

---

# Elbow method: formalization

<br>
<br>
<div class="grid grid-cols-[4fr_5fr] gap-10">
<div>

* Relative change of within-cluster distance:
$$D(K) = \frac{\lvert Q^{(K+1)} - Q^{(K)} \rvert}{\lvert Q^{(K)} - Q^{(K-1)} \rvert}$$
   * Small $D(K)$ → adding cluster $K+1$ doesn't help much
   * **Minimum of $D(K)$** suggests the optimal $K$

</div>
<div>
  <figure>
    <img src="/elbow_3.png" style="width: 500px !important;">
  </figure>
</div>
</div>