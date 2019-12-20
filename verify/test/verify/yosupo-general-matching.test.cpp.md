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
    - Last commit date: 2019-12-12 22:16:00+09:00


* see: <a href="https://judge.yosupo.jp/problem/general_matching">https://judge.yosupo.jp/problem/general_matching</a>


## Depends on

* :heavy_check_mark: <a href="../../../library/graph/flow/gabow-edmonds.cpp.html">graph/flow/gabow-edmonds.cpp</a>
* :warning: <a href="../../../library/template/template.cpp.html">template/template.cpp</a>


## Code

<a id="unbundled"></a>
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

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "test/verify/yosupo-general-matching.test.cpp"
#define PROBLEM "https://judge.yosupo.jp/problem/general_matching"

#line 1 "test/verify/../../template/template.cpp"
#include<bits/stdc++.h>

using namespace std;

using int64 = long long;
const int mod = 1e9 + 7;

const int64 infll = (1LL << 62) - 1;
const int inf = (1 << 30) - 1;

struct IoSetup {
  IoSetup() {
    cin.tie(nullptr);
    ios::sync_with_stdio(false);
    cout << fixed << setprecision(10);
    cerr << fixed << setprecision(10);
  }
} iosetup;


template< typename T1, typename T2 >
ostream &operator<<(ostream &os, const pair< T1, T2 >& p) {
  os << p.first << " " << p.second;
  return os;
}

template< typename T1, typename T2 >
istream &operator>>(istream &is, pair< T1, T2 > &p) {
  is >> p.first >> p.second;
  return is;
}

template< typename T >
ostream &operator<<(ostream &os, const vector< T > &v) {
  for(int i = 0; i < (int) v.size(); i++) {
    os << v[i] << (i + 1 != v.size() ? " " : "");
  }
  return os;
}

template< typename T >
istream &operator>>(istream &is, vector< T > &v) {
  for(T &in : v) is >> in;
  return is;
}

template< typename T1, typename T2 >
inline bool chmax(T1 &a, T2 b) { return a < b && (a = b, true); }

template< typename T1, typename T2 >
inline bool chmin(T1 &a, T2 b) { return a > b && (a = b, true); }

template< typename T = int64 >
vector< T > make_v(size_t a) {
  return vector< T >(a);
}

template< typename T, typename... Ts >
auto make_v(size_t a, Ts... ts) {
  return vector< decltype(make_v< T >(ts...)) >(a, make_v< T >(ts...));
}

template< typename T, typename V >
typename enable_if< is_class< T >::value == 0 >::type fill_v(T &t, const V &v) {
  t = v;
}

template< typename T, typename V >
typename enable_if< is_class< T >::value != 0 >::type fill_v(T &t, const V &v) {
  for(auto &e : t) fill_v(e, v);
}

template< typename F >
struct FixPoint : F {
  FixPoint(F &&f) : F(forward< F >(f)) {}
 
  template< typename... Args >
  decltype(auto) operator()(Args &&... args) const {
    return F::operator()(*this, forward< Args >(args)...);
  }
};
 
template< typename F >
inline decltype(auto) MFP(F &&f) {
  return FixPoint< F >{forward< F >(f)};
}
#line 4 "test/verify/yosupo-general-matching.test.cpp"

#line 1 "test/verify/../../graph/flow/gabow-edmonds.cpp"
// https://qiita.com/Kutimoti_T/items/5b579773e0a24d650bdf
struct GabowEdmonds {

  struct edge {
    int to, idx;
  };

  vector< vector< edge > > g;
  vector< pair< int, int > > edges;
  vector< int > mate, label, first;
  queue< int > que;

  GabowEdmonds(int n) : g(n + 1), mate(n + 1), label(n + 1, -1), first(n + 1) {}

  void add_edge(int u, int v) {
    ++u, ++v;
    g[u].push_back((edge) {v, (int) (edges.size() + g.size())});
    g[v].push_back((edge) {u, (int) (edges.size() + g.size())});
    edges.emplace_back(u, v);
  }

  int find(int x) {
    if(label[first[x]] < 0) return first[x];
    first[x] = find(first[x]);
    return first[x];
  }

  void rematch(int v, int w) {
    int t = mate[v];
    mate[v] = w;
    if(mate[t] != v) return;
    if(label[v] < g.size()) {
      mate[t] = label[v];
      rematch(label[v], t);
    } else {
      int x = edges[label[v] - g.size()].first;
      int y = edges[label[v] - g.size()].second;
      rematch(x, y);
      rematch(y, x);
    }
  }

  void assign_label(int x, int y, int num) {
    int r = find(x);
    int s = find(y);
    int join = 0;
    if(r == s) return;
    label[r] = -num;
    label[s] = -num;
    while(true) {
      if(s != 0) swap(r, s);
      r = find(label[mate[r]]);
      if(label[r] == -num) {
        join = r;
        break;
      }
      label[r] = -num;
    }
    int v = first[x];
    while(v != join) {
      que.push(v);
      label[v] = num;
      first[v] = join;
      v = first[label[mate[v]]];
    }
    v = first[y];
    while(v != join) {
      que.push(v);
      label[v] = num;
      first[v] = join;
      v = first[label[mate[v]]];
    }
  }

  bool augment_check(int u) {
    que = queue< int >();
    first[u] = 0;
    label[u] = 0;
    que.push(u);
    while(!que.empty()) {
      int x = que.front();
      que.pop();
      for(auto e : g[x]) {
        int y = e.to;
        if(mate[y] == 0 && y != u) {
          mate[y] = x;
          rematch(x, y);
          return true;
        } else if(label[y] >= 0) {
          assign_label(x, y, e.idx);
        } else if(label[mate[y]] < 0) {
          label[mate[y]] = x;
          first[mate[y]] = y;
          que.push(mate[y]);
        }
      }
    }
    return false;
  }

  vector< pair< int, int > > max_matching() {
    for(int i = 1; i < g.size(); i++) {
      if(mate[i] != 0) continue;
      if(augment_check(i)) label.assign(g.size(), -1);
    }
    vector< pair< int, int > > ret;
    for(int i = 1; i < g.size(); i++) {
      if(i < mate[i]) ret.emplace_back(i - 1, mate[i] - 1);
    }
    return ret;
  }
};
#line 6 "test/verify/yosupo-general-matching.test.cpp"

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

