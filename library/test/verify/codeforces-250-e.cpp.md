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


# :warning: test/verify/codeforces-250-e.cpp
* category: test/verify


[Back to top page](../../../index.html)



## Code
```cpp
int main() {
  int N, M;
  cin >> N >> M;
  PolynominalMod< modint > C(M + 1);
  C[0] = 1;
  for(int i = 0; i < N; i++) {
    int k;
    cin >> k;
    if(k <= M) C[k] = mod - 4;
  }
  C = C.sqrt();
  C[0] += 1;
  C = C.inverse();
  for(int i = 1; i <= M; i++) {
    cout << C[i] * 2 << "\n";
  }
}

```

[Back to top page](../../../index.html)

