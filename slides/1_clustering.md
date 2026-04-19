# Supervised vs Unsupervised Learning

<br>
<div class="grid grid-cols-[1fr_1fr] gap-10">
<div>

### Supervised Learning
* We have features $X$ **and** labels $y$
* Goal: learn $f(X) \approx y$
* Examples you've seen:
  * Linear/logistic regression
  * Decision trees, SVMs, kNN
* **"Teacher"** provides correct answers
</div>
<div>

### Unsupervised Learning
* We have **only** features $X$, **no** labels $y$
* Goal: discover **hidden structure** in data
* Key tasks:
  * **Clustering** — group similar objects
  * **Dimensionality reduction** — compress features
  * **Anomaly detection** — find outliers
* No "correct answer" to evaluate against
</div>
</div>

---

# Why Unsupervised Learning?

### Real-world applications of clustering:

* **Customer segmentation** — group customers by behavior for targeted marketing
* **Image compression** — reduce colors by clustering pixel values (Andrew Ng, CS229)
* **Document organization** — group news articles or emails by topic
* **Genomics** — identify groups of genes with similar expression patterns
* **Anomaly detection** — fraud detection, network intrusion detection
* **Social network analysis** — community detection in graphs

<br>

> *"Most of the data in the world is unlabeled. Learning from unlabeled data is one of the most important long-term challenges."* — **Andrew Ng**

---

# Clustering vs classification

<br>
<br>
<div class="grid grid-cols-[5fr_4fr] gap-10">
<div>

* In **classification**, we have object
features $X$ and class labels $y \in \{0, 1\}$
* A classifier learns decision rule $f$,<br> so
that $f(X) \approx y$
* The trained classifier predicts class
labels for new objects
</div>
<div>
  <figure>
    <img src="/classification_example.png" style="width: 500px !important;">
    <figcaption style="color:#b3b3b3ff; font-size: 11px; float: right;"><span>Classification example</span>
    </figcaption>
  </figure>
</div>
</div>

---

# Clustering vs classification

<br>
<br>
<div class="grid grid-cols-[5fr_4fr] gap-10">
<div>

* In **clustering**, we don’t have class
labels $y$
* The goal is to divide all objects into
separate groups using only object
features $X$
* Objects inside groups are **similar**
* Objects from different groups are
**dissimilar**
</div>
<div>
  <figure>
    <img src="/clustering_example.png" style="width: 500px !important;">
    <figcaption style="color:#b3b3b3ff; font-size: 11px; float: right;"><span>Clustering example</span>
    </figcaption>
  </figure>
</div>
</div>

---

# Clustering example

<div>
  <figure>
    <img src="/em_clusters_example.png" style="width: 400px !important;">
<!--     <figcaption style="color:#b3b3b3ff; font-size: 11px; float: center;"><span>
    Clusters in electromagnetic calorimeter of KTeV experiment for $K \rightarrow \pi^0 \pi^0$ decay
  </span>
    </figcaption> -->
  </figure>
</div>
<div style="color:#b3b3b3ff; font-size: 11px; float: center;">

Clusters in electromagnetic calorimeter of KTeV experiment for $\textcolor{#B3B3B3}{K \rightarrow \pi^0 \pi^0}$ decay
  </div>

---

# Clustering assumptions

#### Most clustering algorithms rely on the following assumptions:

* Objects form **dense groups** (clusters) in feature space
* Objects within one cluster are **similar** to each other
* Objects from different clusters are **dissimilar**
* Similarity is typically measured by a **distance function**
* Distances between neighbors **within** a cluster < distances **between** clusters

<br>

#### Key question: How do we define "similar"?
* Euclidean distance, Manhattan distance, cosine similarity, ...
* Choice of distance metric **significantly affects** clustering results