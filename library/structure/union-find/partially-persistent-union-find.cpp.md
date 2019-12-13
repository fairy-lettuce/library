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


# :warning: structure/union-find/partially-persistent-union-find.cpp
<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#16695eacefd17254ea5bccf40066c856">structure/union-find</a>
* <a href="{{ site.github.repository_url }}/blob/master/structure/union-find/partially-persistent-union-find.cpp">View this file on GitHub</a>
    - Last commit date: 2019-11-30 22:41:48 +0900




## Code
{% raw %}
```cpp
struct PartiallyPersistentUnionFind {
  vector< int > data;
  vector< int > last;
  vector< vector< pair< int, int > > > add;

  PartiallyPersistentUnionFind() {}

  PartiallyPersistentUnionFind(int sz) : data(sz, -1), last(sz, 1e9), add(sz) {
    for(auto &vs : add) vs.emplace_back(-1, -1);
  }

  bool unite(int t, int x, int y) {
    x = find(t, x);
    y = find(t, y);
    if(x == y) return false;
    if(data[x] > data[y]) swap(x, y);
    data[x] += data[y];
    add[x].emplace_back(t, data[x]);
    data[y] = x;
    last[y] = t;
    return true;
  }

  int find(int t, int x) {
    if(t < last[x]) return x;
    return find(t, data[x]);
  }

  int size(int t, int x) {
    x = find(t, x);
    return -prev(lower_bound(begin(add[x]), end(add[x]), make_pair(t, 0)))->second;
  }
};

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

