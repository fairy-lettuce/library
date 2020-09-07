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


# :heavy_check_mark: test/verify/aoj-dsl-2-b-2.test.cpp

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#5a4423c79a88aeb6104a40a645f9430c">test/verify</a>
* <a href="{{ site.github.repository_url }}/blob/master/test/verify/aoj-dsl-2-b-2.test.cpp">View this file on GitHub</a>
    - Last commit date: 2020-08-14 17:23:13+09:00


* see: <a href="http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=DSL_2_B">http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=DSL_2_B</a>


## Depends on

* :heavy_check_mark: <a href="../../../library/structure/trie/binary-trie.cpp.html">Binary-Trie <small>(structure/trie/binary-trie.cpp)</small></a>
* :question: <a href="../../../library/template/template.cpp.html">template/template.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
#define PROBLEM "http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=DSL_2_B"

#include "../../template/template.cpp"

#include "../../structure/trie/binary-trie.cpp"

int main() {
  int N, Q;
  cin >> N >> Q;
  BinaryTrie< int, 20 > bt;
  for(int i = 0; i < Q; i++) {
    int c, x, y;
    cin >> c >> x >> y;
    if(c == 0) {
      bt.add(x, -1, y);
    } else if(c == 1) {
      cout << bt.count_less(y + 1) - bt.count_less(x) << "\n";
    }
  }
}

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "test/verify/aoj-dsl-2-b-2.test.cpp"
#define PROBLEM "http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=DSL_2_B"

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
#line 4 "test/verify/aoj-dsl-2-b-2.test.cpp"

#line 1 "structure/trie/binary-trie.cpp"
/**
 * @brief Binary-Trie
 * @docs docs/binary-trie.md
 */
template< typename T, int MAX_LOG, typename D = int >
struct BinaryTrie {
public:
  struct Node {
    Node *nxt[2];
    D exist;
    vector< int > accept;

    Node() : nxt{nullptr, nullptr}, exist(0) {}
  };

  Node *root;

  explicit BinaryTrie() : root(new Node()) {}

  explicit BinaryTrie(Node *root) : root(root) {}

  void add(const T &bit, int idx = -1, D delta = 1, T xor_val = 0) {
    root = add(root, bit, idx, MAX_LOG, delta, xor_val);
  }

  void erase(const T &bit, T xor_val = 0) {
    add(bit, -1, -1, xor_val);
  }

  Node *find(const T &bit, T xor_val = 0) {
    return find(root, bit, MAX_LOG, xor_val);
  }

  D count(const T &bit, T xor_val = 0) {
    auto node = find(bit, xor_val);
    return node ? node->exist : 0;
  }

  pair< T, Node * > min_element(T xor_val = 0) {
    assert(root->exist > 0);
    return kth_element(0, xor_val);
  }

  pair< T, Node * > max_element(T xor_val = 0) {
    assert(root->exist > 0);
    return kth_element(root->exist - 1, xor_val);
  }

  pair< T, Node * > kth_element(D k, T xor_val = 0) { // 0-indexed
    assert(0 <= k && k < root->exist);
    return kth_element(root, k, MAX_LOG, xor_val);
  }

  D count_less(const T &bit, T xor_val = 0) { // < bit
    return count_less(root, bit, MAX_LOG, xor_val);
  }

private:

  virtual Node *clone(Node *t) { return t; }

  Node *add(Node *t, T bit, int idx, int depth, D x, T xor_val, bool need = true) {
    if(need) t = clone(t);
    if(depth == -1) {
      t->exist += x;
      if(idx >= 0) t->accept.emplace_back(idx);
    } else {
      bool f = (xor_val >> depth) & 1;
      auto &to = t->nxt[f ^ ((bit >> depth) & 1)];
      if(!to) to = new Node(), need = false;
      to = add(to, bit, idx, depth - 1, x, xor_val, need);
      t->exist += x;
    }
    return t;
  }

  Node *find(Node *t, T bit, int depth, T xor_val) {
    if(depth == -1) {
      return t;
    } else {
      bool f = (xor_val >> depth) & 1;
      auto &to = t->nxt[f ^ ((bit >> depth) & 1)];
      return to ? find(to, bit, depth - 1, xor_val) : nullptr;
    }
  }

  pair< T, Node * > kth_element(Node *t, D k, int bit_index, T xor_val) { // 0-indexed
    if(bit_index == -1) {
      return {0, t};
    } else {
      bool f = (xor_val >> bit_index) & 1;
      if((t->nxt[f] ? t->nxt[f]->exist : 0) <= k) {
        auto ret = kth_element(t->nxt[f ^ 1], k - (t->nxt[f] ? t->nxt[f]->exist : 0), bit_index - 1, xor_val);
        ret.first |= T(1) << bit_index;
        return ret;
      } else {
        return kth_element(t->nxt[f], k, bit_index - 1, xor_val);
      }
    }
  }

  D count_less(Node *t, const T &bit, int bit_index, T xor_val) {
    if(bit_index == -1) return 0;
    D ret = 0;
    bool f = (xor_val >> bit_index) & 1;
    if(f ^ ((bit >> bit_index) & 1)) {
      if(t->nxt[f]) ret += t->nxt[f]->exist;
      if(t->nxt[1 ^ f]) ret += count_less(t->nxt[1 ^ f], bit, bit_index - 1, xor_val);
    } else {
      if(t->nxt[f]) ret += count_less(t->nxt[f], bit, bit_index - 1, xor_val);
    }
    return ret;
  }
};
#line 6 "test/verify/aoj-dsl-2-b-2.test.cpp"

int main() {
  int N, Q;
  cin >> N >> Q;
  BinaryTrie< int, 20 > bt;
  for(int i = 0; i < Q; i++) {
    int c, x, y;
    cin >> c >> x >> y;
    if(c == 0) {
      bt.add(x, -1, y);
    } else if(c == 1) {
      cout << bt.count_less(y + 1) - bt.count_less(x) << "\n";
    }
  }
}

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

