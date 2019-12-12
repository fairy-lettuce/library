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


# :heavy_check_mark: test/verify/aoj-dsl-1-a.test.cpp
<a href="../../../index.html">Back to top page</a>

* <a href="{{ site.github.repository_url }}/blob/master/test/verify/aoj-dsl-1-a.test.cpp">View this file on GitHub</a>
    - Last commit date: 2019-11-30 22:41:48 +0900


* see: <a href="http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=DSL_1_A">http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=DSL_1_A</a>


## Depends On
* :heavy_check_mark: <a href="../../../library/structure/union-find/union-find.cpp.html">structure/union-find/union-find.cpp</a>
* :heavy_check_mark: <a href="../../../library/template/template.cpp.html">template/template.cpp</a>


## Code
{% raw %}
```cpp
#define PROBLEM "http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=DSL_1_A"

#include "../../template/template.cpp"

#include "../../structure/union-find/union-find.cpp"

int main() {
  int N, Q;
  scanf("%d %d", &N, &Q);
  UnionFind uf(N);
  while(Q--) {
    int t, x, y;
    scanf("%d %d %d", &t, &x, &y);
    if(t == 0) uf.unite(x, y);
    else printf("%d\n", uf.find(x) == uf.find(y));
  }
}

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

