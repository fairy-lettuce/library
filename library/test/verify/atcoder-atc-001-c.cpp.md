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


# :warning: test/verify/atcoder-atc-001-c.cpp
* category: test/verify


[Back to top page](../../../index.html)



## Code
```cpp
int main() {
  int N;
  scanf("%d", &N);
  vector< int > A(N + 1), B(N + 1);
  for(int i = 0; i < N; i++) scanf("%d %d", &A[i + 1], &B[i + 1]);
  NumberTheoreticTransform< 1012924417 > ntt;
  auto C = ntt.multiply(A, B);
  for(int i = 1; i <= 2 * N; i++) printf("%d\n", C[i]);
}

```

[Back to top page](../../../index.html)

