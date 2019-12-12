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


# :warning: graph/others/maximum-independent-set.cpp
<a href="../../../index.html">Back to top page</a>

* category: graph/others
* <a href="{{ site.github.repository_url }}/blob/master/graph/others/maximum-independent-set.cpp">View this file on GitHub</a>
    - Last commit date: 2019-11-30 23:02:43 +0900




## Code
{% raw %}
```cpp
template< typename T >
vector< int > maximum_independent_set(const Matrix< T > &g, int trial = 1000000) {

  int N = (int) g.size();
  vector< uint64_t > bit(N);

  assert(N <= 64);
  for(int i = 0; i < N; i++) {
    for(int j = 0; j < N; j++) {
      if(i != j) {
        assert(g[i][j] == g[j][i]);
        if(g[i][j]) bit[i] |= uint64_t(1) << j;
      }
    }
  }

  vector< int > ord(N);
  iota(begin(ord), end(ord), 0);
  mt19937 mt(chrono::steady_clock::now().time_since_epoch().count());
  int ret = 0;
  uint64_t ver;
  for(int i = 0; i < trial; i++) {
    shuffle(begin(ord), end(ord), mt);
    uint64_t used = 0;
    int add = 0;
    for(int j : ord) {
      if(used & bit[j]) continue;
      used |= uint64_t(1) << j;
      ++add;
    }
    if(ret < add) {
      ret = add;
      ver = used;
    }
  }
  vector< int > ans;
  for(int i = 0; i < N; i++) {
    if((ver >> i) & 1) ans.emplace_back(i);
  }
  return ans;
}

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

