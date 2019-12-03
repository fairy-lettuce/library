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


# :warning: test/verify/codeforces-564-e.cpp
* category: test/verify


[Back to top page](../../../index.html)



## Code
```cpp
int main() {
  struct tap {
    int64 sz, szsum, cashsz, cashszsum;
 
    tap() : sz(0), szsum(0), cashsz(0), cashszsum(0) {}
 
 
    void merge(int64 key, const tap &parent, const tap &child) {
      szsum = cashszsum;
      szsum += parent.sz * parent.sz;
      szsum += child.sz * child.sz;
 
      sz = key;
      sz += parent.sz;
      sz += child.sz;
      sz += cashsz;
    }
 
    void toggle() {
    }
 
    void add(const tap &child) {
      cashszsum += child.sz * child.sz;
      cashsz += child.sz;
    }
 
    void erase(const tap &child) {
      cashszsum -= child.sz * child.sz;
      cashsz -= child.sz;
    }
  } e;
 
  int N, M;
  cin >> N >> M;
  vector< int > C(N);
  cin >> C;
 
  using pi = pair< int64, int >;
 
  using LCT = LinkCutTreeSubtree< tap, int64 >;
  LCT lct(e);
  vector< LCT::Node * > sub(N);
  vector< map< int, vector< pair< int, int > > > > belong(N + 1);
  for(int i = 0; i < N; i++) {
    --C[i];
    sub[i] = lct.make_node(1);
    belong[C[i]][-1].emplace_back(i, 0);
  }
 
  vector< int > parent(N + 1, -1);
  vector< int > g[400001];
 
  g[N].emplace_back(0);
  sub.emplace_back(lct.make_node(1));
 
  function< void(int, int) > dfs = [&](int idx, int par) {
    parent[idx] = par;
    for(auto &to : g[idx]) {
      if(to == par) continue;
      dfs(to, idx);
    }
  };
  for(int i = 1; i < N; i++) {
    int x, y;
    cin >> x >> y;
    --x, --y;
    g[x].emplace_back(y);
    g[y].emplace_back(x);
    lct.evert(sub[y]);
    lct.link(sub[y], sub[x]);
  }
  lct.evert(sub[0]);
  lct.link(sub[0], sub[N]);
  dfs(N, -1);
 
  for(int i = 0; i < M; i++) {
    int u, x;
    cin >> u >> x;
    --u, --x;
    if(C[u] != x) {
      belong[C[u]][i].emplace_back(u, 1); // set black
      C[u] = x;
      belong[x][i].emplace_back(u, 0); // set white
    }
  }
 
 
  vector< int64 > ans(M + 1);
 
 
  for(int i = 0; i < N; i++) {
 
    int last = -1;
    int64 path = 1LL * N * N;
 
    set< int > st;
 
    for(auto &vs : belong[i]) {
      ans[last + 1] += path;
      ans[vs.first + 1] -= path;
 
      for(auto &p : vs.second) {
        if(!p.second) {
          st.emplace(p.first);
          path -= lct.query(lct.get_root(sub[p.first])).szsum;
          lct.cut(sub[p.first]);
          path += lct.query(lct.get_root(sub[parent[p.first]])).szsum;
          path += lct.query(lct.get_root(sub[p.first])).szsum;
        } else {
          st.erase(p.first);
          path -= lct.query(lct.get_root(sub[p.first])).szsum;
          path -= lct.query(lct.get_root(sub[parent[p.first]])).szsum;
          lct.link(sub[p.first], sub[parent[p.first]]);
          path += lct.query(lct.get_root(sub[p.first])).szsum;
        }
      }
      last = vs.first;
    }
    ans[last + 1] += path;
    for(auto &p : st) lct.link(sub[p], sub[parent[p]]);
  }
 
  int64 ret = 0;
  for(int j = 0; j <= M; j++) {
    ret += ans[j];
    cout << 1LL * N * N * N - ret << "\n";
  }
}

```

[Back to top page](../../../index.html)

