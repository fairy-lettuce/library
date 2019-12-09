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


# :warning: math/fps/berlekamp-massey.cpp
* category: math/fps


[Back to top page](../../../index.html)



## Code
{% raw %}
```cpp
template< class T >
FormalPowerSeries< T > berlekamp_massey(const FormalPowerSeries< T > &s) {
  const int N = (int) s.size();
  FormalPowerSeries< T > b = {T(-1)}, c = {T(-1)};
  T y = T(1);
  for(int ed = 1; ed <= N; ed++) {
    int l = int(c.size()), m = int(b.size());
    T x = 0;
    for(int i = 0; i < l; i++) x += c[i] * s[ed - l + i];
    b.emplace_back(0);
    m++;
    if(x == T(0)) continue;
    T freq = x / y;
    if(l < m) {
      auto tmp = c;
      c.insert(begin(c), m - l, T(0));
      for(int i = 0; i < m; i++) c[m - 1 - i] -= freq * b[m - 1 - i];
      b = tmp;
      y = x;
    } else {
      for(int i = 0; i < m; i++) c[l - 1 - i] -= freq * b[m - 1 - i];
    }
  }
  return c;
}

```
{% endraw %}

[Back to top page](../../../index.html)

