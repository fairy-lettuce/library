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


# :warning: test/verify/atcoder-agc-018-d.cpp
<a href="../../../index.html">Back to top page</a>

* category: test/verify
* <a href="{{ site.github.repository_url }}/blob/master/test/verify/atcoder-agc-018-d.cpp">View this file on GitHub</a>
    - Last commit date: 2019-11-30 23:02:43 +0900




## Code
{% raw %}
```cpp
template< typename G >
vector< int > centroid(const G &g) {
  const int N = (int) g.size();

  stack< pair< int, int > > st;
  st.emplace(0, -1);
  vector< int > sz(N), par(N);
  while(!st.empty()) {
    auto p = st.top();
    if(sz[p.first] == 0) {
      sz[p.first] = 1;
      for(auto &to : g[p.first]) if(to != p.second) st.emplace(to, p.first);
    } else {
      for(auto &to : g[p.first]) if(to != p.second) sz[p.first] += sz[to];
      par[p.first] = p.second;
      st.pop();
    }
  }

  vector< int > ret;
  int size = N;
  for(int i = 0; i < N; i++) {
    int val = N - sz[i];
    for(auto &to : g[i]) if(to != par[i]) val = max(val, sz[to]);
    if(val < size) size = val, ret.clear();
    if(val == size) ret.emplace_back(i);
  }

  return ret;
}

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

