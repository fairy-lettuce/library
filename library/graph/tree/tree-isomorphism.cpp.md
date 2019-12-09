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


# :warning: graph/tree/tree-isomorphism.cpp
* category: graph/tree


[Back to top page](../../../index.html)



## Code
{% raw %}
```cpp
template< typename G >
bool tree_isomorphism(const G &a, const G &b) {
  if(a.size() != b.size()) return false;

  const int N = (int) a.size();
  using pvi = pair< vector< int >, vector< int > >;

  auto get_uku = [&](const G &t, int e) {
    stack< pair< int, int > > st;
    st.emplace(e, -1);
    vector< int > dep(N, -1), par(N);
    while(!st.empty()) {
      auto p = st.top();
      if(dep[p.first] == -1) {
        dep[p.first] = p.second == -1 ? 0 : dep[p.second] + 1;
        for(auto &to : t[p.first]) if(to != p.second) st.emplace(to, p.first);
      } else {
        par[p.first] = p.second;
        st.pop();
      }
    }
    return make_pair(dep, par);
  };

  auto solve = [&](const pvi &latte, const pvi &malta) {

    int d = *max_element(begin(latte.first), end(latte.first));
    if(d != *max_element(begin(malta.first), end(malta.first))) return false;

    vector< vector< int > > latte_d(d + 1), malta_d(d + 1), latte_key(N), malta_key(N);

    for(int i = 0; i < N; i++) latte_d[latte.first[i]].emplace_back(i);
    for(int i = 0; i < N; i++) malta_d[malta.first[i]].emplace_back(i);

    for(int i = d; i >= 0; i--) {
      map< vector< int >, int > ord;
      for(auto &idx : latte_d[i]) {
        sort(begin(latte_key[idx]), end(latte_key[idx]));
        ord[latte_key[idx]]++;
      }
      for(auto &idx : malta_d[i]) {
        sort(begin(malta_key[idx]), end(malta_key[idx]));
        if(--ord[malta_key[idx]] < 0) return false;
      }
      if(i == 0) return ord.size() == 1;

      int ptr = 0;
      for(auto &p : ord) {
        if(p.second != 0) return false;
        p.second = ptr++;
      }
      for(auto &idx : latte_d[i]) {
        latte_key[latte.second[idx]].emplace_back(ord[latte_key[idx]]);
      }
      for(auto &idx : malta_d[i]) {
        malta_key[malta.second[idx]].emplace_back(ord[malta_key[idx]]);
      }
    }
    assert(0);
  };
  auto p = centroid(a), q = centroid(b);
  if(p.size() != q.size()) return false;
  auto a1 = get_uku(a, p[0]);
  auto b1 = get_uku(b, q[0]);
  if(solve(a1, b1)) return true;
  if(p.size() == 1) return false;
  auto a2 = get_uku(a, p[1]);
  return solve(a2, b1);
}

```
{% endraw %}

[Back to top page](../../../index.html)

