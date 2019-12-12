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


# :heavy_check_mark: test/verify/yosupo-general-matching.test.cpp
<a href="../../../index.html">Back to top page</a>

* <a href="{{ site.github.repository_url }}/blob/master/test/verify/yosupo-general-matching.test.cpp">View this file on GitHub</a>
    - Last commit date: 2019-12-12 22:16:00 +0900


* see: <a href="https://judge.yosupo.jp/problem/general_matching">https://judge.yosupo.jp/problem/general_matching</a>


## Depends On
* :heavy_check_mark: <a href="../../../library/graph/flow/gabow-edmonds.cpp.html">graph/flow/gabow-edmonds.cpp</a>
* :heavy_check_mark: <a href="../../../library/template/template.cpp.html">template/template.cpp</a>


## Code
{% raw %}
```cpp
#define PROBLEM "https://judge.yosupo.jp/problem/general_matching"

#include "../../template/template.cpp"

#include "../../graph/flow/gabow-edmonds.cpp"

int main() {
  int N, M;
  cin >> N >> M;
  GabowEdmonds flow(N);
  for(int i = 0; i < M; i++) {
    int a, b;
    cin >> a >> b;
    flow.add_edge(a, b);
  }
  auto ret = flow.max_matching();
  cout << ret.size() << endl;
  for(auto &p : ret) cout << p << endl;
}

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

