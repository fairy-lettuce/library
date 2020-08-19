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


# :heavy_check_mark: Wavelet-Tree(ウェーブレット木) <small>(structure/wavelet/wavelet-tree.cpp)</small>

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#5f498e54a9680c92dbc18487ab14a24d">structure/wavelet</a>
* <a href="{{ site.github.repository_url }}/blob/master/structure/wavelet/wavelet-tree.cpp">View this file on GitHub</a>
    - Last commit date: 2020-08-20 02:29:21+09:00




## 概要

$2$ 次元平面上にある点が事前に与えられているとき, オンラインでいろいろなクエリを処理するデータ構造.

基本的には事前に要素の値を要素数に圧縮する CompressedWaveletTree を用いると高速に動作する.

ウェーブレット行列を用いたほうが時間と空間の計算量が良いため, 使い所なし. 悲しい.

## 使い方
* `WaveletTree(v)`: 各要素の高さ `v` を初期値として構築する.
* `rank(x, r)`: 区間 $[0, r)$ に含まれる `x` の個数を返す.
* `kth_smallest(l, r, k)`: 区間 $[l, r)$ に含まれる要素のうち $k$ 番目(0-indexed) に小さいものを返す.
* `kth_largest(l, r, k)`: 区間 $[l, r)$ に含まれる要素のうち $k$ 番目 (0-indexed) に大きいものを返す.
* `range_freq(l, r, lower, upper)`: 区間 $[l, r)$ に含まれる要素のうち $[lower, upper)$ である要素数を返す.
* `prev_value(l, r, upper)`: 区間 $[l, r)$ に含まれる要素のうち `upper` の次に小さいものを返す.
* `next_value(l, r, lower)`: 区間 $[l, r)$ に含まれる要素のうち `lower` の次に大きいものを返す.

## 計算量

* 構築: $O(N \log V)$
* クエリ: $O(\log V)$

$V$ は値の最大値.


## Verified with

* :heavy_check_mark: <a href="../../../verify/test/verify/aoj-1549-2.test.cpp.html">test/verify/aoj-1549-2.test.cpp</a>
* :heavy_check_mark: <a href="../../../verify/test/verify/aoj-2674-2.test.cpp.html">test/verify/aoj-2674-2.test.cpp</a>
* :heavy_check_mark: <a href="../../../verify/test/verify/yosupo-range-kth-smallest-2.test.cpp.html">test/verify/yosupo-range-kth-smallest-2.test.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
/*
 * @brief Wavelet-Tree(ウェーブレット木)
 * @docs docs/wavelet-tree.md
 */
template< typename T, int MAXLOG >
struct WaveletTree {

  struct Node {
    SuccinctIndexableDictionary sid;
    Node *ch[2];

    Node() = default;

    Node(size_t length) : sid(length + 1), ch{nullptr} {}

  };

  Node *root;

  Node *build(vector< T > &v, vector< T > &rbuff, int bit, int l, int r) {
    if(l >= r || bit == -1) return nullptr;
    Node *node = new Node(r - l);
    int left = 0, right = 0;
    for(int k = l; k < r; k++) {
      if(((v[k] >> bit) & 1)) {
        rbuff[right++] = v[k];
        node->sid.set(k - l);
      } else {
        v[l + left++] = v[k];
      }
    }
    for(int k = 0; k < right; k++) {
      v[l + left + k] = rbuff[k];
    }
    node->sid.build();
    node->ch[0] = build(v, rbuff, bit - 1, l, l + left);
    node->ch[1] = build(v, rbuff, bit - 1, l + left, r);
    return node;
  }

  WaveletTree() = default;

  WaveletTree(vector< T > v) {
    vector< T > rbuff(v.size());
    root = build(v, rbuff, MAXLOG - 1, 0, v.size());
  }

  int rank(Node *t, int l, int r, const T &x, int level) {
    if(l >= r || t == nullptr) return 0;
    if(level == -1) return r - l;
    bool f = (x >> level) & 1;
    l = t->sid.rank(f, l), r = t->sid.rank(f, r);
    return rank(t->ch[f], l, r, x, level - 1);
  }

  int rank(const T &x, int r) {
    return rank(root, 0, r, x, MAXLOG - 1);
  }

  T kth_smallest(Node *t, int l, int r, int k, int level) {
    if(l >= r || t == nullptr) return 0;
    int cnt = t->sid.rank(false, r) - t->sid.rank(false, l);
    bool f = cnt <= k;
    l = t->sid.rank(f, l), r = t->sid.rank(f, r);
    if(f) return kth_smallest(t->ch[f], l, r, k - cnt, level - 1) | ((T(1) << level));
    return kth_smallest(t->ch[f], l, r, k, level - 1);
  }

  // k-th(0-indexed) smallest number in v[l,r)
  T kth_smallest(int l, int r, int k) {
    assert(0 <= k && k < r - l);
    return kth_smallest(root, l, r, k, MAXLOG - 1);
  }

  // k-th(0-indexed) largest number in v[l,r)
  T kth_largest(int l, int r, int k) {
    return kth_smallest(l, r, r - l - k - 1);
  }

  int range_freq(Node *t, int l, int r, T upper, int level) {
    if(t == nullptr || l >= r) return 0;
    bool f = ((upper >> level) & 1);
    int ret = 0;
    if(f) ret += t->sid.rank(false, r) - t->sid.rank(false, l);
    l = t->sid.rank(f, l), r = t->sid.rank(f, r);
    return range_freq(t->ch[f], l, r, upper, level - 1) + ret;
  }

  // count i s.t. (l <= i < r) && (v[i] < upper)
  int range_freq(int l, int r, T upper) {
    return range_freq(root, l, r, upper, MAXLOG - 1);
  }

  // count i s.t. (l <= i < r) && (lower <= v[i] < upper)
  int range_freq(int l, int r, T lower, T upper) {
    return range_freq(l, r, upper) - range_freq(l, r, lower);
  }

  // max v[i] s.t. (l <= i < r) && (v[i] < upper)
  T prev_value(int l, int r, T upper) {
    int cnt = range_freq(l, r, upper);
    return cnt == 0 ? T(-1) : kth_smallest(l, r, cnt - 1);
  }

  // min v[i] s.t. (l <= i < r) && (lower <= v[i])
  T next_value(int l, int r, T lower) {
    int cnt = range_freq(l, r, lower);
    return cnt == r - l ? T(-1) : kth_smallest(l, r, cnt);
  }
};

template< typename T, int MAXLOG >
struct CompressedWaveletTree {
  WaveletTree< int, MAXLOG > mat;
  vector< T > ys;

  CompressedWaveletTree(const vector< T > &v) : ys(v) {
    sort(begin(ys), end(ys));
    ys.erase(unique(begin(ys), end(ys)), end(ys));
    vector< int > t(v.size());
    for(int i = 0; i < v.size(); i++) t[i] = get(v[i]);
    mat = WaveletTree< int, MAXLOG >(t);
  }

  inline int get(const T &x) {
    return lower_bound(begin(ys), end(ys), x) - begin(ys);
  }

  int rank(const T &x, int r) {
    auto pos = get(x);
    if(pos == ys.size() || ys[pos] != x) return 0;
    return mat.rank(pos, r);
  }

  T kth_smallest(int l, int r, int k) {
    return ys[mat.kth_smallest(l, r, k)];
  }

  T kth_largest(int l, int r, int k) {
    return ys[mat.kth_largest(l, r, k)];
  }

  int range_freq(int l, int r, T upper) {
    return mat.range_freq(l, r, get(upper));
  }

  int range_freq(int l, int r, T lower, T upper) {
    return mat.range_freq(l, r, get(lower), get(upper));
  }

  T prev_value(int l, int r, T upper) {
    auto ret = mat.prev_value(l, r, get(upper));
    return ret == -1 ? T(-1) : ys[ret];
  }

  T next_value(int l, int r, T lower) {
    auto ret = mat.next_value(l, r, get(lower));
    return ret == -1 ? T(-1) : ys[ret];
  }
};


```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "structure/wavelet/wavelet-tree.cpp"
/*
 * @brief Wavelet-Tree(ウェーブレット木)
 * @docs docs/wavelet-tree.md
 */
template< typename T, int MAXLOG >
struct WaveletTree {

  struct Node {
    SuccinctIndexableDictionary sid;
    Node *ch[2];

    Node() = default;

    Node(size_t length) : sid(length + 1), ch{nullptr} {}

  };

  Node *root;

  Node *build(vector< T > &v, vector< T > &rbuff, int bit, int l, int r) {
    if(l >= r || bit == -1) return nullptr;
    Node *node = new Node(r - l);
    int left = 0, right = 0;
    for(int k = l; k < r; k++) {
      if(((v[k] >> bit) & 1)) {
        rbuff[right++] = v[k];
        node->sid.set(k - l);
      } else {
        v[l + left++] = v[k];
      }
    }
    for(int k = 0; k < right; k++) {
      v[l + left + k] = rbuff[k];
    }
    node->sid.build();
    node->ch[0] = build(v, rbuff, bit - 1, l, l + left);
    node->ch[1] = build(v, rbuff, bit - 1, l + left, r);
    return node;
  }

  WaveletTree() = default;

  WaveletTree(vector< T > v) {
    vector< T > rbuff(v.size());
    root = build(v, rbuff, MAXLOG - 1, 0, v.size());
  }

  int rank(Node *t, int l, int r, const T &x, int level) {
    if(l >= r || t == nullptr) return 0;
    if(level == -1) return r - l;
    bool f = (x >> level) & 1;
    l = t->sid.rank(f, l), r = t->sid.rank(f, r);
    return rank(t->ch[f], l, r, x, level - 1);
  }

  int rank(const T &x, int r) {
    return rank(root, 0, r, x, MAXLOG - 1);
  }

  T kth_smallest(Node *t, int l, int r, int k, int level) {
    if(l >= r || t == nullptr) return 0;
    int cnt = t->sid.rank(false, r) - t->sid.rank(false, l);
    bool f = cnt <= k;
    l = t->sid.rank(f, l), r = t->sid.rank(f, r);
    if(f) return kth_smallest(t->ch[f], l, r, k - cnt, level - 1) | ((T(1) << level));
    return kth_smallest(t->ch[f], l, r, k, level - 1);
  }

  // k-th(0-indexed) smallest number in v[l,r)
  T kth_smallest(int l, int r, int k) {
    assert(0 <= k && k < r - l);
    return kth_smallest(root, l, r, k, MAXLOG - 1);
  }

  // k-th(0-indexed) largest number in v[l,r)
  T kth_largest(int l, int r, int k) {
    return kth_smallest(l, r, r - l - k - 1);
  }

  int range_freq(Node *t, int l, int r, T upper, int level) {
    if(t == nullptr || l >= r) return 0;
    bool f = ((upper >> level) & 1);
    int ret = 0;
    if(f) ret += t->sid.rank(false, r) - t->sid.rank(false, l);
    l = t->sid.rank(f, l), r = t->sid.rank(f, r);
    return range_freq(t->ch[f], l, r, upper, level - 1) + ret;
  }

  // count i s.t. (l <= i < r) && (v[i] < upper)
  int range_freq(int l, int r, T upper) {
    return range_freq(root, l, r, upper, MAXLOG - 1);
  }

  // count i s.t. (l <= i < r) && (lower <= v[i] < upper)
  int range_freq(int l, int r, T lower, T upper) {
    return range_freq(l, r, upper) - range_freq(l, r, lower);
  }

  // max v[i] s.t. (l <= i < r) && (v[i] < upper)
  T prev_value(int l, int r, T upper) {
    int cnt = range_freq(l, r, upper);
    return cnt == 0 ? T(-1) : kth_smallest(l, r, cnt - 1);
  }

  // min v[i] s.t. (l <= i < r) && (lower <= v[i])
  T next_value(int l, int r, T lower) {
    int cnt = range_freq(l, r, lower);
    return cnt == r - l ? T(-1) : kth_smallest(l, r, cnt);
  }
};

template< typename T, int MAXLOG >
struct CompressedWaveletTree {
  WaveletTree< int, MAXLOG > mat;
  vector< T > ys;

  CompressedWaveletTree(const vector< T > &v) : ys(v) {
    sort(begin(ys), end(ys));
    ys.erase(unique(begin(ys), end(ys)), end(ys));
    vector< int > t(v.size());
    for(int i = 0; i < v.size(); i++) t[i] = get(v[i]);
    mat = WaveletTree< int, MAXLOG >(t);
  }

  inline int get(const T &x) {
    return lower_bound(begin(ys), end(ys), x) - begin(ys);
  }

  int rank(const T &x, int r) {
    auto pos = get(x);
    if(pos == ys.size() || ys[pos] != x) return 0;
    return mat.rank(pos, r);
  }

  T kth_smallest(int l, int r, int k) {
    return ys[mat.kth_smallest(l, r, k)];
  }

  T kth_largest(int l, int r, int k) {
    return ys[mat.kth_largest(l, r, k)];
  }

  int range_freq(int l, int r, T upper) {
    return mat.range_freq(l, r, get(upper));
  }

  int range_freq(int l, int r, T lower, T upper) {
    return mat.range_freq(l, r, get(lower), get(upper));
  }

  T prev_value(int l, int r, T upper) {
    auto ret = mat.prev_value(l, r, get(upper));
    return ret == -1 ? T(-1) : ys[ret];
  }

  T next_value(int l, int r, T lower) {
    auto ret = mat.next_value(l, r, get(lower));
    return ret == -1 ? T(-1) : ys[ret];
  }
};


```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

