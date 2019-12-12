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


# :warning: test/verify/spoj-rmqsq.cpp
<a href="../../../index.html">Back to top page</a>

* category: test/verify
* <a href="{{ site.github.repository_url }}/blob/master/test/verify/spoj-rmqsq.cpp">View this file on GitHub</a>
    - Last commit date: 2019-11-30 22:41:48 +0900




## Code
{% raw %}
```cpp
int main() {
  int N, Q;
  scanf("%d", &N);
  vector< int > vs(N);
  for(int i = 0; i < N; i++) scanf("%d", &vs[i]);
  SparseTable< int > table(vs);
  scanf("%d", &Q);
  while(Q--) {
    int x, y;
    scanf("%d %d", &x, &y);
    printf("%d\n", table.rmq(x, y + 1));
  }
}

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

