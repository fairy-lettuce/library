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
<script type="text/javascript" src="../../assets/js/copy-button.js"></script>
<link rel="stylesheet" href="../../assets/css/copy-button.css" />


# :heavy_check_mark: dp/edit-distance.cpp

<a href="../../index.html">Back to top page</a>

* category: <a href="../../index.html#95687afb5d9a2a9fa39038f991640b0c">dp</a>
* <a href="{{ site.github.repository_url }}/blob/master/dp/edit-distance.cpp">View this file on GitHub</a>
    - Last commit date: 2019-12-23 02:27:30+09:00




## Verified with

* :heavy_check_mark: <a href="../../verify/test/verify/aoj-dpl-1-e.test.cpp.html">test/verify/aoj-dpl-1-e.test.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
int edit_distance(const string &S, const string &T) {
  const int N = (int) S.size(), M = (int) T.size();
  vector< vector< int > > dp(N + 1, vector< int >(M + 1, N + M));
  for(int i = 0; i <= N; i++) dp[i][0] = i;
  for(int i = 0; i <= M; i++) dp[0][i] = i;
  for(int i = 1; i <= N; i++) {
    for(int j = 1; j <= M; j++) {
      dp[i][j] = min(dp[i][j], dp[i - 1][j] + 1);
      dp[i][j] = min(dp[i][j], dp[i][j - 1] + 1);
      dp[i][j] = min(dp[i][j], dp[i - 1][j - 1] + (S[i - 1] != T[j - 1]));
    }
  }
  return dp[N][M];
}


```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "dp/edit-distance.cpp"
int edit_distance(const string &S, const string &T) {
  const int N = (int) S.size(), M = (int) T.size();
  vector< vector< int > > dp(N + 1, vector< int >(M + 1, N + M));
  for(int i = 0; i <= N; i++) dp[i][0] = i;
  for(int i = 0; i <= M; i++) dp[0][i] = i;
  for(int i = 1; i <= N; i++) {
    for(int j = 1; j <= M; j++) {
      dp[i][j] = min(dp[i][j], dp[i - 1][j] + 1);
      dp[i][j] = min(dp[i][j], dp[i][j - 1] + 1);
      dp[i][j] = min(dp[i][j], dp[i - 1][j - 1] + (S[i - 1] != T[j - 1]));
    }
  }
  return dp[N][M];
}


```
{% endraw %}

<a href="../../index.html">Back to top page</a>

