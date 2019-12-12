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


# :warning: structure/union-find/weighted-union-find.cpp
<a href="../../../index.html">Back to top page</a>

* category: structure/union-find
* <a href="{{ site.github.repository_url }}/blob/master/structure/union-find/weighted-union-find.cpp">View this file on GitHub</a>
    - Last commit date: 2019-11-30 22:41:48 +0900




## Verified With
* :warning: <a href="../../../verify/test/verify/aoj-dsl-1-b.test.cpp.html">test/verify/aoj-dsl-1-b.test.cpp</a>


## Code
{% raw %}
```cpp
template< typename T >
struct WeightedUnionFind {
  vector< int > data;
  vector< T > ws;

  WeightedUnionFind() {}

  WeightedUnionFind(int sz) : data(sz, -1), ws(sz) {}

  int find(int k) {
    if(data[k] < 0) return k;
    auto par = find(data[k]);
    ws[k] += ws[data[k]];
    return data[k] = par;
  }

  T weight(int t) {
    find(t);
    return ws[t];
  }

  bool unite(int x, int y, T w) {
    w += weight(x);
    w -= weight(y);
    x = find(x), y = find(y);
    if(x == y) return false;
    if(data[x] > data[y]) {
      swap(x, y);
      w *= -1;
    }
    data[x] += data[y];
    data[y] = x;
    ws[y] = w;
    return true;
  }

  T diff(int x, int y) {
    return weight(y) - weight(x);
  }
};

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

