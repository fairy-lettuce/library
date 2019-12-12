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


# :warning: test/verify/aoj-dpl-5-i.test.cpp
<a href="../../../index.html">Back to top page</a>

* <a href="{{ site.github.repository_url }}/blob/master/test/verify/aoj-dpl-5-i.test.cpp">View this file on GitHub</a>
    - Last commit date: 2019-11-30 23:36:31 +0900


* see: <a href="http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=DPL_5_I">http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=DPL_5_I</a>


## Depends On
* :warning: <a href="../../../library/math/combinatorics/combination.cpp.html">math/combinatorics/combination.cpp</a>
* :warning: <a href="../../../library/math/combinatorics/mod-int.cpp.html">math/combinatorics/mod-int.cpp</a>
* :warning: <a href="../../../library/math/combinatorics/stirling-number-second.cpp.html">math/combinatorics/stirling-number-second.cpp</a>
* :warning: <a href="../../../library/template/template.cpp.html">template/template.cpp</a>


## Code
{% raw %}
```cpp
#define PROBLEM "http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=DPL_5_I"

#include "../../template/template.cpp"

#include "../../math/combinatorics/mod-int.cpp"
#include "../../math/combinatorics/combination.cpp"

#include "../../math/combinatorics/stirling-number-second.cpp"

int main() {
  int N, K;
  cin >> N >> K;
  cout << stirling_number_second< modint >(N, K) << endl;
}


```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

