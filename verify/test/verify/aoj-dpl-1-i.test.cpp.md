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


# :heavy_check_mark: test/verify/aoj-dpl-1-i.test.cpp
<a href="../../../index.html">Back to top page</a>

* <a href="{{ site.github.repository_url }}/blob/master/test/verify/aoj-dpl-1-i.test.cpp">View this file on GitHub</a>
    - Last commit date: 2019-12-03 22:44:33 +0900


* see: <a href="http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=DPL_1_I">http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=DPL_1_I</a>


## Depends On
* :heavy_check_mark: <a href="../../../library/dp/knapsack-limitations-2.cpp.html">dp/knapsack-limitations-2.cpp</a>
* :warning: <a href="../../../library/dp/knapsack-limitations.cpp.html">dp/knapsack-limitations.cpp</a>
* :warning: <a href="../../../library/template/template.cpp.html">template/template.cpp</a>


## Code
{% raw %}
```cpp
#define PROBLEM "http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=DPL_1_I"

#include "../../template/template.cpp"

#include "../../dp/knapsack-limitations.cpp"

#include "../../dp/knapsack-limitations-2.cpp"

int main() {
  int N;
  int64 W;
  cin >> N >> W;
  vector< int > v(N);
  vector< int64 > w(N), m(N);
  for(int i = 0; i < N; i++) {
    cin >> v[i] >> w[i] >> m[i];
  }
  cout << knapsack_limitations(w, m, v, W) << endl;
}

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

