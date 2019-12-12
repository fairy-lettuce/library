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


# :heavy_check_mark: test/verify/yosupo-sparse-matrix-det.test.cpp
<a href="../../../index.html">Back to top page</a>

* <a href="{{ site.github.repository_url }}/blob/master/test/verify/yosupo-sparse-matrix-det.test.cpp">View this file on GitHub</a>
    - Last commit date: 2019-12-12 22:16:00 +0900


* see: <a href="https://judge.yosupo.jp/problem/sparse_matrix_det">https://judge.yosupo.jp/problem/sparse_matrix_det</a>


## Depends On
* :heavy_check_mark: <a href="../../../library/math/combinatorics/mod-int.cpp.html">math/combinatorics/mod-int.cpp</a>
* :heavy_check_mark: <a href="../../../library/math/fps/berlekamp-massey.cpp.html">math/fps/berlekamp-massey.cpp</a>
* :heavy_check_mark: <a href="../../../library/math/fps/formal-power-series.cpp.html">math/fps/formal-power-series.cpp</a>
* :heavy_check_mark: <a href="../../../library/math/fps/sparse-matrix.cpp.html">math/fps/sparse-matrix.cpp</a>
* :heavy_check_mark: <a href="../../../library/template/template.cpp.html">template/template.cpp</a>


## Code
{% raw %}
```cpp
#define PROBLEM "https://judge.yosupo.jp/problem/sparse_matrix_det"

#include "../../template/template.cpp"

#include "../../math/combinatorics/mod-int.cpp"

#include "../../math/fps/formal-power-series.cpp"

#include "../../math/fps/berlekamp-massey.cpp"
#include "../../math/fps/sparse-matrix.cpp"

const int MOD = 998244353;
using mint = ModInt< MOD >;

int main() {
  int N, K;
  cin >> N >> K;
  FPSGraph< mint > g(N);
  for(int i = 0; i < K; i++) {
    int a, b, c;
    cin >> a >> b >> c;
    g[a].emplace_back(b, c);
  }
  cout << sparse_determinant(g) << endl;
}

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

