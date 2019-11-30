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


# :warning: other/verify/codeforces-dynamic-connectivity-contest-a.cpp
* category: other/verify


[Back to top page](../../../index.html)



## Code
```cpp
int main() {
  FILE *in, *out;
  in = fopen("connect.in", "r");
  out = fopen("connect.out", "w");

  int N, Q;
  fscanf(in, "%d %d", &N, &Q);
  OfflineDynamicConnectivity odc(N, Q);
  vector< char > T(Q);
  for(int i = 0; i < Q; i++) {
    fscanf(in, " %c", &T[i]);
    if(T[i] == '+' || T[i] == '-') {
      int x, y;
      fscanf(in, "%d %d", &x, &y);
      --x, --y;
      if(T[i] == '+') odc.insert(i, x, y);
      else odc.erase(i, x, y);
    }
  }
  odc.build();
  odc.run([&](int k) {
    if(T[k] == '?') fprintf(out, "%d\n", odc.comp);
  });
}


```

[Back to top page](../../../index.html)

