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
<script type="text/javascript" src="../../assets/js/copy-button.js"></script>
<link rel="stylesheet" href="../../assets/css/copy-button.css" />


# :warning: math/mod-sqrt.cpp
* category: math


[Back to top page](../../index.html)



## Code
```cpp
template< typename T >
T mod_sqrt(const T &a, const T &p) {
  if(a == 0) return 0;
  if(p == 2) return a;
  if(mod_pow(a, (p - 1) >> 1, p) != 1) return -1;
  T b = 1;
  while(mod_pow(b, (p - 1) >> 1, p) == 1) ++b;
  T e = 0, m = p - 1;
  while(m % 2 == 0) m >>= 1, ++e;
  T x = mod_pow(a, (m - 1) >> 1, p);
  T y = a * (x * x % p) % p;
  (x *= a) %= p;
  T z = mod_pow(b, m, p);
  while(y != 1) {
    T j = 0, t = y;
    while(t != 1) {
      j += 1;
      (t *= t) %= p;
    }
    z = mod_pow(z, T(1) << (e - j - 1), p);
    (x *= z) %= p;
    (z *= z) %= p;
    (y *= z) %= p;
    e = j;
  }
  return x;
}

```

[Back to top page](../../index.html)

