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


# :warning: test/verify/codeforces-438-f.cpp
* category: test/verify


[Back to top page](../../../index.html)



## Code
```cpp
int main() {
  int N, K;
  cin >> N >> K;
  vector< int > A(N);
  for(int i = 0; i < N; i++) {
    cin >> A[i];
    --A[i];
  }
  constexpr int64_t INF = 1LL << 58;

  int64 L = 0, R = 0, sum = 0;
  vector< int > appear(100000);
  auto add = [&](int idx) { sum += appear[A[idx]]++; };
  auto del = [&](int idx) { sum -= --appear[A[idx]]; };
  function< int64_t(int l, int r) > f = [&](int l, int r) {
    while(L > l) add(--L);
    while(R < r) add(R++);
    while(L < l) del(L++);
    while(R > r) del(--R);
    return sum;
  };
  cout << divide_and_conquer_optimization(K, N, INF, f).back().back() << endl;
}


```

[Back to top page](../../../index.html)

