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


# :warning: structure/union-find/persistent-union-find.cpp

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#16695eacefd17254ea5bccf40066c856">structure/union-find</a>
* <a href="{{ site.github.repository_url }}/blob/master/structure/union-find/persistent-union-find.cpp">View this file on GitHub</a>
    - Last commit date: 2019-11-30 22:41:48+09:00




## Code

<a id="unbundled"></a>
{% raw %}
```cpp
struct PersistentUnionFind
{
  PersistentArray< int, 3 > data;

  PersistentUnionFind() {}

  PersistentUnionFind(int sz)
  {
    data.build(vector< int >(sz, -1));
  }

  int find(int k)
  {
    int p = data.get(k);
    return p >= 0 ? find(p) : k;
  }

  int size(int k)
  {
    return (-data.get(find(k)));
  }

  PersistentUnionFind unite(int x, int y)
  {
    x = find(x);
    y = find(y);
    if(x == y) return *this;
    auto u = data.get(x);
    auto v = data.get(y);

    if(u < v) {
      auto a = data.mutable_get(x);
      *a += v;
      auto b = data.mutable_get(y);
      *b = x;
    } else {
      auto a = data.mutable_get(y);
      *a += u;
      auto b = data.mutable_get(x);
      *b = y;
    }
    return *this;
  }
};

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "structure/union-find/persistent-union-find.cpp"
struct PersistentUnionFind
{
  PersistentArray< int, 3 > data;

  PersistentUnionFind() {}

  PersistentUnionFind(int sz)
  {
    data.build(vector< int >(sz, -1));
  }

  int find(int k)
  {
    int p = data.get(k);
    return p >= 0 ? find(p) : k;
  }

  int size(int k)
  {
    return (-data.get(find(k)));
  }

  PersistentUnionFind unite(int x, int y)
  {
    x = find(x);
    y = find(y);
    if(x == y) return *this;
    auto u = data.get(x);
    auto v = data.get(y);

    if(u < v) {
      auto a = data.mutable_get(x);
      *a += v;
      auto b = data.mutable_get(y);
      *b = x;
    } else {
      auto a = data.mutable_get(y);
      *a += u;
      auto b = data.mutable_get(x);
      *b = y;
    }
    return *this;
  }
};

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

