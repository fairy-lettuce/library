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


# :warning: test/verify/atcoder-joisc-2015-g.cpp
* category: test/verify


[Back to top page](../../../index.html)



## Code
```cpp
struct UnionFind {
  vector< int > data;
 
  UnionFind(int sz) {
    data.assign(sz, -1);
  }
 
  bool unite(int x, int y) {
    x = find(x), y = find(y);
    if(x == y) return (false);
    if(data[x] > data[y]) swap(x, y);
    data[x] += data[y];
    data[y] = x;
    return (true);
  }
 
  int find(int k) {
    if(data[k] < 0) return (k);
    return (data[k] = find(data[k]));
  }
 
  int size(int k) {
    return (-data[find(k)]);
  }
};
 
int main() {
  int N, Q;
  cin >> N >> Q;
  auto f = [](int a, int b) { return a + b; };
  auto g = [](int a, int b, int l) { return 0; };
  auto h = [](int a, int b) { return (a | b); };
  auto s = [](int a) { return a; };
  using LCT=LinkCutTree< int >;
  LCT lct(f, g, h, s, 0, 0);
  vector< LCT::Node * > nodev, nodee;
  for(int i = 0; i < N; i++) {
    nodev.emplace_back(lct.make_node(i, 0));
    nodee.emplace_back(lct.make_node(i, 1));
  }
  UnionFind uf(N);
  int cnt = 0;
  for(int i = 0; i < Q; i++) {
    int T, A, B;
    cin >> T >> A >> B;
    --A, --B;
    if(T == 1) {
      if(uf.find(A) != uf.find(B)) {
        lct.evert(nodev[B]);
        lct.link(nodee[cnt], nodev[A]);
        lct.link(nodev[B], nodee[cnt]);
        uf.unite(A, B);
        ++cnt;
      } else {
        lct.evert(nodev[A]);
        lct.expose(nodev[B]);
        lct.set_propagate(nodev[B], 1);
      }
    } else {
      if(uf.find(A) != uf.find(B)) {
        cout << -1 << "\n";
      } else {
        lct.evert(nodev[A]);
        lct.expose(nodev[B]);
        cout << nodev[B]->sum << "\n";
      }
    }
  }
}

```

[Back to top page](../../../index.html)

