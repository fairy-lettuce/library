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


# :question: Block-Cut-Tree <small>(graph/others/block-cut-tree.cpp)</small>

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#e557c7f962c39680942b9dada22cabec">graph/others</a>
* <a href="{{ site.github.repository_url }}/blob/master/graph/others/block-cut-tree.cpp">View this file on GitHub</a>
    - Last commit date: 2020-03-25 22:02:49+09:00


* see: <a href="https://ei1333.hateblo.jp/entry/2020/03/25/010057">https://ei1333.hateblo.jp/entry/2020/03/25/010057</a>


## Verified with

* :x: <a href="../../../verify/test/verify/aoj-3022.test.cpp.html">test/verify/aoj-3022.test.cpp</a>
* :heavy_check_mark: <a href="../../../verify/test/verify/aoj-3139.test.cpp.html">test/verify/aoj-3139.test.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
/**
 * @brief Block-Cut-Tree
 * @see https://ei1333.hateblo.jp/entry/2020/03/25/010057
 */
template< typename T = int >
struct BlockCutTree : BiConnectedComponents< T > {
public:
  using BiConnectedComponents< T >::BiConnectedComponents;
  using BiConnectedComponents< T >::g;
  using BiConnectedComponents< T >::articulation;
  using BiConnectedComponents< T >::bc;

  vector< int > rev;
  vector< vector< int > > group;
  Graph< T > tree;

  explicit BlockCutTree(const Graph< T > &g) : Graph< T >(g) {}

  int operator[](const int &k) const {
    return rev[k];
  }

  void build() override {
    BiConnectedComponents< T >::build();
    rev.assign(g.size(), -1);
    int ptr = (int) bc.size();
    for(auto &idx : articulation) {
      rev[idx] = ptr++;
    }
    vector< int > last(ptr, -1);
    tree = Graph< T >(ptr);
    for(int i = 0; i < (int) bc.size(); i++) {
      for(auto &e : bc[i]) {
        for(auto &ver : {e.from, e.to}) {
          if(rev[ver] >= (int) bc.size()) {
            if(exchange(last[rev[ver]], i) != i) {
              tree.add_edge(rev[ver], i, e.cost);
            }
          } else {
            rev[ver] = i;
          }
        }
      }
    }
    group.resize(ptr);
    for(int i = 0; i < (int) g.size(); i++) {
      group[rev[i]].emplace_back(i);
    }
  }
};

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "graph/others/block-cut-tree.cpp"
/**
 * @brief Block-Cut-Tree
 * @see https://ei1333.hateblo.jp/entry/2020/03/25/010057
 */
template< typename T = int >
struct BlockCutTree : BiConnectedComponents< T > {
public:
  using BiConnectedComponents< T >::BiConnectedComponents;
  using BiConnectedComponents< T >::g;
  using BiConnectedComponents< T >::articulation;
  using BiConnectedComponents< T >::bc;

  vector< int > rev;
  vector< vector< int > > group;
  Graph< T > tree;

  explicit BlockCutTree(const Graph< T > &g) : Graph< T >(g) {}

  int operator[](const int &k) const {
    return rev[k];
  }

  void build() override {
    BiConnectedComponents< T >::build();
    rev.assign(g.size(), -1);
    int ptr = (int) bc.size();
    for(auto &idx : articulation) {
      rev[idx] = ptr++;
    }
    vector< int > last(ptr, -1);
    tree = Graph< T >(ptr);
    for(int i = 0; i < (int) bc.size(); i++) {
      for(auto &e : bc[i]) {
        for(auto &ver : {e.from, e.to}) {
          if(rev[ver] >= (int) bc.size()) {
            if(exchange(last[rev[ver]], i) != i) {
              tree.add_edge(rev[ver], i, e.cost);
            }
          } else {
            rev[ver] = i;
          }
        }
      }
    }
    group.resize(ptr);
    for(int i = 0; i < (int) g.size(); i++) {
      group[rev[i]].emplace_back(i);
    }
  }
};

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

