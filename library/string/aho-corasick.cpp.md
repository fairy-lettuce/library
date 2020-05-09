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
<script type="text/javascript" src="../../assets/js/copy-button.js"></script>
<link rel="stylesheet" href="../../assets/css/copy-button.css" />


# :heavy_check_mark: Aho-Corasick(エイホ–コラシック法) <small>(string/aho-corasick.cpp)</small>

<a href="../../index.html">Back to top page</a>

* category: <a href="../../index.html#b45cffe084dd3d20d928bee85e7b0f21">string</a>
* <a href="{{ site.github.repository_url }}/blob/master/string/aho-corasick.cpp">View this file on GitHub</a>
    - Last commit date: 2020-05-10 01:03:47+09:00




## 概要

複数文字列に対するパターンマッチングオートマトンを構築する.

Trie のそれぞれのノードがオートマトンのある状態に相当する.

* `build()`: 現在のTrieをもとにオートマトンを構築する.
* `match(str, now)`: 現状態が `now` で, 文字列 `str` が現れた時に, 新たに各パターン文字列にマッチした回数を返す.
* `move(c, now)`: 現状態が `now` で, 文字 `c` が現れたときに, 新たにパターン文字列にマッチした個数と, 次状態を返す.

## 計算量

* `build()`: パターン文字列の長さの総和
* クエリ: $O(1)$


## Verified with

* :heavy_check_mark: <a href="../../verify/test/verify/yukicoder-430.test.cpp.html">test/verify/yukicoder-430.test.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
/**
 * @brief Aho-Corasick(エイホ–コラシック法)
 * @docs docs/aho-corasick.md
 */
template< int char_size, int margin >
struct AhoCorasick : Trie< char_size + 1, margin > {
  using Trie< char_size + 1, margin >::Trie;

  const int FAIL = char_size;
  vector< int > correct;

  void build(bool heavy = true) {
    correct.resize(this->size());
    for(int i = 0; i < this->size(); i++) {
      correct[i] = (int) this->nodes[i].accept.size();
    }
    queue< int > que;
    for(int i = 0; i <= char_size; i++) {
      if(~this->nodes[0].nxt[i]) {
        this->nodes[this->nodes[0].nxt[i]].nxt[FAIL] = 0;
        que.emplace(this->nodes[0].nxt[i]);
      } else {
        this->nodes[0].nxt[i] = 0;
      }
    }
    while(!que.empty()) {
      auto &now = this->nodes[que.front()];
      int fail = now.nxt[FAIL];
      correct[que.front()] += correct[fail];
      que.pop();
      for(int i = 0; i < char_size; i++) {
        if(~now.nxt[i]) {
          this->nodes[now.nxt[i]].nxt[FAIL] = this->nodes[fail].nxt[i];
          if(heavy) {
            auto &u = this->nodes[now.nxt[i]].accept;
            auto &v = this->nodes[this->nodes[fail].nxt[i]].accept;
            vector< int > accept;
            set_union(begin(u), end(u), begin(v), end(v), back_inserter(accept));
            u = accept;
          }
          que.emplace(now.nxt[i]);
        } else {
          now.nxt[i] = this->nodes[fail].nxt[i];
        }
      }
    }
  }

  map< int, int > match(const string &str, int now = 0) {
    map< int, int > result;
    for(auto &c : str) {
      now = this->nodes[now].nxt[c - margin];
      for(auto &v : this->nodes[now].accept) result[v] += 1;
    }
    return result;
  }

  pair< int64_t, int > move(const char &c, int now = 0) {
    now = this->nodes[now].nxt[c - margin];
    return {correct[now], now};
  }

  pair< int64_t, int > move(const string &str, int now = 0) {
    int64_t sum = 0;
    for(auto &c : str) {
      auto nxt = move(c, now);
      sum += nxt.first;
      now = nxt.second;
    }
    return {sum, now};
  }
};

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "string/aho-corasick.cpp"
/**
 * @brief Aho-Corasick(エイホ–コラシック法)
 * @docs docs/aho-corasick.md
 */
template< int char_size, int margin >
struct AhoCorasick : Trie< char_size + 1, margin > {
  using Trie< char_size + 1, margin >::Trie;

  const int FAIL = char_size;
  vector< int > correct;

  void build(bool heavy = true) {
    correct.resize(this->size());
    for(int i = 0; i < this->size(); i++) {
      correct[i] = (int) this->nodes[i].accept.size();
    }
    queue< int > que;
    for(int i = 0; i <= char_size; i++) {
      if(~this->nodes[0].nxt[i]) {
        this->nodes[this->nodes[0].nxt[i]].nxt[FAIL] = 0;
        que.emplace(this->nodes[0].nxt[i]);
      } else {
        this->nodes[0].nxt[i] = 0;
      }
    }
    while(!que.empty()) {
      auto &now = this->nodes[que.front()];
      int fail = now.nxt[FAIL];
      correct[que.front()] += correct[fail];
      que.pop();
      for(int i = 0; i < char_size; i++) {
        if(~now.nxt[i]) {
          this->nodes[now.nxt[i]].nxt[FAIL] = this->nodes[fail].nxt[i];
          if(heavy) {
            auto &u = this->nodes[now.nxt[i]].accept;
            auto &v = this->nodes[this->nodes[fail].nxt[i]].accept;
            vector< int > accept;
            set_union(begin(u), end(u), begin(v), end(v), back_inserter(accept));
            u = accept;
          }
          que.emplace(now.nxt[i]);
        } else {
          now.nxt[i] = this->nodes[fail].nxt[i];
        }
      }
    }
  }

  map< int, int > match(const string &str, int now = 0) {
    map< int, int > result;
    for(auto &c : str) {
      now = this->nodes[now].nxt[c - margin];
      for(auto &v : this->nodes[now].accept) result[v] += 1;
    }
    return result;
  }

  pair< int64_t, int > move(const char &c, int now = 0) {
    now = this->nodes[now].nxt[c - margin];
    return {correct[now], now};
  }

  pair< int64_t, int > move(const string &str, int now = 0) {
    int64_t sum = 0;
    for(auto &c : str) {
      auto nxt = move(c, now);
      sum += nxt.first;
      now = nxt.second;
    }
    return {sum, now};
  }
};

```
{% endraw %}

<a href="../../index.html">Back to top page</a>

