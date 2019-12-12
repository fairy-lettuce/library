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


# :warning: test/verify/aoj-dsl-1-b.test.cpp
<a href="../../../index.html">Back to top page</a>

* <a href="{{ site.github.repository_url }}/blob/master/test/verify/aoj-dsl-1-b.test.cpp">View this file on GitHub</a>
    - Last commit date: 2019-11-30 22:41:48 +0900


* see: <a href="http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=DSL_1_B">http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=DSL_1_B</a>


## Depends On
* :warning: <a href="../../../library/structure/union-find/weighted-union-find.cpp.html">structure/union-find/weighted-union-find.cpp</a>
* :warning: <a href="../../../library/template/template.cpp.html">template/template.cpp</a>


## Code
{% raw %}
```cpp
#define PROBLEM "http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=DSL_1_B"

#include "../../template/template.cpp"

#include "../../structure/union-find/weighted-union-find.cpp"

int main() {
  int N, M;
  cin >> N >> M;
  WeightedUnionFind< int > tree(N);
  while(M--) {
    int A, B, C, D;
    cin >> A >> B >> C;
    if(A == 0) {
      cin >> D;
      tree.unite(B, C, D);
    } else {
      if(tree.find(B) == tree.find(C)) {
        cout << tree.diff(B, C) << endl;
      } else {
        cout << "?" << endl;
      }
    }
  }
}

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

