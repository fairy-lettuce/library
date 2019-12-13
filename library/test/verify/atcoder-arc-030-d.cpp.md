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


# :warning: test/verify/atcoder-arc-030-d.cpp
<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#5a4423c79a88aeb6104a40a645f9430c">test/verify</a>
* <a href="{{ site.github.repository_url }}/blob/master/test/verify/atcoder-arc-030-d.cpp">View this file on GitHub</a>
    - Last commit date: 2019-11-30 22:41:48 +0900




## Code
{% raw %}
```cpp
using int64 = long long;
 
int64 add(int64 x, int64 y) { return x + y; }
 
int64 mul(int64 x, int y) { return x * y; }
 
int main() {
  int N, Q;
  scanf("%d %d", &N, &Q);
  vector< int64 > x(N);
  for(int i = 0; i < N; i++) {
    scanf("%lld", &x[i]);
  }
  const int LIM = 10000000;
  PersistentRedBlackTree< int64, int64, add, add, add, mul > beet(LIM, 0, 0);
  auto root = beet.build(x);
  int a, b, c, d;
 
  while(Q--) {
    scanf("%d", &a);
    if(a == 1) {
      scanf("%d %d %d", &a, &b, &c);
      beet.set_propagate(root, --a, b, c);
    } else if(a == 2) {
      scanf("%d %d %d %d", &a, &b, &c, &d);
      auto S = beet.split(root, b);
      auto T = beet.split(S.first, --a);
      auto U = beet.split(root, d);
      auto V = beet.split(U.first, --c);
      root = beet.merge(T.first, beet.merge(V.second, S.second));
    } else {
      scanf("%d %d", &a, &b);
      auto S = beet.split(root, b);
      auto T = beet.split(S.first, --a);
      printf("%lld\n", beet.sum(T.second));
    }
    if(beet.pool.ptr < 1000) root = beet.rebuild(root);
  }
}

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

