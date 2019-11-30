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


# :warning: math/mod-log.cpp
* category: math


[Back to top page](../../index.html)



## Code
```cpp
int64_t mod_log(int64_t a, int64_t b, int64_t p) {
  int64_t g = 1;

  for(int64_t i = p; i; i /= 2) (g *= a) %= p;
  g = __gcd(g, p);

  int64_t t = 1, c = 0;
  for(; t % g; c++) {
    if(t == b) return c;
    (t *= a) %= p;
  }
  if(b % g) return -1;

  t /= g;
  b /= g;

  int64_t n = p / g, h = 0, gs = 1;

  for(; h * h < n; h++) (gs *= a) %= n;

  unordered_map< int64_t, int64_t > bs;
  for(int64_t s = 0, e = b; s < h; bs[e] = ++s) {
    (e *= a) %= n;
  }

  for(int64_t s = 0, e = t; s < n;) {
    (e *= gs) %= n;
    s += h;
    if(bs.count(e)) return c + s - bs[e];
  }
  return -1;
}

```

[Back to top page](../../index.html)

