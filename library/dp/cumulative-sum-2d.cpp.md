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


# :warning: dp/cumulative-sum-2d.cpp
<a href="../../index.html">Back to top page</a>

* category: dp
* <a href="{{ site.github.repository_url }}/blob/master/dp/cumulative-sum-2d.cpp">View this file on GitHub</a>
    - Last commit date: 2019-07-20 01:29:30 +0900




## Code
{% raw %}
```cpp
template< class T >
struct CumulativeSum2D {
  vector< vector< T > > data;

  CumulativeSum2D(int W, int H) : data(W + 1, vector< int >(H + 1, 0)) {}

  void add(int x, int y, T z) {
    ++x, ++y;
    if(x >= data.size() || y >= data[0].size()) return;
    data[x][y] += z;
  }

  void build() {
    for(int i = 1; i < data.size(); i++) {
      for(int j = 1; j < data[i].size(); j++) {
        data[i][j] += data[i][j - 1] + data[i - 1][j] - data[i - 1][j - 1];
      }
    }
  }

  T query(int sx, int sy, int gx, int gy) {
    return (data[gx][gy] - data[sx][gy] - data[gx][sy] + data[sx][sy]);
  }
};

```
{% endraw %}

<a href="../../index.html">Back to top page</a>

