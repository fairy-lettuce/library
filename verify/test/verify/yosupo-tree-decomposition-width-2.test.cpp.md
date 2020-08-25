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


# :heavy_check_mark: test/verify/yosupo-tree-decomposition-width-2.test.cpp

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#5a4423c79a88aeb6104a40a645f9430c">test/verify</a>
* <a href="{{ site.github.repository_url }}/blob/master/test/verify/yosupo-tree-decomposition-width-2.test.cpp">View this file on GitHub</a>
    - Last commit date: 2020-05-27 13:26:09+09:00


* see: <a href="https://judge.yosupo.jp/problem/tree_decomposition_width_2">https://judge.yosupo.jp/problem/tree_decomposition_width_2</a>


## Depends on

* :heavy_check_mark: <a href="../../../library/graph/others/tree-decomposition.cpp.html">Tree-Decomposition(木分解) <small>(graph/others/tree-decomposition.cpp)</small></a>
* :heavy_check_mark: <a href="../../../library/other/printer.cpp.html">Printer(高速出力) <small>(other/printer.cpp)</small></a>
* :heavy_check_mark: <a href="../../../library/other/scanner.cpp.html">Scanner(高速入力) <small>(other/scanner.cpp)</small></a>
* :question: <a href="../../../library/structure/union-find/union-find.cpp.html">Union-Find <small>(structure/union-find/union-find.cpp)</small></a>
* :question: <a href="../../../library/template/template.cpp.html">template/template.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
#define PROBLEM "https://judge.yosupo.jp/problem/tree_decomposition_width_2"

#include "../../template/template.cpp"

#include "../../other/scanner.cpp"
#include "../../other/printer.cpp"

#include "../../structure/union-find/union-find.cpp"

#include "../../graph/others/tree-decomposition.cpp"

int main() {
  string x;
  int N, M;
  Scanner pin(stdin);
  Printer pout(stdout);
  pin.read(x, x, N, M);
  vector< int > A(M), B(M);
  UnionFind uf(N);
  for(int i = 0; i < M; i++) {
    pin.read(A[i], B[i]);
    --A[i], --B[i];
    uf.unite(A[i], B[i]);
  }
  int root = -1;
  for(int i = 0; i < N; i++) {
    if(uf.find(i) == i) {
      if(root == -1) {
        root = i;
      } else {
        A.emplace_back(root);
        B.emplace_back(i);
      }
    }
  }
  TreeDecomposition td(N);
  for(int i = 0; i < A.size(); i++) {
    td.add_edge(A[i], B[i]);
  }
  auto tap = td.build();
  if(tap.empty()) {
    pout.writeln("-1");
    return 0;
  }
  pout.writeln("s", "td", tap.size(), 2, N);
  for(int i = 0; i < tap.size(); i++) {
    for(auto &t : tap[i].bag) ++t;
    pout.writeln("b", i + 1, tap[i].bag);
  }
  for(int i = 0; i < tap.size(); i++) {
    for(auto &t : tap[i].child) pout.writeln(i + 1, t + 1);
  }
}

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "test/verify/yosupo-tree-decomposition-width-2.test.cpp"
#define PROBLEM "https://judge.yosupo.jp/problem/tree_decomposition_width_2"

#line 1 "template/template.cpp"
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
#line 4 "test/verify/yosupo-tree-decomposition-width-2.test.cpp"

#line 1 "other/scanner.cpp"
/**
 * @brief Scanner(高速入力)
 */
struct Scanner {
public:

  explicit Scanner(FILE *fp) : fp(fp) {}

  template< typename T, typename... E >
  void read(T &t, E &... e) {
    read_single(t);
    read(e...);
  }

private:
  static constexpr size_t line_size = 1 << 16;
  static constexpr size_t int_digits = 20;
  char line[line_size + 1] = {};
  FILE *fp = nullptr;
  char *st = line;
  char *ed = line;

  void read() {}

  static inline bool is_space(char c) {
    return c <= ' ';
  }

  void reread() {
    ptrdiff_t len = ed - st;
    memmove(line, st, len);
    char *tmp = line + len;
    ed = tmp + fread(tmp, 1, line_size - len, fp);
    *ed = 0;
    st = line;
  }

  void skip_space() {
    while(true) {
      if(st == ed) reread();
      while(*st && is_space(*st)) ++st;
      if(st != ed) return;
    }
  }

  template< typename T, enable_if_t< is_integral< T >::value, int > = 0 >
  void read_single(T &s) {
    skip_space();
    if(st + int_digits >= ed) reread();
    bool neg = false;
    if(is_signed< T >::value && *st == '-') {
      neg = true;
      ++st;
    }
    typename make_unsigned< T >::type y = *st++ - '0';
    while(*st >= '0') {
      y = 10 * y + *st++ - '0';
    }
    s = (neg ? -y : y);
  }

  template< typename T, enable_if_t< is_same< T, string >::value, int > = 0 >
  void read_single(T &s) {
    s = "";
    skip_space();
    while(true) {
      char *base = st;
      while(*st && !is_space(*st)) ++st;
      s += string(base, st);
      if(st != ed) return;
      reread();
    }
  }

  template< typename T >
  void read_single(vector< T > &s) {
    for(auto &d : s) read(d);
  }
};
#line 1 "other/printer.cpp"
/**
 * @brief Printer(高速出力)
 */
struct Printer {
public:
  explicit Printer(FILE *fp) : fp(fp) {}

  ~Printer() { flush(); }

  template< bool f = false, typename T, typename... E >
  void write(const T &t, const E &... e) {
    if(f) write_single(' ');
    write_single(t);
    write< true >(e...);
  }

  template< typename... T >
  void writeln(const T &...t) {
    write(t...);
    write_single('\n');
  }

  void flush() {
    fwrite(line, 1, st - line, fp);
    st = line;
  }

private:
  FILE *fp = nullptr;
  static constexpr size_t line_size = 1 << 16;
  static constexpr size_t int_digits = 20;
  char line[line_size + 1] = {};
  char small[32] = {};
  char *st = line;

  template< bool f = false >
  void write() {}

  void write_single(const char &t) {
    if(st + 1 >= line + line_size) flush();
    *st++ = t;
  }

  template< typename T, enable_if_t< is_integral< T >::value, int > = 0 >
  void write_single(T s) {
    if(st + int_digits >= line + line_size) flush();
    if(s == 0) {
      write_single('0');
      return;
    }
    if(s < 0) {
      write_single('-');
      s = -s;
    }
    char *mp = small + sizeof(small);
    typename make_unsigned< T >::type y = s;
    size_t len = 0;
    while(y > 0) {
      *--mp = y % 10 + '0';
      y /= 10;
      ++len;
    }
    memmove(st, mp, len);
    st += len;
  }

  void write_single(const string &s) {
    for(auto &c : s) write_single(c);
  }

  void write_single(const char *s) {
    while(*s != 0) write_single(*s++);
  }

  template< typename T >
  void write_single(const vector< T > &s) {
    for(size_t i = 0; i < s.size(); i++) {
      if(i) write_single(' ');
      write_single(s[i]);
    }
  }
};
#line 7 "test/verify/yosupo-tree-decomposition-width-2.test.cpp"

#line 1 "structure/union-find/union-find.cpp"
/**
 * @brief Union-Find
 * @docs docs/union-find.md
 */
struct UnionFind {
  vector< int > data;

  UnionFind() = default;

  explicit UnionFind(size_t sz) : data(sz, -1) {}

  bool unite(int x, int y) {
    x = find(x), y = find(y);
    if(x == y) return false;
    if(data[x] > data[y]) swap(x, y);
    data[x] += data[y];
    data[y] = x;
    return true;
  }

  int find(int k) {
    if(data[k] < 0) return (k);
    return data[k] = find(data[k]);
  }

  int size(int k) {
    return -data[find(k)];
  }

  bool same(int x, int y) {
    return find(x) == find(y);
  }
};
#line 9 "test/verify/yosupo-tree-decomposition-width-2.test.cpp"

#line 1 "graph/others/tree-decomposition.cpp"
/**
 * @brief Tree-Decomposition(木分解)
 * @see https://ei1333.hateblo.jp/entry/2020/02/12/150319
 */
struct DecompNode {
  vector< int > bag, child;

  DecompNode() = default;
};

struct TreeDecomposition {

  vector< vector< int > > g;

  explicit TreeDecomposition(int V) : g(V) {}

  void add_edge(int a, int b) {
    g[a].emplace_back(b);
    g[b].emplace_back(a);
  }

  vector< DecompNode > build() {
    const int N = (int) g.size();

    vector< int > used(N, -1), deg(N);
    queue< int > que;
    for(int i = 0; i < N; i++) {
      deg[i] = (int) g[i].size();
      if(deg[i] <= 2) que.emplace(i);
    }

    vector< set< int > > exists(N);
    for(int i = 0; i < N; i++) {
      for(auto &j : g[i]) {
        if(i < j) exists[i].emplace(j);
      }
    }

    vector< DecompNode > ret;
    ret.emplace_back();
    while(!que.empty()) {
      int idx = que.front();
      que.pop();
      if(deg[idx] > 2 || used[idx] != -1) continue;

      DecompNode r;
      r.bag.emplace_back(idx);
      int u = -1, v = -1;
      for(auto &to : g[idx]) {
        if(used[to] == -1) {
          (u == -1 ? u : v) = to;
          r.bag.emplace_back(to);
        } else if(used[to] >= 0) {
          r.child.emplace_back(used[to]);
          used[to] = -2;
        }
      }

      if(u == -1) {

      } else if(v == -1) {
        --deg[u];
      } else {
        if(u > v) swap(u, v);
        if(!exists[u].count(v)) {
          g[u].emplace_back(v);
          g[v].emplace_back(u);
          exists[u].emplace(v);
        } else {
          --deg[u];
          --deg[v];
        }
      }

      for(auto &to : g[idx]) {
        if(deg[to] <= 2) que.emplace(to);
      }

      used[idx] = (int) ret.size();
      deg[idx] = 0;
      ret.emplace_back(r);
    }
    for(int i = 0; i < N; i++) {
      if(deg[i] > 0) return {};
    }
    ret.front() = ret.back();
    ret.pop_back();
    return ret;
  }
};


void to_nice(vector< DecompNode > &g, int root = 0) {

  for(auto &p : g) {
    sort(p.bag.begin(), p.bag.end());
  }

  stack< int > st;
  st.emplace(root);

  while(!st.empty()) {
    int idx = st.top();
    st.pop();

    // join
    while(g[idx].child.size() > 2) {
      DecompNode r;
      r.child.resize(2);
      r.child[0] = g[idx].child.back();
      g[idx].child.pop_back();
      r.child[1] = g[idx].child.back();
      g[idx].child.pop_back();
      r.bag = g[idx].bag;
      g[idx].child.emplace_back((int) g.size());
      g.emplace_back(r);
    }

    if(g[idx].child.size() == 2) {
      for(auto &ch : g[idx].child) {
        if(g[ch].bag != g[idx].bag) {
          DecompNode r;
          r.child = {ch};
          r.bag = g[idx].bag;
          ch = (int) g.size();
          g.emplace_back(r);
        }
      }
    }

    // introduce / forget
    if(g[idx].child.size() == 1) {
      int &ch = g[idx].child[0];

      vector< int > latte, malta;
      set_difference(g[idx].bag.begin(), g[idx].bag.end(),
                     g[ch].bag.begin(), g[ch].bag.end(),
                     back_inserter(latte));
      set_difference(g[ch].bag.begin(), g[ch].bag.end(),
                     g[idx].bag.begin(), g[idx].bag.end(),
                     back_inserter(malta));
      if(latte.size() + malta.size() > 1) {
        DecompNode r;
        r.child = {ch};
        r.bag = g[idx].bag;
        if(!latte.empty()) {
          r.bag.erase(find(r.bag.begin(), r.bag.end(), latte.back()));
        } else {
          r.bag.emplace_back(malta.back());
        }
        ch = (int) g.size();
        g.emplace_back(r);
      }
    }

    // leaf
    if(g[idx].child.empty()) {
      if(g[idx].bag.size() > 1) {
        DecompNode r;
        r.bag = g[idx].bag;
        r.bag.pop_back();
        g[idx].child.emplace_back((int) g.size());
        g.emplace_back(r);
      }
    }

    for(auto &ch : g[idx].child) {
      st.emplace(ch);
    }
  }
}
#line 11 "test/verify/yosupo-tree-decomposition-width-2.test.cpp"

int main() {
  string x;
  int N, M;
  Scanner pin(stdin);
  Printer pout(stdout);
  pin.read(x, x, N, M);
  vector< int > A(M), B(M);
  UnionFind uf(N);
  for(int i = 0; i < M; i++) {
    pin.read(A[i], B[i]);
    --A[i], --B[i];
    uf.unite(A[i], B[i]);
  }
  int root = -1;
  for(int i = 0; i < N; i++) {
    if(uf.find(i) == i) {
      if(root == -1) {
        root = i;
      } else {
        A.emplace_back(root);
        B.emplace_back(i);
      }
    }
  }
  TreeDecomposition td(N);
  for(int i = 0; i < A.size(); i++) {
    td.add_edge(A[i], B[i]);
  }
  auto tap = td.build();
  if(tap.empty()) {
    pout.writeln("-1");
    return 0;
  }
  pout.writeln("s", "td", tap.size(), 2, N);
  for(int i = 0; i < tap.size(); i++) {
    for(auto &t : tap[i].bag) ++t;
    pout.writeln("b", i + 1, tap[i].bag);
  }
  for(int i = 0; i < tap.size(); i++) {
    for(auto &t : tap[i].child) pout.writeln(i + 1, t + 1);
  }
}

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

