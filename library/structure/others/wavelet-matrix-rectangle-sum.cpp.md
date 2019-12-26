---
layout: default
---

<!-- mathjax config similar to math.stackexchange -->
<script type="text/javascript" async
  src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.5/MathJax.js?config=TeX-MML-AM_CHTML">
</script>
<script type="text/x-mathjax-config">
  MathJax.Hub.Config({
    TeX: { equationNumbers: { autoNumber: "AMS" }},
    tex2jax: {
      inlineMath: [ ['$','$'] ],
      processEscapes: true
    },
    "HTML-CSS": { matchFontHeight: false },
    displayAlign: "left",
    displayIndent: "2em"
  });
</script>

<script type="text/javascript" src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.4.1/jquery.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/jquery-balloon-js@1.1.2/jquery.balloon.min.js" integrity="sha256-ZEYs9VrgAeNuPvs15E39OsyOJaIkXEEt10fzxJ20+2I=" crossorigin="anonymous"></script>
<script type="text/javascript" src="../../../assets/js/copy-button.js"></script>
<link rel="stylesheet" href="../../../assets/css/copy-button.css" />


# :heavy_check_mark: structure/others/wavelet-matrix-rectangle-sum.cpp

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#40d73e22b7d986e3399449c25c8b23a1">structure/others</a>
* <a href="{{ site.github.repository_url }}/blob/master/structure/others/wavelet-matrix-rectangle-sum.cpp">View this file on GitHub</a>
    - Last commit date: 2019-12-27 01:39:33+09:00




## Verified with

* :heavy_check_mark: <a href="../../../verify/test/verify/yosupo-rectangle-sum.test.cpp.html">test/verify/yosupo-rectangle-sum.test.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
template< typename T, int MAXLOG, typename D >
struct WaveletMatrixRectangleSum {
  size_t length;
  SuccinctIndexableDictionary matrix[MAXLOG];
  vector< D > ds[MAXLOG];
  int mid[MAXLOG];

  WaveletMatrixRectangleSum(const vector< T > &v, const vector< D > &d) : length(v.size()) {
    assert(v.size() == d.size());
    vector< int > l(length), r(length), ord(length);
    iota(begin(ord), end(ord), 0);
    for(int level = MAXLOG - 1; level >= 0; level--) {
      matrix[level] = SuccinctIndexableDictionary(length + 1);
      int left = 0, right = 0;
      for(int i = 0; i < length; i++) {
        if(((v[ord[i]] >> level) & 1)) {
          matrix[level].set(i);
          r[right++] = ord[i];
        } else {
          l[left++] = ord[i];
        }
      }
      mid[level] = left;
      matrix[level].build();
      ord.swap(l);
      for(int i = 0; i < right; i++) {
        ord[left + i] = r[i];
      }
      ds[level].resize(length + 1);
      ds[level][0] = D();
      for(int i = 0; i < length; i++) {
        ds[level][i + 1] = ds[level][i] + d[ord[i]];
      }
    }
  }

  pair< int, int > succ(bool f, int l, int r, int level) {
    return {matrix[level].rank(f, l) + mid[level] * f, matrix[level].rank(f, r) + mid[level] * f};
  }

  // count d[i] s.t. (l <= i < r) && (v[i] < upper)
  D range_sum(int l, int r, T upper) {
    D ret = 0;
    for(int level = MAXLOG - 1; level >= 0; level--) {
      bool f = ((upper >> level) & 1);
      if(f) ret += ds[level][matrix[level].rank(false, r)] - ds[level][matrix[level].rank(false, l)];
      tie(l, r) = succ(f, l, r, level);
    }
    return ret;
  }

  D range_sum(int l, int r, T lower, T upper) {
    return range_sum(l, r, upper) - range_sum(l, r, lower);
  }
};


```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "structure/others/wavelet-matrix-rectangle-sum.cpp"
template< typename T, int MAXLOG, typename D >
struct WaveletMatrixRectangleSum {
  size_t length;
  SuccinctIndexableDictionary matrix[MAXLOG];
  vector< D > ds[MAXLOG];
  int mid[MAXLOG];

  WaveletMatrixRectangleSum(const vector< T > &v, const vector< D > &d) : length(v.size()) {
    assert(v.size() == d.size());
    vector< int > l(length), r(length), ord(length);
    iota(begin(ord), end(ord), 0);
    for(int level = MAXLOG - 1; level >= 0; level--) {
      matrix[level] = SuccinctIndexableDictionary(length + 1);
      int left = 0, right = 0;
      for(int i = 0; i < length; i++) {
        if(((v[ord[i]] >> level) & 1)) {
          matrix[level].set(i);
          r[right++] = ord[i];
        } else {
          l[left++] = ord[i];
        }
      }
      mid[level] = left;
      matrix[level].build();
      ord.swap(l);
      for(int i = 0; i < right; i++) {
        ord[left + i] = r[i];
      }
      ds[level].resize(length + 1);
      ds[level][0] = D();
      for(int i = 0; i < length; i++) {
        ds[level][i + 1] = ds[level][i] + d[ord[i]];
      }
    }
  }

  pair< int, int > succ(bool f, int l, int r, int level) {
    return {matrix[level].rank(f, l) + mid[level] * f, matrix[level].rank(f, r) + mid[level] * f};
  }

  // count d[i] s.t. (l <= i < r) && (v[i] < upper)
  D range_sum(int l, int r, T upper) {
    D ret = 0;
    for(int level = MAXLOG - 1; level >= 0; level--) {
      bool f = ((upper >> level) & 1);
      if(f) ret += ds[level][matrix[level].rank(false, r)] - ds[level][matrix[level].rank(false, l)];
      tie(l, r) = succ(f, l, r, level);
    }
    return ret;
  }

  D range_sum(int l, int r, T lower, T upper) {
    return range_sum(l, r, upper) - range_sum(l, r, lower);
  }
};


```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

