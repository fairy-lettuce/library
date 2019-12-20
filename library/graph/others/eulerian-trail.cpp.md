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


# :warning: graph/others/eulerian-trail.cpp

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#e557c7f962c39680942b9dada22cabec">graph/others</a>
* <a href="{{ site.github.repository_url }}/blob/master/graph/others/eulerian-trail.cpp">View this file on GitHub</a>
    - Last commit date: 2019-11-30 23:02:43+09:00




## Code

<a id="unbundled"></a>
{% raw %}
```cpp
template< typename T >
vector< edge< T > > eulerian_path(Edges< T > es, int s, bool directed) {
  int V = 0;
  for(auto &e : es) V = max(V, max(e.to, e.src) + 1);
  vector< vector< pair< edge< T >, int > > > g(V);
  for(auto &e : es) {
    int sz_to = (int) g[e.to].size();
    g[e.src].emplace_back(e, sz_to);
    if(!directed) {
      int sz_src = (int) g[e.src].size() - 1;
      swap(e.src, e.to);
      g[e.src].emplace_back(e, sz_src);
    }
  }
  vector< edge< T > > ord;
  stack< pair< int, edge< T > > > st;
  st.emplace(s, edge< T >(-1, -1));
  while(st.size()) {
    int idx = st.top().first;
    if(g[idx].empty()) {
      ord.emplace_back(st.top().second);
      st.pop();
    } else {
      auto e = g[idx].back();
      g[idx].pop_back();
      if(e.second == -1) continue;
      if(!directed) g[e.first.to][e.second].second = -1;
      st.emplace(e.first.to, e.first);
    }
  }
  ord.pop_back();
  reverse(begin(ord), end(ord));
  if(ord.size() != es.size()) return {};
  return ord;
}

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "graph/others/eulerian-trail.cpp"
template< typename T >
vector< edge< T > > eulerian_path(Edges< T > es, int s, bool directed) {
  int V = 0;
  for(auto &e : es) V = max(V, max(e.to, e.src) + 1);
  vector< vector< pair< edge< T >, int > > > g(V);
  for(auto &e : es) {
    int sz_to = (int) g[e.to].size();
    g[e.src].emplace_back(e, sz_to);
    if(!directed) {
      int sz_src = (int) g[e.src].size() - 1;
      swap(e.src, e.to);
      g[e.src].emplace_back(e, sz_src);
    }
  }
  vector< edge< T > > ord;
  stack< pair< int, edge< T > > > st;
  st.emplace(s, edge< T >(-1, -1));
  while(st.size()) {
    int idx = st.top().first;
    if(g[idx].empty()) {
      ord.emplace_back(st.top().second);
      st.pop();
    } else {
      auto e = g[idx].back();
      g[idx].pop_back();
      if(e.second == -1) continue;
      if(!directed) g[e.first.to][e.second].second = -1;
      st.emplace(e.first.to, e.first);
    }
  }
  ord.pop_back();
  reverse(begin(ord), end(ord));
  if(ord.size() != es.size()) return {};
  return ord;
}

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

