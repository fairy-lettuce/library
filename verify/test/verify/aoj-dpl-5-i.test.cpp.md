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


# :warning: test/verify/aoj-dpl-5-i.test.cpp


[Back to top page](../../../index.html)

* see: [http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=DPL_5_I](http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=DPL_5_I)


## Dependencies
* :warning: [math/combinatorics/combination.cpp](../../../library/math/combinatorics/combination.cpp.html)
* :warning: [math/combinatorics/mod-int.cpp](../../../library/math/combinatorics/mod-int.cpp.html)
* :warning: [math/combinatorics/stirling-number-second.cpp](../../../library/math/combinatorics/stirling-number-second.cpp.html)
* :warning: [template/template.cpp](../../../library/template/template.cpp.html)


## Code
```cpp
#define PROBLEM "http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=DPL_5_I"

#include "../../template/template.cpp"

#include "../../math/combinatorics/mod-int.cpp"
#include "../../math/combinatorics/combination.cpp"

#include "../../math/combinatorics/stirling-number-second.cpp"

int main() {
  int N, K;
  cin >> N >> K;
  cout << stirling_number_second< modint >(N, K) << endl;
}


```

[Back to top page](../../../index.html)

