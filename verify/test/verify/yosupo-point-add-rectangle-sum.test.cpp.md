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


# :heavy_check_mark: test/verify/yosupo-point-add-rectangle-sum.test.cpp

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#5a4423c79a88aeb6104a40a645f9430c">test/verify</a>
* <a href="{{ site.github.repository_url }}/blob/master/test/verify/yosupo-point-add-rectangle-sum.test.cpp">View this file on GitHub</a>
    - Last commit date: 2020-06-17 14:58:48+09:00


* see: <a href="https://judge.yosupo.jp/problem/point_add_rectangle_sum">https://judge.yosupo.jp/problem/point_add_rectangle_sum</a>


## Depends on

* :heavy_check_mark: <a href="../../../library/other/printer.cpp.html">Printer(高速出力) <small>(other/printer.cpp)</small></a>
* :heavy_check_mark: <a href="../../../library/other/scanner.cpp.html">Scanner(高速入力) <small>(other/scanner.cpp)</small></a>
* :heavy_check_mark: <a href="../../../library/structure/others/binary-indexed-tree.cpp.html">Binary-Indexed-Tree(BIT) <small>(structure/others/binary-indexed-tree.cpp)</small></a>
* :heavy_check_mark: <a href="../../../library/structure/wavelet/succinct-indexable-dictionary.cpp.html">structure/wavelet/succinct-indexable-dictionary.cpp</a>
* :heavy_check_mark: <a href="../../../library/structure/wavelet/wavelet-matrix-point-add-rectangle-sum.cpp.html">structure/wavelet/wavelet-matrix-point-add-rectangle-sum.cpp</a>
* :heavy_check_mark: <a href="../../../library/template/template.cpp.html">template/template.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
#define PROBLEM "https://judge.yosupo.jp/problem/point_add_rectangle_sum"

#include "../../template/template.cpp"

#include "../../structure/others/binary-indexed-tree.cpp"

#include "../../structure/wavelet/succinct-indexable-dictionary.cpp"
#include "../../structure/wavelet/wavelet-matrix-point-add-rectangle-sum.cpp"

#include "../../other/scanner.cpp"
#include "../../other/printer.cpp"

int main() {
  Scanner in(stdin);
  Printer out(stdout);
  int N, Q;
  in.read(N, Q);
  vector< int > x(N), y(N), w(N);
  vector< pair< int, int > > xs;
  xs.reserve(N + Q);
  for(int i = 0; i < N; i++) {
    in.read(x[i], y[i], w[i]);
    xs.emplace_back(x[i], y[i]);
  }
  vector< int > t(Q), a(Q), b(Q), c(Q), d(Q);
  for(int i = 0; i < Q; i++) {
    in.read(t[i], a[i], b[i], c[i]);
    if(t[i] == 0) xs.emplace_back(a[i], b[i]);
    else in.read(d[i]);
  }
  sort(begin(xs), end(xs));
  xs.erase(unique(begin(xs), end(xs)), end(xs));
  vector< int > ys(xs.size());
  for(int i = 0; i < xs.size(); i++) ys[i] = xs[i].second;
  vector< int64 > ws(xs.size());
  for(int i = 0; i < N; i++) {
    x[i] = lower_bound(begin(xs), end(xs), make_pair(x[i], y[i])) - begin(xs);
    ws[x[i]] += w[i];
  }
  for(int i = 0; i < Q; i++) {
    if(t[i] == 0) {
      a[i] = lower_bound(begin(xs), end(xs), make_pair(a[i], b[i])) - begin(xs);
    } else {
      a[i] = lower_bound(begin(xs), end(xs), make_pair(a[i], -1)) - begin(xs);
      c[i] = lower_bound(begin(xs), end(xs), make_pair(c[i], -1)) - begin(xs);
    }
  }
  CompressedWaveletMatrixPointAddRectangleSum< int, 18, int64 > mat(ys, ws);
  for(int i = 0; i < Q; i++) {
    if(t[i] == 0) {
      mat.point_add(a[i], b[i], c[i]);
    } else {
      out.writeln(mat.rect_sum(a[i], c[i], b[i], d[i]));
    }
  }
}

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "test/verify/yosupo-point-add-rectangle-sum.test.cpp"
#define PROBLEM "https://judge.yosupo.jp/problem/point_add_rectangle_sum"

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
#line 4 "test/verify/yosupo-point-add-rectangle-sum.test.cpp"

#line 1 "structure/others/binary-indexed-tree.cpp"
/**
 * @brief Binary-Indexed-Tree(BIT)
 * @docs docs/binary-indexed-tree.md
 */
template< typename T >
struct BinaryIndexedTree {
  vector< T > data;

  BinaryIndexedTree() = default;

  explicit BinaryIndexedTree(size_t sz) : data(sz + 1, 0) {}

  explicit BinaryIndexedTree(const vector< T > &vs) : data(vs.size() + 1, 0) {
    for(size_t i = 0; i < vs.size(); i++) data[i + 1] = vs[i];
    for(size_t i = 1; i < data.size(); i++) {
      size_t j = i + (i & -i);
      if(j < data.size()) data[j] += data[i];
    }
  }

  void add(int k, const T &x) {
    for(++k; k < (int) data.size(); k += k & -k) data[k] += x;
  }

  T query(int k) const {
    T ret = T();
    for(++k; k > 0; k -= k & -k) ret += data[k];
    return ret;
  }

  int lower_bound(T x) const {
    int i = 0;
    for(int k = 1 << (__lg(data.size() - 1) + 1); k > 0; k >>= 1) {
      if(i + k < data.size() && data[i + k] < x) {
        x -= data[i + k];
        i += k;
      }
    }
    return i;
  }

  int upper_bound(T x) const {
    int i = 0;
    for(int k = 1 << (__lg(data.size() - 1) + 1); k > 0; k >>= 1) {
      if(i + k < data.size() && data[i + k] <= x) {
        x -= data[i + k];
        i += k;
      }
    }
    return i;
  }
};
#line 6 "test/verify/yosupo-point-add-rectangle-sum.test.cpp"

#line 1 "structure/wavelet/succinct-indexable-dictionary.cpp"
struct SuccinctIndexableDictionary {
  size_t length;
  size_t blocks;
  vector< unsigned > bit, sum;

  SuccinctIndexableDictionary() = default;

  SuccinctIndexableDictionary(size_t length) : length(length), blocks((length + 31) >> 5) {
    bit.assign(blocks, 0U);
    sum.assign(blocks, 0U);
  }

  void set(int k) {
    bit[k >> 5] |= 1U << (k & 31);
  }

  void build() {
    sum[0] = 0U;
    for(int i = 1; i < blocks; i++) {
      sum[i] = sum[i - 1] + __builtin_popcount(bit[i - 1]);
    }
  }

  bool operator[](int k) {
    return (bool((bit[k >> 5] >> (k & 31)) & 1));
  }

  int rank(int k) {
    return (sum[k >> 5] + __builtin_popcount(bit[k >> 5] & ((1U << (k & 31)) - 1)));
  }

  int rank(bool val, int k) {
    return (val ? rank(k) : k - rank(k));
  }
};
#line 1 "structure/wavelet/wavelet-matrix-point-add-rectangle-sum.cpp"
template< typename T, int MAXLOG, typename D >
struct WaveletMatrixPointAddRectangleSum {
  size_t length;
  SuccinctIndexableDictionary matrix[MAXLOG];
  BinaryIndexedTree< D > ds[MAXLOG];
  int mid[MAXLOG];

  WaveletMatrixPointAddRectangleSum() = default;

  WaveletMatrixPointAddRectangleSum(const vector< T > &v, const vector< D > &d) : length(v.size()) {
    assert(v.size() == d.size());
    vector< int > l(length), r(length), ord(length);
    iota(begin(ord), end(ord), 0);
    vector< D > dd(length);
    for(int level = MAXLOG - 1; level >= 0; level--) {
      matrix[level] = SuccinctIndexableDictionary(length + 1);
      int left = 0, right = 0;
      for(int i = 0; i < length; i++) {
        if(((v[ord[i]] >> level) & 1)) {
          matrix[level].set(i);
          r[right++] = ord[i];
        } else {
          l[left++] = ord[i];
        }
      }
      mid[level] = left;
      matrix[level].build();
      ord.swap(l);
      for(int i = 0; i < right; i++) {
        ord[left + i] = r[i];
      }
      for(int i = 0; i < length; i++) {
        dd[i] = d[ord[i]];
      }
      ds[level] = BinaryIndexedTree< D >(dd);
    }
  }

  pair< int, int > succ(bool f, int l, int r, int level) {
    return {matrix[level].rank(f, l) + mid[level] * f, matrix[level].rank(f, r) + mid[level] * f};
  }

  // count d[i] s.t. (l <= i < r) && (v[i] < upper)
  D rect_sum(int l, int r, T upper) {
    D ret = 0;
    for(int level = MAXLOG - 1; level >= 0; level--) {
      bool f = ((upper >> level) & 1);
      if(f) ret += ds[level].query(matrix[level].rank(false, r) - 1) - ds[level].query(matrix[level].rank(false, l) - 1);
      tie(l, r) = succ(f, l, r, level);
    }
    return ret;
  }

  D rect_sum(int l, int r, T lower, T upper) {
    return rect_sum(l, r, upper) - rect_sum(l, r, lower);
  }

  void point_add(int k, T y, const D &x) {
    for(int level = MAXLOG - 1; level >= 0; level--) {
      bool f = ((y >> level) & 1);
      k = matrix[level].rank(f, k) + mid[level] * f;
      ds[level].add(k, x);
    }
  }
};

template< typename T, int MAXLOG, typename D >
struct CompressedWaveletMatrixPointAddRectangleSum {
  WaveletMatrixPointAddRectangleSum< int, MAXLOG, D > mat;
  vector< T > ys;

  CompressedWaveletMatrixPointAddRectangleSum(const vector< T > &v, const vector< D > &d) : ys(v) {
    sort(begin(ys), end(ys));
    ys.erase(unique(begin(ys), end(ys)), end(ys));
    vector< int > t(v.size());
    for(int i = 0; i < v.size(); i++) t[i] = get(v[i]);
    mat = WaveletMatrixPointAddRectangleSum< int, MAXLOG, D >(t, d);
  }

  inline int get(const T &x) {
    return lower_bound(begin(ys), end(ys), x) - begin(ys);
  }

  D rect_sum(int l, int r, T upper) {
    return mat.rect_sum(l, r, get(upper));
  }

  D rect_sum(int l, int r, T lower, T upper) {
    return mat.rect_sum(l, r, get(lower), get(upper));
  }

  void point_add(int k, T y, const D &x) {
    mat.point_add(k, get(y), x);
  }
};
#line 9 "test/verify/yosupo-point-add-rectangle-sum.test.cpp"

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
#line 12 "test/verify/yosupo-point-add-rectangle-sum.test.cpp"

int main() {
  Scanner in(stdin);
  Printer out(stdout);
  int N, Q;
  in.read(N, Q);
  vector< int > x(N), y(N), w(N);
  vector< pair< int, int > > xs;
  xs.reserve(N + Q);
  for(int i = 0; i < N; i++) {
    in.read(x[i], y[i], w[i]);
    xs.emplace_back(x[i], y[i]);
  }
  vector< int > t(Q), a(Q), b(Q), c(Q), d(Q);
  for(int i = 0; i < Q; i++) {
    in.read(t[i], a[i], b[i], c[i]);
    if(t[i] == 0) xs.emplace_back(a[i], b[i]);
    else in.read(d[i]);
  }
  sort(begin(xs), end(xs));
  xs.erase(unique(begin(xs), end(xs)), end(xs));
  vector< int > ys(xs.size());
  for(int i = 0; i < xs.size(); i++) ys[i] = xs[i].second;
  vector< int64 > ws(xs.size());
  for(int i = 0; i < N; i++) {
    x[i] = lower_bound(begin(xs), end(xs), make_pair(x[i], y[i])) - begin(xs);
    ws[x[i]] += w[i];
  }
  for(int i = 0; i < Q; i++) {
    if(t[i] == 0) {
      a[i] = lower_bound(begin(xs), end(xs), make_pair(a[i], b[i])) - begin(xs);
    } else {
      a[i] = lower_bound(begin(xs), end(xs), make_pair(a[i], -1)) - begin(xs);
      c[i] = lower_bound(begin(xs), end(xs), make_pair(c[i], -1)) - begin(xs);
    }
  }
  CompressedWaveletMatrixPointAddRectangleSum< int, 18, int64 > mat(ys, ws);
  for(int i = 0; i < Q; i++) {
    if(t[i] == 0) {
      mat.point_add(a[i], b[i], c[i]);
    } else {
      out.writeln(mat.rect_sum(a[i], c[i], b[i], d[i]));
    }
  }
}

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

