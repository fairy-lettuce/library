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


# :warning: test/verify/atcoder-wupc-2019-d.cpp
* category: test/verify


[Back to top page](../../../index.html)



## Code
```cpp
int main() {
  int N, M;
  vector< int > g[100000];
  cin >> N >> M;
  for(int i = 0; i < M; i++) {
    int a, b;
    cin >> a >> b;
    --a, --b;
    g[b].emplace_back(a);
  }
  for(int i = 0; i < N; i++) {
    g[i].emplace_back(i);
  }
  int in[100000] = {};
  int ok = 0;
  SqrtDecomposition< int > tap(N, 1);
  for(int i = 0; i < N; i++) tap.set(i, 1);
  int ptr = 0, ret = inf, l;
  for(int i = 0; i < N; i++) {
    while(ptr < N && tap.query_low(0, N) < N) {
      tap.add(0, N);
      for(auto &to : g[ptr]) tap.sub(to, to + 1);
      ++ptr;
    }
    if(tap.query_low(0, N) == N) {
      if(ptr - i < ret) {
        ret = ptr - i;
        l = i;
      }
    }
    tap.sub(0, N);
    for(auto &to : g[i]) tap.add(to, to + 1);
  }
  if(ret == inf) cout << -1 << endl;
  else cout << l + 1 << " " << l + 1 + ret - 1 << endl;
}

```

[Back to top page](../../../index.html)

