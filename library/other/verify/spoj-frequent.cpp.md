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


# :warning: other/verify/spoj-frequent.cpp
* category: other/verify


[Back to top page](../../../index.html)



## Code
```cpp
int main() {
  int N, Q;
  while(cin >> N, N) {
    cin >> Q;
    vector< int > A(N);
    for(int i = 0; i < N; i++) {
      cin >> A[i];
      A[i] += 100000;
    }
    vector< int > f(200001), g(200001);
    Mo mo(N, Q);
    for(int i = 0; i < Q; i++) {
      int l, r;
      cin >> l >> r;
      mo.add(--l, r);
    }
    int ret = 0;
    auto add = [&](int idx) {
      g[f[A[idx]]]--;
      f[A[idx]]++;
      g[f[A[idx]]]++;
      if(f[A[idx]] > ret) ++ret;
    };
    auto del = [&](int idx) {
      g[f[A[idx]]]--;
      f[A[idx]]--;
      g[f[A[idx]]]++;
      if(ret - 1 == f[A[idx]] && g[ret] == 0) --ret;
    };
    vector< int > ans(Q);
    auto rem = [&](int idx) { ans[idx] = ret; };
    mo.run(add, del, rem);
    for(int i = 0; i < Q; i++) {
      cout << ans[i] << "\n";
    }
  }
}

```

[Back to top page](../../../index.html)

