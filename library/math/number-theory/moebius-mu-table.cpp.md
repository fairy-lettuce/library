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


# :warning: math/number-theory/moebius-mu-table.cpp

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#d4a327615e3a055131f0682831111ce2">math/number-theory</a>
* <a href="{{ site.github.repository_url }}/blob/master/math/number-theory/moebius-mu-table.cpp">View this file on GitHub</a>
    - Last commit date: 2020-01-16 16:18:06+09:00




## Code

<a id="unbundled"></a>
{% raw %}
```cpp
vector< int > moebius_mu_table(int n) {
  vector< int > mu(n + 1, 1), p(n + 1, 1);
  for(int i = 2; i <= n; i++) {
    if(p[i] == 1) {
      for(int j = i; j <= n; j += i) p[j] = i;
    }
    if((i / p[i]) % p[i] == 0) mu[i] = 0;
    else mu[i] = -mu[i / p[i]];
  }
  return mu;
}

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "math/number-theory/moebius-mu-table.cpp"
vector< int > moebius_mu_table(int n) {
  vector< int > mu(n + 1, 1), p(n + 1, 1);
  for(int i = 2; i <= n; i++) {
    if(p[i] == 1) {
      for(int j = i; j <= n; j += i) p[j] = i;
    }
    if((i / p[i]) % p[i] == 0) mu[i] = 0;
    else mu[i] = -mu[i / p[i]];
  }
  return mu;
}

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

