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


# :heavy_check_mark: Wavelet-Matrix-Point-Add-Rectangle-Sum <small>(structure/wavelet/wavelet-matrix-point-add-rectangle-sum.cpp)</small>

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#5f498e54a9680c92dbc18487ab14a24d">structure/wavelet</a>
* <a href="{{ site.github.repository_url }}/blob/master/structure/wavelet/wavelet-matrix-point-add-rectangle-sum.cpp">View this file on GitHub</a>
    - Last commit date: 2020-08-14 04:28:43+09:00




## 概要

$2$ 次元平面上にある点の位置が事前に与えられているとき, オンラインである点に対する重みの加算と, 矩形内にある点の重みの総和を効率的に求めるデータ構造.

Wavelet-Matrix-Rectangle-Sum で用いた重みの累積和を持たせた配列をBinary-Indexed-Tree に置き換えると, ある点に対する重みの加算を効率的に行える.

## 使い方
* `WaveletMatrixRectangleSum(v, d)`: 各要素の高さ `v` , 対応する要素の重み `d` >を初期値として構築する.
* `rect_sum(l, r, upper)`: 区間 $[l, r)$ の高さ $[0, upper)$ にある要素の重みの>
総和を返す.
* `rect_sum(l, r, lower, upper)`: 区間 $[l, r)$ の高さ $[lower, upper)$ にある要
素の重みの総和を返す.
* `point_add(k, y, x)`: 要素 $k$ (高さ $y$) の重みに $x$ を加算する.

## 計算量

* 構築: $O(N \log V)$
* クエリ: $O(N \log N \log V)$

$V$ は値の最大値.


## Verified with

* :heavy_check_mark: <a href="../../../verify/test/verify/yosupo-point-add-rectangle-sum.test.cpp.html">test/verify/yosupo-point-add-rectangle-sum.test.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
/*
 * @brief Wavelet-Matrix-Point-Add-Rectangle-Sum
 * @docs docs/wavelet-matrix-point-add-rectangle-sum.md
 */
template< typename T, int MAXLOG, typename D >
struct WaveletMatrixPointAddRectangleSum {
  size_t length;
  SuccinctIndexableDictionary matrix[MAXLOG];
  BinaryIndexedTree< D > ds[MAXLOG];
  int mid[MAXLOG];

  WaveletMatrixPointAddRectangleSum() = default;

  WaveletMatrixPointAddRectangleSum(const vector< T > &v, const vector< D > &d) : length(v.size()) {
    assert(v.size() == d.size());
    vector< int > l(length), r(length), ord(length);
    iota(begin(ord), end(ord), 0);
    vector< D > dd(length);
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
      for(int i = 0; i < length; i++) {
        dd[i] = d[ord[i]];
      }
      ds[level] = BinaryIndexedTree< D >(dd);
    }
  }

  pair< int, int > succ(bool f, int l, int r, int level) {
    return {matrix[level].rank(f, l) + mid[level] * f, matrix[level].rank(f, r) + mid[level] * f};
  }

  // count d[i] s.t. (l <= i < r) && (v[i] < upper)
  D rect_sum(int l, int r, T upper) {
    D ret = 0;
    for(int level = MAXLOG - 1; level >= 0; level--) {
      bool f = ((upper >> level) & 1);
      if(f) ret += ds[level].query(matrix[level].rank(false, r) - 1) - ds[level].query(matrix[level].rank(false, l) - 1);
      tie(l, r) = succ(f, l, r, level);
    }
    return ret;
  }

  D rect_sum(int l, int r, T lower, T upper) {
    return rect_sum(l, r, upper) - rect_sum(l, r, lower);
  }

  void point_add(int k, T y, const D &x) {
    for(int level = MAXLOG - 1; level >= 0; level--) {
      bool f = ((y >> level) & 1);
      k = matrix[level].rank(f, k) + mid[level] * f;
      ds[level].add(k, x);
    }
  }
};

template< typename T, int MAXLOG, typename D >
struct CompressedWaveletMatrixPointAddRectangleSum {
  WaveletMatrixPointAddRectangleSum< int, MAXLOG, D > mat;
  vector< T > ys;

  CompressedWaveletMatrixPointAddRectangleSum(const vector< T > &v, const vector< D > &d) : ys(v) {
    sort(begin(ys), end(ys));
    ys.erase(unique(begin(ys), end(ys)), end(ys));
    vector< int > t(v.size());
    for(int i = 0; i < v.size(); i++) t[i] = get(v[i]);
    mat = WaveletMatrixPointAddRectangleSum< int, MAXLOG, D >(t, d);
  }

  inline int get(const T &x) {
    return lower_bound(begin(ys), end(ys), x) - begin(ys);
  }

  D rect_sum(int l, int r, T upper) {
    return mat.rect_sum(l, r, get(upper));
  }

  D rect_sum(int l, int r, T lower, T upper) {
    return mat.rect_sum(l, r, get(lower), get(upper));
  }

  void point_add(int k, T y, const D &x) {
    mat.point_add(k, get(y), x);
  }
};

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "structure/wavelet/wavelet-matrix-point-add-rectangle-sum.cpp"
/*
 * @brief Wavelet-Matrix-Point-Add-Rectangle-Sum
 * @docs docs/wavelet-matrix-point-add-rectangle-sum.md
 */
template< typename T, int MAXLOG, typename D >
struct WaveletMatrixPointAddRectangleSum {
  size_t length;
  SuccinctIndexableDictionary matrix[MAXLOG];
  BinaryIndexedTree< D > ds[MAXLOG];
  int mid[MAXLOG];

  WaveletMatrixPointAddRectangleSum() = default;

  WaveletMatrixPointAddRectangleSum(const vector< T > &v, const vector< D > &d) : length(v.size()) {
    assert(v.size() == d.size());
    vector< int > l(length), r(length), ord(length);
    iota(begin(ord), end(ord), 0);
    vector< D > dd(length);
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
      for(int i = 0; i < length; i++) {
        dd[i] = d[ord[i]];
      }
      ds[level] = BinaryIndexedTree< D >(dd);
    }
  }

  pair< int, int > succ(bool f, int l, int r, int level) {
    return {matrix[level].rank(f, l) + mid[level] * f, matrix[level].rank(f, r) + mid[level] * f};
  }

  // count d[i] s.t. (l <= i < r) && (v[i] < upper)
  D rect_sum(int l, int r, T upper) {
    D ret = 0;
    for(int level = MAXLOG - 1; level >= 0; level--) {
      bool f = ((upper >> level) & 1);
      if(f) ret += ds[level].query(matrix[level].rank(false, r) - 1) - ds[level].query(matrix[level].rank(false, l) - 1);
      tie(l, r) = succ(f, l, r, level);
    }
    return ret;
  }

  D rect_sum(int l, int r, T lower, T upper) {
    return rect_sum(l, r, upper) - rect_sum(l, r, lower);
  }

  void point_add(int k, T y, const D &x) {
    for(int level = MAXLOG - 1; level >= 0; level--) {
      bool f = ((y >> level) & 1);
      k = matrix[level].rank(f, k) + mid[level] * f;
      ds[level].add(k, x);
    }
  }
};

template< typename T, int MAXLOG, typename D >
struct CompressedWaveletMatrixPointAddRectangleSum {
  WaveletMatrixPointAddRectangleSum< int, MAXLOG, D > mat;
  vector< T > ys;

  CompressedWaveletMatrixPointAddRectangleSum(const vector< T > &v, const vector< D > &d) : ys(v) {
    sort(begin(ys), end(ys));
    ys.erase(unique(begin(ys), end(ys)), end(ys));
    vector< int > t(v.size());
    for(int i = 0; i < v.size(); i++) t[i] = get(v[i]);
    mat = WaveletMatrixPointAddRectangleSum< int, MAXLOG, D >(t, d);
  }

  inline int get(const T &x) {
    return lower_bound(begin(ys), end(ys), x) - begin(ys);
  }

  D rect_sum(int l, int r, T upper) {
    return mat.rect_sum(l, r, get(upper));
  }

  D rect_sum(int l, int r, T lower, T upper) {
    return mat.rect_sum(l, r, get(lower), get(upper));
  }

  void point_add(int k, T y, const D &x) {
    mat.point_add(k, get(y), x);
  }
};

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

