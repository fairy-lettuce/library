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


# :heavy_check_mark: Binary-Trie <small>(structure/trie/binary-trie.cpp)</small>

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#495454930b047da7eed81bd52d55784a">structure/trie</a>
* <a href="{{ site.github.repository_url }}/blob/master/structure/trie/binary-trie.cpp">View this file on GitHub</a>
    - Last commit date: 2020-08-14 17:23:13+09:00




## 概要

整数をビット列とみなして, トライ木のように持つデータ構造.


## 使い方

* `add(bit, idx = -1, delta = 1, xor_val = 0)`: トライ木に値 `bit` に `delta` を加える. `exist` には自分を含む部分木に追加された値の `delta` の総和, `idx` に対して $-1$ 以外を与えると `accept` にそのノードにマッチする全ての値のindexが格納される.
* `erase(bit, xor_val = 0)`: 値 `bit` に対応する `delta` に $-1$ を加える.
* `find(bit, xor_val = 0)`: 値 `bit` に対応するノードを返す. 存在しないとき `nullptr`.
* `count(bit, xor_val = 0)`: 値 `bit` に対応するノードの `delta` を返す. 存在しないとき $0$.
* `min_element(xor_val = 0)`: 最小値とそれに対応するノードを返す.
* `max_element(xor_val = 0)`: 最大値とそれに対応するノードを返す.
* `kth_element(k, xor_val = 0)`: $k$ 番目(0-indexed) に小さい値とそれに対応するノードを返す.
* `count_less(bit, xor_val = 0)`: 値 `bit` 未満の `delta` の総和を返す.

引数の最後の `xor_val` を指定すると, トライ木に存在する値全体に `xor_val` を xor とした場合の動作をする.

## 計算量

* クエリ: $O(\log V)$ 


## Verified with

* :heavy_check_mark: <a href="../../../verify/test/verify/aoj-dsl-2-b-2.test.cpp.html">test/verify/aoj-dsl-2-b-2.test.cpp</a>
* :heavy_check_mark: <a href="../../../verify/test/verify/yosupo-set-xor-min.test.cpp.html">test/verify/yosupo-set-xor-min.test.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
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

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
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

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

