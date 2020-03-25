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


# :warning: test/verify/yukicoder-715.cpp

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#5a4423c79a88aeb6104a40a645f9430c">test/verify</a>
* <a href="{{ site.github.repository_url }}/blob/master/test/verify/yukicoder-715.cpp">View this file on GitHub</a>
    - Last commit date: 2020-01-07 02:07:19+09:00




## Code

<a id="unbundled"></a>
{% raw %}
```cpp
#define IGNORE

int main() {
  int n;
  cin >> n;
  vector< int > a(n), x(n), y(n);
  for(int i = 0; i < n; i++) cin >> a[i];
  for(int i = 0; i < n; i++) cin >> x[i];
  for(int i = 0; i < n; i++) cin >> y[i];
  function< int64_t(int, int) > dist = [&](int i, int j) {
    assert(0 <= i && i < j && j <= n);
    int s = abs(a[j - 1] - x[i]);
    int t = abs(y[i]);
    return 1LL * s * s * s + 1LL * t * t * t;
  };
  cout << online_offline_dp(n, dist).back() << endl;
}

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "test/verify/yukicoder-715.cpp"
#define IGNORE

int main() {
  int n;
  cin >> n;
  vector< int > a(n), x(n), y(n);
  for(int i = 0; i < n; i++) cin >> a[i];
  for(int i = 0; i < n; i++) cin >> x[i];
  for(int i = 0; i < n; i++) cin >> y[i];
  function< int64_t(int, int) > dist = [&](int i, int j) {
    assert(0 <= i && i < j && j <= n);
    int s = abs(a[j - 1] - x[i]);
    int t = abs(y[i]);
    return 1LL * s * s * s + 1LL * t * t * t;
  };
  cout << online_offline_dp(n, dist).back() << endl;
}

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

