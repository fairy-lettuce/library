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


# :x: Persistent-Binary-Trie <small>(structure/trie/persistent-binary-trie.cpp)</small>

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#495454930b047da7eed81bd52d55784a">structure/trie</a>
* <a href="{{ site.github.repository_url }}/blob/master/structure/trie/persistent-binary-trie.cpp">View this file on GitHub</a>
    - Last commit date: 2020-08-14 17:23:13+09:00




## Verified with

* :x: <a href="../../../verify/test/verify/aoj-2270.test.cpp.html">test/verify/aoj-2270.test.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
/**
 * @brief Persistent-Binary-Trie
 */
template< typename T, int MAX_LOG, typename D = int >
struct PersistentBinaryTrie : BinaryTrie< T, MAX_LOG, D > {
  using BinaryTrie< T, MAX_LOG, D >::BinaryTrie;
  using Node = typename BinaryTrie< T, MAX_LOG, D >::Node;
private:
  Node *clone(Node *t) { return new Node(*t); }
};

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "structure/trie/persistent-binary-trie.cpp"
/**
 * @brief Persistent-Binary-Trie
 */
template< typename T, int MAX_LOG, typename D = int >
struct PersistentBinaryTrie : BinaryTrie< T, MAX_LOG, D > {
  using BinaryTrie< T, MAX_LOG, D >::BinaryTrie;
  using Node = typename BinaryTrie< T, MAX_LOG, D >::Node;
private:
  Node *clone(Node *t) { return new Node(*t); }
};

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

