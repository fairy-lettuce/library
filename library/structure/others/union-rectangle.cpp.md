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


# :warning: structure/others/union-rectangle.cpp

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#40d73e22b7d986e3399449c25c8b23a1">structure/others</a>
* <a href="{{ site.github.repository_url }}/blob/master/structure/others/union-rectangle.cpp">View this file on GitHub</a>
    - Last commit date: 2019-11-30 22:41:48+09:00




## Code

<a id="unbundled"></a>
{% raw %}
```cpp
template< typename T >
struct UnionRectangle {
  map< T, T > data;
  int64 sum;

  UnionRectangle() : sum(0) {
    const T INF = numeric_limits< T >::max();
    data[0] = INF;
    data[INF] = 0;
  }
  void add_point(T x, T y) {
    auto p = data.lower_bound(x);
    if(p->second >= y) return;
    const T nxtY = p->second;
    --p;
    while(p->second <= y) {
      auto it = *p;
      p = --data.erase(p);
      sum -= (it.first - p->first) * (it.second - nxtY);
    }
    sum += (x - p->first) * (y - nxtY);
    data[x] = y;
  }

  int64 get() {
    return sum;
  }
};

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "structure/others/union-rectangle.cpp"
template< typename T >
struct UnionRectangle {
  map< T, T > data;
  int64 sum;

  UnionRectangle() : sum(0) {
    const T INF = numeric_limits< T >::max();
    data[0] = INF;
    data[INF] = 0;
  }
  void add_point(T x, T y) {
    auto p = data.lower_bound(x);
    if(p->second >= y) return;
    const T nxtY = p->second;
    --p;
    while(p->second <= y) {
      auto it = *p;
      p = --data.erase(p);
      sum -= (it.first - p->first) * (it.second - nxtY);
    }
    sum += (x - p->first) * (y - nxtY);
    data[x] = y;
  }

  int64 get() {
    return sum;
  }
};

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

