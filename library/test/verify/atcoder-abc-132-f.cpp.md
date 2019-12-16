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


# :warning: test/verify/atcoder-abc-132-f.cpp

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#5a4423c79a88aeb6104a40a645f9430c">test/verify</a>
* <a href="{{ site.github.repository_url }}/blob/master/test/verify/atcoder-abc-132-f.cpp">View this file on GitHub</a>
    - Last commit date: 2019-11-30 23:36:31 +0900




## Code

<a id="unbundled"></a>
{% raw %}
```cpp
int main() {
  int N, K;
  cin >> N >> K;
  auto range = quotient_range(N);

  vector< modint > dp(range.size());
  dp[0] = 1;
  for(int i = 0; i < K; i++) {
    reverse(begin(dp), end(dp));
    vector< modint > dp2(range.size());
    modint add = 0;
    for(int j = range.size() - 1; j >= 0; j--) {
      add += dp[j];
      dp2[j] = add * (range[j].first.second - range[j].first.first + 1);
    }
    dp.swap(dp2);
  }
  modint ret;
  for(auto &t : dp) ret += t;
  cout << ret << endl;
}


```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "test/verify/atcoder-abc-132-f.cpp"
int main() {
  int N, K;
  cin >> N >> K;
  auto range = quotient_range(N);

  vector< modint > dp(range.size());
  dp[0] = 1;
  for(int i = 0; i < K; i++) {
    reverse(begin(dp), end(dp));
    vector< modint > dp2(range.size());
    modint add = 0;
    for(int j = range.size() - 1; j >= 0; j--) {
      add += dp[j];
      dp2[j] = add * (range[j].first.second - range[j].first.first + 1);
    }
    dp.swap(dp2);
  }
  modint ret;
  for(auto &t : dp) ret += t;
  cout << ret << endl;
}

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

