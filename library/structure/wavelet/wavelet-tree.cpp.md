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


# :heavy_check_mark: structure/wavelet/wavelet-tree.cpp

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#5f498e54a9680c92dbc18487ab14a24d">structure/wavelet</a>
* <a href="{{ site.github.repository_url }}/blob/master/structure/wavelet/wavelet-tree.cpp">View this file on GitHub</a>
    - Last commit date: 2019-12-31 16:31:54+09:00




## Verified with

* :heavy_check_mark: <a href="../../../verify/test/verify/aoj-2674-2.test.cpp.html">test/verify/aoj-2674-2.test.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
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


  WaveletTree(vector< T > v) {
    vector< T > rbuff(v.size());
    root = build(v, rbuff, MAXLOG - 1, 0, v.size());
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
};

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "structure/wavelet/wavelet-tree.cpp"
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


  WaveletTree(vector< T > v) {
    vector< T > rbuff(v.size());
    root = build(v, rbuff, MAXLOG - 1, 0, v.size());
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
};

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

