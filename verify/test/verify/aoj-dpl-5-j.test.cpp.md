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


# :warning: test/verify/aoj-dpl-5-j.test.cpp


[Back to top page](../../../index.html)

* see: [http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=DPL_5_J](http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=DPL_5_J)


## Dependencies
* :warning: [math/combinatorics/mod-int.cpp](../../../library/math/combinatorics/mod-int.cpp.html)
* :warning: [math/combinatorics/partition-table.cpp](../../../library/math/combinatorics/partition-table.cpp.html)
* :warning: [template/template.cpp](../../../library/template/template.cpp.html)


## Code
```cpp
#define PROBLEM "http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=DPL_5_J"

#include "../../template/template.cpp"

#include "../../math/combinatorics/mod-int.cpp"

#include "../../math/combinatorics/partition-table.cpp"

int main() {
  int N, K;
  cin >> N >> K;
  cout << get_partition< modint >(N, K)[N][K] << endl;
}

```

[Back to top page](../../../index.html)

