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


# :warning: test/verify/atcoder-agc-034-c.cpp

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#5a4423c79a88aeb6104a40a645f9430c">test/verify</a>
* <a href="{{ site.github.repository_url }}/blob/master/test/verify/atcoder-agc-034-c.cpp">View this file on GitHub</a>
    - Last commit date: 2019-11-30 22:41:48 +0900




## Code

<a id="unbundled"></a>
{% raw %}
```cpp
int main() {
  int N, X;
  cin >> N >> X;
  int64 loss = 0;
  vector< int64 > A(N), B(N), C(N);
  vector< int > ord;
  for(int i = 0; i < N; i++) {
    cin >> A[i] >> B[i] >> C[i];
    loss += B[i] * A[i];
    ord.emplace_back(i);
  }
  sort(begin(ord), end(ord), [&](int a, int b) {
    return B[a] > B[b];
  });
 
  auto get_cost = [&](int idx, int64 sum) {
    int64 add = 0;
    add += B[idx] * min(sum, A[idx]);
    add += C[idx] * max(0LL, sum - A[idx]);
    return add;
  };
  MaximumSum< int64 > tap(0);
  for(int i = 0; i < N; i++) {
    tap.insert(get_cost(i, X));
  }
  auto check = [&](int64 sum) {
    int64 need = sum / X;
    tap.set_k(need);
    for(int i : ord) {
      tap.erase(get_cost(i, X));
      bool f = tap.query() + get_cost(i, sum % X) >= loss;
      tap.insert(get_cost(i, X));
      if(f) return true;
    }
    return false;
  };
  int64 ok = 1LL * N * X, ng = -1;
  while(ok - ng > 1) {
    auto mid = (ok + ng) / 2;
    if(check(mid)) ok = mid;
    else ng = mid;
  }
  cout << ok << endl;
}

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "test/verify/atcoder-agc-034-c.cpp"
int main() {
  int N, X;
  cin >> N >> X;
  int64 loss = 0;
  vector< int64 > A(N), B(N), C(N);
  vector< int > ord;
  for(int i = 0; i < N; i++) {
    cin >> A[i] >> B[i] >> C[i];
    loss += B[i] * A[i];
    ord.emplace_back(i);
  }
  sort(begin(ord), end(ord), [&](int a, int b) {
    return B[a] > B[b];
  });
 
  auto get_cost = [&](int idx, int64 sum) {
    int64 add = 0;
    add += B[idx] * min(sum, A[idx]);
    add += C[idx] * max(0LL, sum - A[idx]);
    return add;
  };
  MaximumSum< int64 > tap(0);
  for(int i = 0; i < N; i++) {
    tap.insert(get_cost(i, X));
  }
  auto check = [&](int64 sum) {
    int64 need = sum / X;
    tap.set_k(need);
    for(int i : ord) {
      tap.erase(get_cost(i, X));
      bool f = tap.query() + get_cost(i, sum % X) >= loss;
      tap.insert(get_cost(i, X));
      if(f) return true;
    }
    return false;
  };
  int64 ok = 1LL * N * X, ng = -1;
  while(ok - ng > 1) {
    auto mid = (ok + ng) / 2;
    if(check(mid)) ok = mid;
    else ng = mid;
  }
  cout << ok << endl;
}

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

