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


# :heavy_check_mark: Convert-Base(進数変換) <small>(math/number-theory/convert-base.cpp)</small>

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#d4a327615e3a055131f0682831111ce2">math/number-theory</a>
* <a href="{{ site.github.repository_url }}/blob/master/math/number-theory/convert-base.cpp">View this file on GitHub</a>
    - Last commit date: 2020-02-24 19:08:02+09:00




## 概要

10進数 $x$ を $b$ 進数に変換する.

* `convert_base(x, b)`: 10 進数 `x` を `b` 進数に変換した結果を返す.

## 計算量

* $O(\log x)$


## Verified with

* :heavy_check_mark: <a href="../../../verify/test/verify/aoj-0233.test.cpp.html">test/verify/aoj-0233.test.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
/**
 * @brief Convert-Base(進数変換)
 * @docs docs/convert-base.md
 */
template< typename T >
vector< T > convert_base(T x, T b) {
  vector< T > ret;
  T t = 1, k = abs(b);
  while(x) {
    ret.emplace_back((x * t) % k);
    if(ret.back() < 0) ret.back() += k;
    x -= ret.back() * t;
    x /= k;
    t *= b / k;
  }
  if(ret.empty()) ret.emplace_back(0);
  reverse(begin(ret), end(ret));
  return ret;
}

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "math/number-theory/convert-base.cpp"
/**
 * @brief Convert-Base(進数変換)
 * @docs docs/convert-base.md
 */
template< typename T >
vector< T > convert_base(T x, T b) {
  vector< T > ret;
  T t = 1, k = abs(b);
  while(x) {
    ret.emplace_back((x * t) % k);
    if(ret.back() < 0) ret.back() += k;
    x -= ret.back() * t;
    x /= k;
    t *= b / k;
  }
  if(ret.empty()) ret.emplace_back(0);
  reverse(begin(ret), end(ret));
  return ret;
}

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

