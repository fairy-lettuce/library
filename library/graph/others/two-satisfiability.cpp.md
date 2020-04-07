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


# :heavy_check_mark: 2-SAT <small>(graph/others/two-satisfiability.cpp)</small>

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#e557c7f962c39680942b9dada22cabec">graph/others</a>
* <a href="{{ site.github.repository_url }}/blob/master/graph/others/two-satisfiability.cpp">View this file on GitHub</a>
    - Last commit date: 2020-04-08 00:50:52+09:00




## Verified with

* :heavy_check_mark: <a href="../../../verify/test/verify/yosupo-two-sat.test.cpp.html">test/verify/yosupo-two-sat.test.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
/**
 * @brief 2-SAT
 */
struct TwoSatisfiability : StronglyConnectedComponents< bool > {
public:
  using StronglyConnectedComponents< bool >::g;
  using StronglyConnectedComponents< bool >::comp;
  using StronglyConnectedComponents< bool >::add_edge;
  size_t sz;

  explicit TwoSatisfiability(size_t v) : sz(v), StronglyConnectedComponents< bool >(v + v) {}

  void add_if(int u, int v) {
    // u -> v <=> !v -> !u
    add_directed_edge(u, v);
    add_directed_edge(rev(v), rev(u));
  }

  void add_or(int u, int v) {
    // u or v <=> !u -> v
    add_if(rev(u), v);
  }

  void add_nand(int u, int v) {
    // u nand v <=> u -> !v
    add_if(u, rev(v));
  }

  void set_true(int u) {
    // u <=> !u -> u
    add_directed_edge(rev(u), u);
  }

  void set_false(int u) {
    // !u <=> u -> !u
    add_directed_edge(u, rev(u));
  }

  inline int rev(int x) {
    if(x >= sz) return x - sz;
    return x + sz;
  }

  vector< int > solve() {
    StronglyConnectedComponents< bool >::build();
    vector< int > ret(sz);
    for(int i = 0; i < sz; i++) {
      if(comp[i] == comp[rev(i)]) return {};
      ret[i] = comp[i] > comp[rev(i)];
    }
    return ret;
  }
};

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "graph/others/two-satisfiability.cpp"
/**
 * @brief 2-SAT
 */
struct TwoSatisfiability : StronglyConnectedComponents< bool > {
public:
  using StronglyConnectedComponents< bool >::g;
  using StronglyConnectedComponents< bool >::comp;
  using StronglyConnectedComponents< bool >::add_edge;
  size_t sz;

  explicit TwoSatisfiability(size_t v) : sz(v), StronglyConnectedComponents< bool >(v + v) {}

  void add_if(int u, int v) {
    // u -> v <=> !v -> !u
    add_directed_edge(u, v);
    add_directed_edge(rev(v), rev(u));
  }

  void add_or(int u, int v) {
    // u or v <=> !u -> v
    add_if(rev(u), v);
  }

  void add_nand(int u, int v) {
    // u nand v <=> u -> !v
    add_if(u, rev(v));
  }

  void set_true(int u) {
    // u <=> !u -> u
    add_directed_edge(rev(u), u);
  }

  void set_false(int u) {
    // !u <=> u -> !u
    add_directed_edge(u, rev(u));
  }

  inline int rev(int x) {
    if(x >= sz) return x - sz;
    return x + sz;
  }

  vector< int > solve() {
    StronglyConnectedComponents< bool >::build();
    vector< int > ret(sz);
    for(int i = 0; i < sz; i++) {
      if(comp[i] == comp[rev(i)]) return {};
      ret[i] = comp[i] > comp[rev(i)];
    }
    return ret;
  }
};

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

