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


# :heavy_check_mark: test/verify/aoj-grl-2-a-3.test.cpp


[Back to top page](../../../index.html)

* see: [http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=GRL_2_A](http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=GRL_2_A)


## Dependencies
* :heavy_check_mark: [graph/mst/boruvka.cpp](../../../library/graph/mst/boruvka.cpp.html)
* :heavy_check_mark: [graph/template.cpp](../../../library/graph/template.cpp.html)
* :heavy_check_mark: [structure/union-find/union-find.cpp](../../../library/structure/union-find/union-find.cpp.html)
* :heavy_check_mark: [template/template.cpp](../../../library/template/template.cpp.html)


## Code
{% raw %}
```cpp
#define PROBLEM "http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=GRL_2_A"

#include "../../template/template.cpp"
#include "../../graph/template.cpp"

#include "../../structure/union-find/union-find.cpp"

#include "../../graph/mst/boruvka.cpp"

int main() {
  int V, E;
  cin >> V >> E;
  Edges< int > g;
  for(int i = 0; i < E; i++) {
    int x, y, z;
    cin >> x >> y >> z;
    g.emplace_back(x, y, z);
  }
  const int INF = 1 << 30;
  auto f = [&](int sz, vector< int > belong) {
    vector< pair< int, int > > ret(sz, {INF, -1});
    for(auto &e : g) {
      if(belong[e.src] == belong[e.to]) continue;
      ret[belong[e.src]] = min(ret[belong[e.src]], make_pair(e.cost, belong[e.to]));
      ret[belong[e.to]] = min(ret[belong[e.to]], make_pair(e.cost, belong[e.src]));
    }
    return ret;
  };
  cout << boruvka< int, decltype(f) >(V, f) << endl;
}

```
{% endraw %}

[Back to top page](../../../index.html)

