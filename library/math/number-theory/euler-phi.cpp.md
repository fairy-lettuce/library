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


# :heavy_check_mark: Euler's-Phi-Function(オイラーのφ関数) <small>(math/number-theory/euler-phi.cpp)</small>

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#d4a327615e3a055131f0682831111ce2">math/number-theory</a>
* <a href="{{ site.github.repository_url }}/blob/master/math/number-theory/euler-phi.cpp">View this file on GitHub</a>
    - Last commit date: 2020-02-24 19:08:02+09:00




## 概要

正の整数 $n$ が与えられたとき, $1$ から $n$ までの自然数のうち $n$ と互いに素なものの個数 $\phi(n)$ を求める.

以下の式で効率的に求めることができる.

$\phi(n)=n\displaystyle\prod_{i=1}^k(1-\dfrac{1}{p_i})$ (ただし $p_i$ は $n$ の素因数)

* `euler_phi(n)`: $\phi(n)$ を返す.

## 計算量

* $O(\sqrt N)$


## Verified with

* :heavy_check_mark: <a href="../../../verify/test/verify/aoj-ntl-1-d.test.cpp.html">test/verify/aoj-ntl-1-d.test.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
/**
 * @brief Euler's-Phi-Function(オイラーのφ関数)
 * @docs docs/euler-phi.md
 */
int64_t euler_phi(int64_t n) {
  int64_t ret = n;
  for(int64_t i = 2; i * i <= n; i++) {
    if(n % i == 0) {
      ret -= ret / i;
      while(n % i == 0) n /= i;
    }
  }
  if(n > 1) ret -= ret / n;
  return ret;
}

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "math/number-theory/euler-phi.cpp"
/**
 * @brief Euler's-Phi-Function(オイラーのφ関数)
 * @docs docs/euler-phi.md
 */
int64_t euler_phi(int64_t n) {
  int64_t ret = n;
  for(int64_t i = 2; i * i <= n; i++) {
    if(n % i == 0) {
      ret -= ret / i;
      while(n % i == 0) n /= i;
    }
  }
  if(n > 1) ret -= ret / n;
  return ret;
}

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

