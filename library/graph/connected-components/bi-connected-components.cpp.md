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


# :heavy_check_mark: Bi-Connected-Components(二重頂点連結成分分解) <small>(graph/connected-components/bi-connected-components.cpp)</small>

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#3a7c46e10de1b2cce1293b2074b86f0a">graph/connected-components</a>
* <a href="{{ site.github.repository_url }}/blob/master/graph/connected-components/bi-connected-components.cpp">View this file on GitHub</a>
    - Last commit date: 2020-03-25 22:02:49+09:00




## Verified with

* :heavy_check_mark: <a href="../../../verify/test/verify/aoj-3022.test.cpp.html">test/verify/aoj-3022.test.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
/**
 * @brief Bi-Connected-Components(二重頂点連結成分分解)
 */
template< typename T = int >
struct BiConnectedComponents : LowLink< T > {
public:
  using LowLink< T >::LowLink;
  using LowLink< T >::g;
  using LowLink< T >::ord;
  using LowLink< T >::low;

  vector< vector< Edge< T > > > bc;

  void build() override {
    LowLink< T >::build();
    used.assign(g.size(), 0);
    for(int i = 0; i < used.size(); i++) {
      if(!used[i]) dfs(i, -1);
    }
  }

  explicit BiConnectedComponents(const Graph< T > &g) : Graph< T >(g) {}

private:
  vector< int > used;
  vector< Edge< T > > tmp;

  void dfs(int idx, int par) {
    used[idx] = true;
    bool beet = false;
    for(auto &to : g[idx]) {
      if(to == par && !exchange(beet, true)) continue;
      if(!used[to] || ord[to] < ord[idx]) {
        tmp.emplace_back(to);
      }
      if(!used[to]) {
        dfs(to, idx);
        if(low[to] >= ord[idx]) {
          bc.emplace_back();
          for(;;) {
            auto e = tmp.back();
            bc.back().emplace_back(e);
            tmp.pop_back();
            if(e.idx == to.idx) break;
          }
        }
      }
    }
  }
};

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "graph/connected-components/bi-connected-components.cpp"
/**
 * @brief Bi-Connected-Components(二重頂点連結成分分解)
 */
template< typename T = int >
struct BiConnectedComponents : LowLink< T > {
public:
  using LowLink< T >::LowLink;
  using LowLink< T >::g;
  using LowLink< T >::ord;
  using LowLink< T >::low;

  vector< vector< Edge< T > > > bc;

  void build() override {
    LowLink< T >::build();
    used.assign(g.size(), 0);
    for(int i = 0; i < used.size(); i++) {
      if(!used[i]) dfs(i, -1);
    }
  }

  explicit BiConnectedComponents(const Graph< T > &g) : Graph< T >(g) {}

private:
  vector< int > used;
  vector< Edge< T > > tmp;

  void dfs(int idx, int par) {
    used[idx] = true;
    bool beet = false;
    for(auto &to : g[idx]) {
      if(to == par && !exchange(beet, true)) continue;
      if(!used[to] || ord[to] < ord[idx]) {
        tmp.emplace_back(to);
      }
      if(!used[to]) {
        dfs(to, idx);
        if(low[to] >= ord[idx]) {
          bc.emplace_back();
          for(;;) {
            auto e = tmp.back();
            bc.back().emplace_back(e);
            tmp.pop_back();
            if(e.idx == to.idx) break;
          }
        }
      }
    }
  }
};

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

