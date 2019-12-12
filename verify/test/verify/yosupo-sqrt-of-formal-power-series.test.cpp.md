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


# :heavy_check_mark: test/verify/yosupo-sqrt-of-formal-power-series.test.cpp
<a href="../../../index.html">Back to top page</a>

* <a href="{{ site.github.repository_url }}/blob/master/test/verify/yosupo-sqrt-of-formal-power-series.test.cpp">View this file on GitHub</a>
    - Last commit date: 2019-12-11 22:31:39 +0900


* see: <a href="https://judge.yosupo.jp/problem/sqrt_of_formal_power_series">https://judge.yosupo.jp/problem/sqrt_of_formal_power_series</a>


## Depends On
* :warning: <a href="../../../library/math/combinatorics/mod-int.cpp.html">math/combinatorics/mod-int.cpp</a>
* :heavy_check_mark: <a href="../../../library/math/combinatorics/mod-pow.cpp.html">math/combinatorics/mod-pow.cpp</a>
* :heavy_check_mark: <a href="../../../library/math/combinatorics/mod-sqrt.cpp.html">math/combinatorics/mod-sqrt.cpp</a>
* :heavy_check_mark: <a href="../../../library/math/fft/number-theoretic-transform-friendly-mod-int.cpp.html">math/fft/number-theoretic-transform-friendly-mod-int.cpp</a>
* :heavy_check_mark: <a href="../../../library/math/fps/formal-power-series.cpp.html">math/fps/formal-power-series.cpp</a>
* :warning: <a href="../../../library/template/template.cpp.html">template/template.cpp</a>


## Code
{% raw %}
```cpp
#define PROBLEM "https://judge.yosupo.jp/problem/sqrt_of_formal_power_series"

#include "../../template/template.cpp"

#include "../../math/combinatorics/mod-int.cpp"
#include "../../math/fft/number-theoretic-transform-friendly-mod-int.cpp"

#include "../../math/combinatorics/mod-pow.cpp"
#include "../../math/combinatorics/mod-sqrt.cpp"

#include "../../math/fps/formal-power-series.cpp"

const int MOD = 998244353;
using mint = ModInt< MOD >;

int main() {
  NumberTheoreticTransformFriendlyModInt< mint > ntt;
  using FPS = FormalPowerSeries< mint >;
  auto mult = [&](const FPS::P &a, const FPS::P &b) {
    auto ret = ntt.multiply(a, b);
    return FPS::P(ret.begin(), ret.end());
  };
  FPS::set_mult(mult);
  FPS::set_fft([&](FPS::P &a) { ntt.ntt(a); }, [&](FPS::P &a) { ntt.intt(a); });
  FPS::set_sqrt([](mint a) { return mod_sqrt< int64_t >(a.x, MOD); });
  int N;
  cin >> N;
  FPS F(N);
  cin >> F;
  auto ret = F.sqrt();
  if(ret.empty()) cout << -1 << endl;
  else cout << ret << endl;
}

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

