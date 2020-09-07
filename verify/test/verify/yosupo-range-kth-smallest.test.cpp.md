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


# :heavy_check_mark: test/verify/yosupo-range-kth-smallest.test.cpp

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#5a4423c79a88aeb6104a40a645f9430c">test/verify</a>
* <a href="{{ site.github.repository_url }}/blob/master/test/verify/yosupo-range-kth-smallest.test.cpp">View this file on GitHub</a>
    - Last commit date: 2020-08-20 02:29:21+09:00


* see: <a href="https://judge.yosupo.jp/problem/range_kth_smallest">https://judge.yosupo.jp/problem/range_kth_smallest</a>


## Depends on

* :heavy_check_mark: <a href="../../../library/structure/wavelet/succinct-indexable-dictionary.cpp.html">structure/wavelet/succinct-indexable-dictionary.cpp</a>
* :heavy_check_mark: <a href="../../../library/structure/wavelet/wavelet-matrix.cpp.html">Wavelet-Matrix(ウェーブレット行列) <small>(structure/wavelet/wavelet-matrix.cpp)</small></a>
* :heavy_check_mark: <a href="../../../library/template/template.cpp.html">template/template.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
#define PROBLEM "https://judge.yosupo.jp/problem/range_kth_smallest"

#include "../../template/template.cpp"

#include "../../structure/wavelet/succinct-indexable-dictionary.cpp"
#include "../../structure/wavelet/wavelet-matrix.cpp"

int main() {
  int N, Q;
  cin >> N >> Q;
  vector< int > A(N);
  cin >> A;
  CompressedWaveletMatrix< int, 18 > mat(A);
  for(int i = 0; i < Q; i++) {
    int a, b, c;
    cin >> a >> b >> c;
    cout << mat.kth_smallest(a, b, c) << "\n";
  }
}

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "test/verify/yosupo-range-kth-smallest.test.cpp"
#define PROBLEM "https://judge.yosupo.jp/problem/range_kth_smallest"

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
#line 4 "test/verify/yosupo-range-kth-smallest.test.cpp"

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
#line 1 "structure/wavelet/wavelet-matrix.cpp"
/*
 * @brief Wavelet-Matrix(ウェーブレット行列)
 * @docs docs/wavelet-matrix.md
 */
template< typename T, int MAXLOG >
struct WaveletMatrix {
  size_t length;
  SuccinctIndexableDictionary matrix[MAXLOG];
  int mid[MAXLOG];

  WaveletMatrix() = default;

  WaveletMatrix(vector< T > v) : length(v.size()) {
    vector< T > l(length), r(length);
    for(int level = MAXLOG - 1; level >= 0; level--) {
      matrix[level] = SuccinctIndexableDictionary(length + 1);
      int left = 0, right = 0;
      for(int i = 0; i < length; i++) {
        if(((v[i] >> level) & 1)) {
          matrix[level].set(i);
          r[right++] = v[i];
        } else {
          l[left++] = v[i];
        }
      }
      mid[level] = left;
      matrix[level].build();
      v.swap(l);
      for(int i = 0; i < right; i++) {
        v[left + i] = r[i];
      }
    }
  }

  pair< int, int > succ(bool f, int l, int r, int level) {
    return {matrix[level].rank(f, l) + mid[level] * f, matrix[level].rank(f, r) + mid[level] * f};
  }

  // v[k]
  T access(int k) {
    T ret = 0;
    for(int level = MAXLOG - 1; level >= 0; level--) {
      bool f = matrix[level][k];
      if(f) ret |= T(1) << level;
      k = matrix[level].rank(f, k) + mid[level] * f;
    }
    return ret;
  }

  T operator[](const int &k) {
    return access(k);
  }

  // count i s.t. (0 <= i < r) && v[i] == x
  int rank(const T &x, int r) {
    int l = 0;
    for(int level = MAXLOG - 1; level >= 0; level--) {
      tie(l, r) = succ((x >> level) & 1, l, r, level);
    }
    return r - l;
  }

  // k-th(0-indexed) smallest number in v[l,r)
  T kth_smallest(int l, int r, int k) {
    assert(0 <= k && k < r - l);
    T ret = 0;
    for(int level = MAXLOG - 1; level >= 0; level--) {
      int cnt = matrix[level].rank(false, r) - matrix[level].rank(false, l);
      bool f = cnt <= k;
      if(f) {
        ret |= T(1) << level;
        k -= cnt;
      }
      tie(l, r) = succ(f, l, r, level);
    }
    return ret;
  }

  // k-th(0-indexed) largest number in v[l,r)
  T kth_largest(int l, int r, int k) {
    return kth_smallest(l, r, r - l - k - 1);
  }

  // count i s.t. (l <= i < r) && (v[i] < upper)
  int range_freq(int l, int r, T upper) {
    int ret = 0;
    for(int level = MAXLOG - 1; level >= 0; level--) {
      bool f = ((upper >> level) & 1);
      if(f) ret += matrix[level].rank(false, r) - matrix[level].rank(false, l);
      tie(l, r) = succ(f, l, r, level);
    }
    return ret;
  }

  // count i s.t. (l <= i < r) && (lower <= v[i] < upper)
  int range_freq(int l, int r, T lower, T upper) {
    return range_freq(l, r, upper) - range_freq(l, r, lower);
  }

  // max v[i] s.t. (l <= i < r) && (v[i] < upper)
  T prev_value(int l, int r, T upper) {
    int cnt = range_freq(l, r, upper);
    return cnt == 0 ? T(-1) : kth_smallest(l, r, cnt - 1);
  }

  // min v[i] s.t. (l <= i < r) && (lower <= v[i])
  T next_value(int l, int r, T lower) {
    int cnt = range_freq(l, r, lower);
    return cnt == r - l ? T(-1) : kth_smallest(l, r, cnt);
  }
};

template< typename T, int MAXLOG >
struct CompressedWaveletMatrix {
  WaveletMatrix< int, MAXLOG > mat;
  vector< T > ys;

  CompressedWaveletMatrix(const vector< T > &v) : ys(v) {
    sort(begin(ys), end(ys));
    ys.erase(unique(begin(ys), end(ys)), end(ys));
    vector< int > t(v.size());
    for(int i = 0; i < v.size(); i++) t[i] = get(v[i]);
    mat = WaveletMatrix< int, MAXLOG >(t);
  }

  inline int get(const T& x) {
    return lower_bound(begin(ys), end(ys), x) - begin(ys);
  }

  T access(int k) {
    return ys[mat.access(k)];
  }

  T operator[](const int &k) {
    return access(k);
  }

  int rank(const T &x, int r) {
    auto pos = get(x);
    if(pos == ys.size() || ys[pos] != x) return 0;
    return mat.rank(pos, r);
  }

  T kth_smallest(int l, int r, int k) {
    return ys[mat.kth_smallest(l, r, k)];
  }

  T kth_largest(int l, int r, int k) {
    return ys[mat.kth_largest(l, r, k)];
  }

  int range_freq(int l, int r, T upper) {
    return mat.range_freq(l, r, get(upper));
  }

  int range_freq(int l, int r, T lower, T upper) {
    return mat.range_freq(l, r, get(lower), get(upper));
  }

  T prev_value(int l, int r, T upper) {
    auto ret = mat.prev_value(l, r, get(upper));
    return ret == -1 ? T(-1) : ys[ret];
  }

  T next_value(int l, int r, T lower) {
    auto ret = mat.next_value(l, r, get(lower));
    return ret == -1 ? T(-1) : ys[ret];
  }
};
#line 7 "test/verify/yosupo-range-kth-smallest.test.cpp"

int main() {
  int N, Q;
  cin >> N >> Q;
  vector< int > A(N);
  cin >> A;
  CompressedWaveletMatrix< int, 18 > mat(A);
  for(int i = 0; i < Q; i++) {
    int a, b, c;
    cin >> a >> b >> c;
    cout << mat.kth_smallest(a, b, c) << "\n";
  }
}

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

