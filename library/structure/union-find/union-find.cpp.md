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


# :warning: structure/union-find/union-find.cpp
* category: structure/union-find


[Back to top page](../../../index.html)



## Verified
* :warning: [test/verify/aoj-dsl-1-a.test.cpp](../../../verify/test/verify/aoj-dsl-1-a.test.cpp.html)
* :warning: [test/verify/aoj-grl-2-a-2.test.cpp](../../../verify/test/verify/aoj-grl-2-a-2.test.cpp.html)
* :warning: [test/verify/aoj-grl-2-a-3.test.cpp](../../../verify/test/verify/aoj-grl-2-a-3.test.cpp.html)
* :warning: [test/verify/aoj-grl-2-b.test.cpp](../../../verify/test/verify/aoj-grl-2-b.test.cpp.html)


## Code
```cpp
struct UnionFind {
  vector< int > data;
 
  UnionFind(int sz) {
    data.assign(sz, -1);
  }
 
  bool unite(int x, int y) {
    x = find(x), y = find(y);
    if(x == y) return (false);
    if(data[x] > data[y]) swap(x, y);
    data[x] += data[y];
    data[y] = x;
    return (true);
  }
 
  int find(int k) {
    if(data[k] < 0) return (k);
    return (data[k] = find(data[k]));
  }
 
  int size(int k) {
    return (-data[find(k)]);
  }
};

```

[Back to top page](../../../index.html)

