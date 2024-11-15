# Problem Explanation

### Definitions

- **Cost to reduce a sub-array:**  
  `g(l, r)`: The cost to reduce the sub-array `A[l...r]` to a single element.  
  The result for the entire array is `g(1, n)`.

- **Cost to shrink a sub-array:**  
  `f(l, r, z)`: The cost to shrink the sub-array `A[l...r]` to a `z`-sized sub-array, where `z <= r - l + 1`.

### Base Cases

- `f(l, r, 1) = g(l, r)`: Shrinking a sub-array to size 1 is equivalent to reducing it.

---

### Recursive Relation for `g(l, r)`

For a segment `[l, r]` and a partition point `p` where `l <= p < r`:

1. `[l, p]` reduces to a single element.  
2. `[p+1, r]` shrinks to a sub-array of size `z`, where `1 <= z < k`.

The `z+1` elements are then merged into one with the cost `g(l, r)`.

This can be expressed as:

```
g(l, r) = sum(A[i] for i in range(l, r+1)) + min_p { g(l, p) + min_z { f(p+1, r, z) } }
```

---

### Recursive Formula for `f(l, r, z)`

We can compute `f(l, r, z)` as:

```
f(l, r, z) = min_p { g(l, p) + f(p+1, r, z-1) }
```

---

### Optimization

To optimize the calculation, use a **prefix-minimum array** to store:

```
min_z { f(l, r, z) }
```

This helps speed up the computation of `f(l, r, z)`.

---

### Time Complexity

The overall complexity per test case is:

```
O(n^3 * k)
```

### Space Complexity

The overall space complexity is:

```
O(n^2 * k)
```
