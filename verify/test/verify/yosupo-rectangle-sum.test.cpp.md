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


# :heavy_check_mark: test/verify/yosupo-rectangle-sum.test.cpp

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#5a4423c79a88aeb6104a40a645f9430c">test/verify</a>
* <a href="{{ site.github.repository_url }}/blob/master/test/verify/yosupo-rectangle-sum.test.cpp">View this file on GitHub</a>
    - Last commit date: 2020-08-14 04:28:43+09:00


* see: <a href="https://judge.yosupo.jp/problem/rectangle_sum">https://judge.yosupo.jp/problem/rectangle_sum</a>


## Depends on

* :heavy_check_mark: <a href="../../../library/structure/wavelet/succinct-indexable-dictionary.cpp.html">structure/wavelet/succinct-indexable-dictionary.cpp</a>
* :heavy_check_mark: <a href="../../../library/structure/wavelet/wavelet-matrix-rectangle-sum.cpp.html">Wavelet-Matrix-Rectangle-Sum <small>(structure/wavelet/wavelet-matrix-rectangle-sum.cpp)</small></a>
* :question: <a href="../../../library/template/template.cpp.html">template/template.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
#define PROBLEM "https://judge.yosupo.jp/problem/rectangle_sum"

#include "../../template/template.cpp"

#include "../../structure/wavelet/succinct-indexable-dictionary.cpp"
#include "../../structure/wavelet/wavelet-matrix-rectangle-sum.cpp"

int main() {
  int N, Q;
  cin >> N >> Q;
  vector< int > x(N), y(N), w(N);
  vector< pair< int, int > > xs(N);
  for(int i = 0; i < N; i++) {
    cin >> x[i] >> y[i] >> w[i];
    xs[i] = {x[i], i};
  }
  sort(begin(xs), end(xs));
  vector< int > ys(N);
  vector< int64 > ws(N);
  for(int i = 0; i < N; i++) {
    x[i] = lower_bound(begin(xs), end(xs), make_pair(x[i], i)) - begin(xs);
    ys[x[i]] = y[i];
    ws[x[i]] = w[i];
  }
  CompressedWaveletMatrixRectangleSum< int, 18, int64 > mat(ys, ws);
  while(Q--) {
    int l, r, d, u;
    cin >> l >> d >> r >> u;
    l = lower_bound(begin(xs), end(xs), make_pair(l, -1)) - begin(xs);
    r = lower_bound(begin(xs), end(xs), make_pair(r, -1)) - begin(xs);
    cout << mat.rect_sum(l, r, d, u) << "\n";
  }
}


```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "test/verify/yosupo-rectangle-sum.test.cpp"
#define PROBLEM "https://judge.yosupo.jp/problem/rectangle_sum"

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
#line 4 "test/verify/yosupo-rectangle-sum.test.cpp"

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
#line 1 "structure/wavelet/wavelet-matrix-rectangle-sum.cpp"
/*
 * @brief Wavelet-Matrix-Rectangle-Sum
 * @docs docs/wavelet-matrix-rectangle-sum.md
 */
template< typename T, int MAXLOG, typename D >
struct WaveletMatrixRectangleSum {
  size_t length;
  SuccinctIndexableDictionary matrix[MAXLOG];
  vector< D > ds[MAXLOG];
  int mid[MAXLOG];

  WaveletMatrixRectangleSum() = default;

  WaveletMatrixRectangleSum(const vector< T > &v, const vector< D > &d) : length(v.size()) {
    assert(v.size() == d.size());
    vector< int > l(length), r(length), ord(length);
    iota(begin(ord), end(ord), 0);
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
      ds[level].resize(length + 1);
      ds[level][0] = D();
      for(int i = 0; i < length; i++) {
        ds[level][i + 1] = ds[level][i] + d[ord[i]];
      }
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
      if(f) ret += ds[level][matrix[level].rank(false, r)] - ds[level][matrix[level].rank(false, l)];
      tie(l, r) = succ(f, l, r, level);
    }
    return ret;
  }

  D rect_sum(int l, int r, T lower, T upper) {
    return rect_sum(l, r, upper) - rect_sum(l, r, lower);
  }
};

template< typename T, int MAXLOG, typename D >
struct CompressedWaveletMatrixRectangleSum {
  WaveletMatrixRectangleSum< int, MAXLOG, D > mat;
  vector< T > ys;

  CompressedWaveletMatrixRectangleSum(const vector< T > &v, const vector< D > &d) : ys(v) {
    sort(begin(ys), end(ys));
    ys.erase(unique(begin(ys), end(ys)), end(ys));
    vector< int > t(v.size());
    for(int i = 0; i < v.size(); i++) t[i] = get(v[i]);
    mat = WaveletMatrixRectangleSum< int, MAXLOG, D >(t, d);
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
};

#line 7 "test/verify/yosupo-rectangle-sum.test.cpp"

int main() {
  int N, Q;
  cin >> N >> Q;
  vector< int > x(N), y(N), w(N);
  vector< pair< int, int > > xs(N);
  for(int i = 0; i < N; i++) {
    cin >> x[i] >> y[i] >> w[i];
    xs[i] = {x[i], i};
  }
  sort(begin(xs), end(xs));
  vector< int > ys(N);
  vector< int64 > ws(N);
  for(int i = 0; i < N; i++) {
    x[i] = lower_bound(begin(xs), end(xs), make_pair(x[i], i)) - begin(xs);
    ys[x[i]] = y[i];
    ws[x[i]] = w[i];
  }
  CompressedWaveletMatrixRectangleSum< int, 18, int64 > mat(ys, ws);
  while(Q--) {
    int l, r, d, u;
    cin >> l >> d >> r >> u;
    l = lower_bound(begin(xs), end(xs), make_pair(l, -1)) - begin(xs);
    r = lower_bound(begin(xs), end(xs), make_pair(r, -1)) - begin(xs);
    cout << mat.rect_sum(l, r, d, u) << "\n";
  }
}


```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

