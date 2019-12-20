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


# :warning: test/verify/spoj-dquery.cpp

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#5a4423c79a88aeb6104a40a645f9430c">test/verify</a>
* <a href="{{ site.github.repository_url }}/blob/master/test/verify/spoj-dquery.cpp">View this file on GitHub</a>
    - Last commit date: 2019-11-30 23:36:31+09:00




## Code

<a id="unbundled"></a>
{% raw %}
```cpp
nt main() {
  int N, Q;
  cin >> N;
  vector< int > A(N);
  for(int i = 0; i < N; i++) {
    cin >> A[i];
  }
  cin >> Q;
  vector< int > f(1000001);
  Mo mo(N, Q);
  for(int i = 0; i < Q; i++) {
    int l, r;
    cin >> l >> r;
    mo.add(--l, r);
  }
  int ret = 0;
  auto add = [&](int idx) { if(f[A[idx]]++ == 0) ret++; };
  auto del = [&](int idx) { if(f[A[idx]]-- == 1) --ret; };
  vector< int > ans(Q);
  auto rem = [&](int idx) { ans[idx] = ret; };
  mo.run(add, del, rem);
  for(int i = 0; i < Q; i++) {
    cout << ans[i] << "\n";
  }
}

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "test/verify/spoj-dquery.cpp"
nt main() {
  int N, Q;
  cin >> N;
  vector< int > A(N);
  for(int i = 0; i < N; i++) {
    cin >> A[i];
  }
  cin >> Q;
  vector< int > f(1000001);
  Mo mo(N, Q);
  for(int i = 0; i < Q; i++) {
    int l, r;
    cin >> l >> r;
    mo.add(--l, r);
  }
  int ret = 0;
  auto add = [&](int idx) { if(f[A[idx]]++ == 0) ret++; };
  auto del = [&](int idx) { if(f[A[idx]]-- == 1) --ret; };
  vector< int > ans(Q);
  auto rem = [&](int idx) { ans[idx] = ret; };
  mo.run(add, del, rem);
  for(int i = 0; i < Q; i++) {
    cout << ans[i] << "\n";
  }
}

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

