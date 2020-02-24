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


# :warning: Euler’s-Phi-Function-Table(オイラーのφ関数テーブル) <small>(math/number-theory/euler-phi-table.cpp)</small>

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#d4a327615e3a055131f0682831111ce2">math/number-theory</a>
* <a href="{{ site.github.repository_url }}/blob/master/math/number-theory/euler-phi-table.cpp">View this file on GitHub</a>
    - Last commit date: 2020-02-24 19:08:02+09:00




## 概要

正の整数 $n$ が与えられたとき, $1$ から $n$ までの自然数のうち $n$ と互いに素なものの個数 $\phi(n)$ を求める.

以下の式で効率的に求めることができる.

$\phi(n)=n\displaystyle\prod_{i=1}^k(1-\dfrac{1}{p_i})$ (ただし $p_i$ は $n$ の素因数)

これは各素因数側から割っていっても同じように計算できるので, $n$ 以下のテーブルを効率的に構築可能である.

* `euler_phi_table(n)`: `n` 以下のオイラーの $\phi$ 関数テーブルを返す.

## 計算量

* $O(N \log \log N)$


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
/**
 * @brief Euler’s-Phi-Function-Table(オイラーのφ関数テーブル)
 * @docs docs/euler-phi-table.md
 */
vector< int > euler_phi_table(int n) {
  vector< int > euler(n + 1);
  for(int i = 0; i <= n; i++) {
    euler[i] = i;
  }
  for(int i = 2; i <= n; i++) {
    if(euler[i] == i) {
      for(int j = i; j <= n; j += i) {
        euler[j] = euler[j] / i * (i - 1);
      }
    }
  }
  return euler;
}

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "math/number-theory/euler-phi-table.cpp"
/**
 * @brief Euler’s-Phi-Function-Table(オイラーのφ関数テーブル)
 * @docs docs/euler-phi-table.md
 */
vector< int > euler_phi_table(int n) {
  vector< int > euler(n + 1);
  for(int i = 0; i <= n; i++) {
    euler[i] = i;
  }
  for(int i = 2; i <= n; i++) {
    if(euler[i] == i) {
      for(int j = i; j <= n; j += i) {
        euler[j] = euler[j] / i * (i - 1);
      }
    }
  }
  return euler;
}

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

