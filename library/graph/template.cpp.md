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


# :warning: graph/template.cpp
* category: graph


[Back to top page](../../index.html)



## Verified
* :warning: [graph/verify/aoj-grl-1-a-2.test.cpp](../../verify/graph/verify/aoj-grl-1-a-2.test.cpp.html)
* :warning: [graph/verify/aoj-grl-1-a-3.test.cpp](../../verify/graph/verify/aoj-grl-1-a-3.test.cpp.html)
* :warning: [graph/verify/aoj-grl-1-a.test.cpp](../../verify/graph/verify/aoj-grl-1-a.test.cpp.html)
* :warning: [graph/verify/aoj-grl-1-b-2.test.cpp](../../verify/graph/verify/aoj-grl-1-b-2.test.cpp.html)
* :warning: [graph/verify/aoj-grl-1-b.test.cpp](../../verify/graph/verify/aoj-grl-1-b.test.cpp.html)
* :warning: [graph/verify/aoj-grl-1-c.test.cpp](../../verify/graph/verify/aoj-grl-1-c.test.cpp.html)
* :warning: [graph/verify/aoj-grl-2-a-2.test.cpp](../../verify/graph/verify/aoj-grl-2-a-2.test.cpp.html)
* :warning: [graph/verify/aoj-grl-2-a-3.test.cpp](../../verify/graph/verify/aoj-grl-2-a-3.test.cpp.html)
* :warning: [graph/verify/aoj-grl-2-a-4.test.cpp](../../verify/graph/verify/aoj-grl-2-a-4.test.cpp.html)
* :warning: [graph/verify/aoj-grl-2-a.test.cpp](../../verify/graph/verify/aoj-grl-2-a.test.cpp.html)
* :warning: [graph/verify/aoj-grl-2-b.test.cpp](../../verify/graph/verify/aoj-grl-2-b.test.cpp.html)
* :warning: [graph/verify/aoj-grl-3-a.test.cpp](../../verify/graph/verify/aoj-grl-3-a.test.cpp.html)
* :warning: [graph/verify/aoj-grl-3-b.test.cpp](../../verify/graph/verify/aoj-grl-3-b.test.cpp.html)
* :warning: [graph/verify/aoj-grl-3-c.test.cpp](../../verify/graph/verify/aoj-grl-3-c.test.cpp.html)
* :warning: [graph/verify/aoj-grl-6-a-2.test.cpp](../../verify/graph/verify/aoj-grl-6-a-2.test.cpp.html)
* :warning: [graph/verify/aoj-grl-6-a-3.test.cpp](../../verify/graph/verify/aoj-grl-6-a-3.test.cpp.html)
* :warning: [graph/verify/aoj-grl-6-a.test.cpp](../../verify/graph/verify/aoj-grl-6-a.test.cpp.html)
* :warning: [graph/verify/aoj-grl-6-b.test.cpp](../../verify/graph/verify/aoj-grl-6-b.test.cpp.html)
* :warning: [graph/verify/aoj-grl-7-a-2.test.cpp](../../verify/graph/verify/aoj-grl-7-a-2.test.cpp.html)
* :warning: [graph/verify/aoj-grl-7-a.test.cpp](../../verify/graph/verify/aoj-grl-7-a.test.cpp.html)
* :warning: [tree/verify/aoj-grl-5-a.test.cpp](../../verify/tree/verify/aoj-grl-5-a.test.cpp.html)
* :warning: [tree/verify/aoj-grl-5-c-2.test.cpp](../../verify/tree/verify/aoj-grl-5-c-2.test.cpp.html)
* :warning: [tree/verify/aoj-grl-5-c.test.cpp](../../verify/tree/verify/aoj-grl-5-c.test.cpp.html)


## Code
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

[Back to top page](../../index.html)

