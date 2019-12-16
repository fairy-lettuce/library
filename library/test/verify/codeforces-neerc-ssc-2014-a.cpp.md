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


# :warning: test/verify/codeforces-neerc-ssc-2014-a.cpp

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#5a4423c79a88aeb6104a40a645f9430c">test/verify</a>
* <a href="{{ site.github.repository_url }}/blob/master/test/verify/codeforces-neerc-ssc-2014-a.cpp">View this file on GitHub</a>
    - Last commit date: 2019-11-30 23:36:31 +0900




## Code

<a id="unbundled"></a>
{% raw %}
```cpp
struct UnionFindUndo {
  vector< int > data;
  stack< pair< int, int > > history;

  UnionFindUndo(int sz) {
    data.assign(sz, -1);
  }

  bool unite(int x, int y) {
    x = find(x), y = find(y);
    history.emplace(x, data[x]);
    history.emplace(y, data[y]);
    if(x == y) return (false);
    if(data[x] > data[y]) swap(x, y);
    data[x] += data[y];
    data[y] = x;
    return (true);
  }

  int find(int k) {
    if(data[k] < 0) return (k);
    return (find(data[k]));
  }

  int size(int k) {
    return (-data[find(k)]);
  }

  void undo() {
    data[history.top().first] = history.top().second;
    history.pop();
    data[history.top().first] = history.top().second;
    history.pop();
  }

  void snapshot() {
    while(history.size()) history.pop();
  }

  void rollback() {
    while(history.size()) undo();
  }
};

int main() {
  int N, M, Q;
  cin >> N >> M >> Q;
  vector< int > X(M), Y(M);
  for(int i = 0; i < M; i++) {
    cin >> X[i] >> Y[i];
    --X[i], --Y[i];
  }
  MoRollBack mo(N, Q);
  for(int i = 0; i < Q; i++) {
    int l, r;
    cin >> l >> r;
    mo.add(--l, r);
  }

  UnionFindUndo uf(N + N);
  vector< int > ans(Q);
  int dame_sum = 0, dame_add = 0;
  vector< int > dame;
  auto add = [&](int idx) {
    uf.unite(X[idx], Y[idx] + N);
    uf.unite(X[idx] + N, Y[idx]);
    dame_add += uf.find(X[idx]) == uf.find(Y[idx]);
  };
  auto rem = [&](int idx) {
    ans[idx] = dame_sum + dame_add > 0;
  };
  auto reset = [&]() {
    uf = UnionFindUndo(N + N);
    dame_add = dame_sum = 0;
  };
  auto snapshot = [&]() {
    uf.snapshot();
    dame_sum += dame_add;
    dame_add = 0;
  };
  auto rollback = [&]() {
    uf.rollback();
    dame_add = 0;
  };
  mo.run(add, rem, reset, snapshot, rollback);
  for(auto &p : ans) {
    if(p) cout << "Impossible\n";
    else cout << "Possible\n";
  }
}

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "test/verify/codeforces-neerc-ssc-2014-a.cpp"
struct UnionFindUndo {
  vector< int > data;
  stack< pair< int, int > > history;

  UnionFindUndo(int sz) {
    data.assign(sz, -1);
  }

  bool unite(int x, int y) {
    x = find(x), y = find(y);
    history.emplace(x, data[x]);
    history.emplace(y, data[y]);
    if(x == y) return (false);
    if(data[x] > data[y]) swap(x, y);
    data[x] += data[y];
    data[y] = x;
    return (true);
  }

  int find(int k) {
    if(data[k] < 0) return (k);
    return (find(data[k]));
  }

  int size(int k) {
    return (-data[find(k)]);
  }

  void undo() {
    data[history.top().first] = history.top().second;
    history.pop();
    data[history.top().first] = history.top().second;
    history.pop();
  }

  void snapshot() {
    while(history.size()) history.pop();
  }

  void rollback() {
    while(history.size()) undo();
  }
};

int main() {
  int N, M, Q;
  cin >> N >> M >> Q;
  vector< int > X(M), Y(M);
  for(int i = 0; i < M; i++) {
    cin >> X[i] >> Y[i];
    --X[i], --Y[i];
  }
  MoRollBack mo(N, Q);
  for(int i = 0; i < Q; i++) {
    int l, r;
    cin >> l >> r;
    mo.add(--l, r);
  }

  UnionFindUndo uf(N + N);
  vector< int > ans(Q);
  int dame_sum = 0, dame_add = 0;
  vector< int > dame;
  auto add = [&](int idx) {
    uf.unite(X[idx], Y[idx] + N);
    uf.unite(X[idx] + N, Y[idx]);
    dame_add += uf.find(X[idx]) == uf.find(Y[idx]);
  };
  auto rem = [&](int idx) {
    ans[idx] = dame_sum + dame_add > 0;
  };
  auto reset = [&]() {
    uf = UnionFindUndo(N + N);
    dame_add = dame_sum = 0;
  };
  auto snapshot = [&]() {
    uf.snapshot();
    dame_sum += dame_add;
    dame_add = 0;
  };
  auto rollback = [&]() {
    uf.rollback();
    dame_add = 0;
  };
  mo.run(add, rem, reset, snapshot, rollback);
  for(auto &p : ans) {
    if(p) cout << "Impossible\n";
    else cout << "Possible\n";
  }
}

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

