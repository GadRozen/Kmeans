# 🧠 K-Means Clustering in C

### 💡 Overview
This project implements the **K-Means clustering algorithm** entirely in **C**, without any external libraries.  
It demonstrates strong understanding of **memory management**, **numerical computation**, and **algorithm design** in a low-level language.

K-Means is a foundational learning algorithm that partitions data into *k* clusters by minimizing the within-cluster variance (sum of squared distances).

---

## ⚙️ Features
- Pure C implementation — no dependencies, no dynamic arrays.
- Dynamically builds vectors using linked lists for arbitrary input dimensions.
- Handles numeric input directly from `stdin`.
- Performs complete K-Means iteration loop:
  - Assign points to nearest centroid  
  - Recompute centroids as mean of assigned points  
  - Stops early when centroids stabilize (`Δ < EPSILON`)
- Supports configurable number of clusters `k` and maximum iterations.

---

## 🧩 Core Algorithm

1. **Input**  
   Reads data points from standard input, each line representing one vector with comma-separated coordinates.  
   Example:
   ```
   1.0,2.0,3.5
   4.1,0.2,8.9
   2.5,3.0,4.0
   ```

2. **Initialization**  
   The first *k* vectors are chosen as the initial centroids.

3. **Iteration Loop**  
   For up to `iter` iterations (default = 400):
   - Assign each vector to the closest centroid (using **Euclidean distance**).
   - Recompute each centroid as the average of its assigned points.
   - Stop if centroids move less than `EPSILON = 0.001`.

4. **Output**  
   Prints the final centroids, one per line, with coordinates separated by commas.

---

## 🧮 Key Functions
| Function | Description |
|-----------|--------------|
| `delta_between_vectors(a, b)` | Calculates Euclidean distance between two vectors. |
| `add_vector(sum, v)` | Adds two vectors coordinate-wise. |
| `divide_vector(v, n)` | Divides each coordinate by `n` (computes mean). |
| `copy_cords(source)` | Creates a deep copy of a coordinate list. |
| `is_positive_integer(str)` | Validates numeric input for `k` and iterations. |
| `free_cords()` / `free_vectors()` | Frees dynamically allocated memory safely. |

---

## 🧠 Design Highlights
- **Dynamic Linked Lists** for representing vectors of unknown dimensionality.  
  Each vector is a linked list of coordinates (`struct cord`), and the dataset is a linked list of vectors (`struct vector`).
- **Explicit Memory Management** — all allocations are paired with `free()` calls.
- **Robust Input Checking** — rejects invalid or non-positive integers for `k` and `iter`.
- **Numerical Stability** — convergence threshold `EPSILON = 0.001` ensures graceful stopping.
- **Readable Modular Code** — each mathematical step is encapsulated in its own function.

---

## 🚀 Usage

### Compile:
```bash
gcc -Wall -ansi -pedantic -lm kmeans.c -o kmeans
```

### Run:
```bash
./kmeans <k> [max_iter] < data.txt
```

**Example:**
```bash
./kmeans 3 100 < points.txt
```

Output:
```
1.1250,3.5460,2.8000
5.0870,1.2210,8.4560
3.3340,2.1240,5.6780
```

---

## 🧪 Testing Tips
- Validate on simple datasets (e.g. points in 2D clusters).  
- Test edge cases:
  - `k >= n` → should print an error.
  - Non-numeric input → triggers “Incorrect number of clusters!”.
  - Empty input → handled gracefully.
- Verify convergence: small `EPSILON` leads to more accurate centroids, larger to faster termination.

---

## 🧰 Example Input and Output

**Input:**
```
1.0,1.0
1.5,2.0
3.0,4.0
5.0,7.0
3.5,5.0
4.5,5.0
3.5,4.5
```

**Command:**
```bash
./kmeans 2 < points.txt
```

**Output:**
```
1.2500,1.5000
4.1000,5.4000
```

---

## 📈 Complexity
| Step | Time | Space |
|------|------|--------|
| Distance computation | O(n·k·d) | O(d) |
| Update centroids | O(n·d) | O(k·d) |
| Overall | **O(iter · n · k · d)** | O(n + k·d) |

Where `n` = number of points, `k` = clusters, `d` = dimensions.

---

## 👩‍💻 Author
**Gad Rozen** 
Developed as part of the *Software project* course.

---

## 📜 License
For academic and interview demonstration use.  

