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


# :heavy_check_mark: graph/template.cpp

<a href="../../index.html">Back to top page</a>

* category: <a href="../../index.html#f8b0b924ebd7046dbfa85a856e4682c8">graph</a>
* <a href="{{ site.github.repository_url }}/blob/master/graph/template.cpp">View this file on GitHub</a>
    - Last commit date: 2019-07-20 01:29:30+09:00




## Verified with

* :heavy_check_mark: <a href="../../verify/test/verify/aoj-1163.test.cpp.html">test/verify/aoj-1163.test.cpp</a>
* :heavy_check_mark: <a href="../../verify/test/verify/aoj-1254.test.cpp.html">test/verify/aoj-1254.test.cpp</a>
* :heavy_check_mark: <a href="../../verify/test/verify/aoj-2306.test.cpp.html">test/verify/aoj-2306.test.cpp</a>
* :heavy_check_mark: <a href="../../verify/test/verify/aoj-grl-1-c.test.cpp.html">test/verify/aoj-grl-1-c.test.cpp</a>
* :heavy_check_mark: <a href="../../verify/test/verify/aoj-grl-2-b.test.cpp.html">test/verify/aoj-grl-2-b.test.cpp</a>
* :heavy_check_mark: <a href="../../verify/test/verify/aoj-grl-6-b.test.cpp.html">test/verify/aoj-grl-6-b.test.cpp</a>
* :heavy_check_mark: <a href="../../verify/test/verify/yosupo-maximum-independent-set.test.cpp.html">test/verify/yosupo-maximum-independent-set.test.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
template< typename T >
struct edge {
  int src, to;
  T cost;

  edge(int to, T cost) : src(-1), to(to), cost(cost) {}

  edge(int src, int to, T cost) : src(src), to(to), cost(cost) {}

  edge &operator=(const int &x) {
    to = x;
    return *this;
  }

  operator int() const { return to; }
};

template< typename T >
using Edges = vector< edge< T > >;
template< typename T >
using WeightedGraph = vector< Edges< T > >;
using UnWeightedGraph = vector< vector< int > >;
template< typename T >
using Matrix = vector< vector< T > >;

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "graph/template.cpp"
template< typename T >
struct edge {
  int src, to;
  T cost;

  edge(int to, T cost) : src(-1), to(to), cost(cost) {}

  edge(int src, int to, T cost) : src(src), to(to), cost(cost) {}

  edge &operator=(const int &x) {
    to = x;
    return *this;
  }

  operator int() const { return to; }
};

template< typename T >
using Edges = vector< edge< T > >;
template< typename T >
using WeightedGraph = vector< Edges< T > >;
using UnWeightedGraph = vector< vector< int > >;
template< typename T >
using Matrix = vector< vector< T > >;

```
{% endraw %}

<a href="../../index.html">Back to top page</a>

