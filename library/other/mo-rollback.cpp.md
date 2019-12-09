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


# :warning: other/mo-rollback.cpp
* category: other


[Back to top page](../../index.html)



## Code
{% raw %}
```cpp
struct MoRollBack {
  using ADD = function< void(int) >;
  using REM = function< void(int) >;
  using RESET = function< void() >;
  using SNAPSHOT = function< void() >;
  using ROLLBACK = function< void() >;

  int width;
  vector< int > left, right, order;

  MoRollBack(int N, int Q) : width((int) sqrt(N)), order(Q) {
    iota(begin(order), end(order), 0);
  }

  void add(int l, int r) { /* [l, r) */
    left.emplace_back(l);
    right.emplace_back(r);
  }

  int run(const ADD &add, const REM &rem, const RESET &reset, const SNAPSHOT &snapshot, const ROLLBACK &rollback) {
    assert(left.size() == order.size());
    sort(begin(order), end(order), [&](int a, int b) {
      int ablock = left[a] / width, bblock = left[b] / width;
      if(ablock != bblock) return ablock < bblock;
      return right[a] < right[b];
    });
    reset();
    for(auto idx : order) {
      if(right[idx] - left[idx] < width) {
        for(int i = left[idx]; i < right[idx]; i++) add(i);
        rem(idx);
        rollback();
      }
    }
    int nr = 0, last_block = -1;
    for(auto idx : order) {
      if(right[idx] - left[idx] < width) continue;
      int block = left[idx] / width;
      if(last_block != block) {
        reset();
        last_block = block;
        nr = (block + 1) * width;
      }
      while(nr < right[idx]) add(nr++);
      snapshot();
      for(int j = (block + 1) * width - 1; j >= left[idx]; j--) add(j);
      rem(idx);
      rollback();
    }
  }
};


```
{% endraw %}

[Back to top page](../../index.html)

