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


# :warning: structure/heap/radix-heap.cpp
* category: structure/heap


[Back to top page](../../../index.html)



## Verified
* :heavy_check_mark: [test/verify/aoj-grl-1-a-3.test.cpp](../../../verify/test/verify/aoj-grl-1-a-3.test.cpp.html)


## Code
```cpp
template< typename key_t, typename val_t >
struct RadixHeap {
  static constexpr int bit = sizeof(key_t) * 8;
  array< vector< pair< key_t, val_t > >, bit > vs;

  size_t sz;
  key_t last;

  RadixHeap() : sz(0), last(0) {}

  bool empty() const { return sz == 0; }

  size_t size() const { return sz; }

  inline int getbit(int a) const {
    return a ? bit - __builtin_clz(a) : 0;
  }

  inline int getbit(int64_t a) const {
    return a ? bit - __builtin_clzll(a) : 0;
  }

  void push(const key_t &key, const val_t &val) {
    sz++;
    vs[getbit(key ^ last)].emplace_back(key, val);
  }

  pair< key_t, val_t > pop() {
    if(vs[0].empty()) {
      int idx = 1;
      while(vs[idx].empty()) idx++;
      last = min_element(vs[idx].begin(), vs[idx].end())->first;
      for(auto &p:vs[idx]) vs[getbit(p.first ^ last)].emplace_back(p);
      vs[idx].clear();
    }
    --sz;
    auto res = vs[0].back();
    vs[0].pop_back();
    return res;
  }
};

```

[Back to top page](../../../index.html)

