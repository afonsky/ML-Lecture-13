# Intuition

#### Density-Based Spatial Clustering of Applications with Noise (DBSCAN)
<br>
<div class="grid grid-cols-[5fr_4fr] gap-10">
<div>
<br>
<br>

* It supposed that clusters form dense groups of objects
* Areas between the clusters are sparse, with very low densities
* Let’s start from a random object and grow up a cluster by adding neighbor objects within some radius
</div>
<div>
  <figure>
    <img src="/dbscan_cluster.png" style="width: 500px !important;">
  </figure>
</div>
</div>

---

# DBSCAN parameters

<br>
<div class="grid grid-cols-[5fr_4fr] gap-10">
<div>
<br>
<br>

#### DBSCAN has two parameters:
* $\epsilon$ — radius of the neighborhood
* **MinPts** — minimum number of points required to form a dense region

<br>

#### Rules of thumb:
* $\mathrm{MinPts} \geq d + 1$ where $d$ is number of features
* Common default: $\mathrm{MinPts} = 5$
</div>
<div>
  <figure>
    <img src="/dbscan_1.png" style="width: 500px !important;">
  </figure>
</div>
</div>

---

# DBSCAN: three types of points

<br>
<div class="grid grid-cols-[5fr_4fr] gap-10">
<div>
<br>
<br>

#### Three types of objects:
* <span style="color:#6E1B1A">**Core**</span>: has $\geq$ **MinPts** objects within $\epsilon$ neighborhood
* <span style="color:#9F8544">**Border**</span>: not <span style="color:#6E1B1A">**core**</span> object, has at least $1$ <span style="color:#6E1B1A">**core**</span> object within its $\epsilon$ neighborhood
* <span style="color:#07227C">**Noise**</span>: neither a <span style="color:#6E1B1A">**core**</span> nor a <span style="color:#9F8544">**border**</span> object

</div>
<div>
  <figure>
    <img src="/dbscan_1.png" style="width: 500px !important;">
  </figure>
</div>
</div>

---

# DBSCAN algorithm

<br>
<br>
<br>

<div class="bg-orange-100">

### Algorithm
   1. Label all objects as <span style="color:#6E1B1A">**core**</span>, <span style="color:#9F8544">**border**</span>, or <span style="color:#07227C">**noise**</span> objects
   2. Remove <span style="color:#07227C">**noise**</span> objects
   3. Connect all <span style="color:#6E1B1A">**core**</span> objects within $\epsilon$ of each other
   4. Each connected component of <span style="color:#6E1B1A">**core**</span> objects forms a **cluster**
   5. Assign each <span style="color:#9F8544">**border**</span> object to the nearest <span style="color:#6E1B1A">**core**</span> object's cluster
</div>

---

# Choosing $\epsilon$: k-distance graph

<br>

#### How to pick a good $\epsilon$?

1. For each point, compute distance to its $k$-th nearest neighbor ($k$ = MinPts)
2. Sort these distances in **increasing** order and plot them
3. Look for the **"elbow"** — the $\epsilon$ at which distances start increasing rapidly

<br>

* Points **before** the elbow are in dense regions (clusters)
* Points **after** the elbow are in sparse regions (noise)
* The elbow point gives a good estimate for $\epsilon$

---
layout: section
---

# DBSCAN demo

[https://www.naftaliharris.com/blog/visualizing-dbscan-clustering/](https://www.naftaliharris.com/blog/visualizing-dbscan-clustering/)

---
layout: iframe

url: https://www.naftaliharris.com/blog/visualizing-dbscan-clustering/
---

---

# DBSCAN: pros and cons

<br>

<div class="grid grid-cols-[1fr_1fr] gap-10">
<div>

### Advantages
* **No need** to specify $K$ — number of clusters is estimated automatically
* Finds clusters of **arbitrary shape**
* **Robust to outliers** — labels them as noise
* Only **two** parameters ($\epsilon$, MinPts)
</div>
<div>

### Disadvantages
* Struggles with **varying densities** — one $\epsilon$ doesn't fit all
* Sensitive to **parameter choices**
* Not suitable for **high-dimensional** data (distances become similar)
* Border points can be **non-deterministic**
</div>
</div>