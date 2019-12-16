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


# :heavy_check_mark: math/fps/multipoint-evaluation.cpp

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#1201bfd5f7a5d1c5bfa65e9be4237f63">math/fps</a>
* <a href="{{ site.github.repository_url }}/blob/master/math/fps/multipoint-evaluation.cpp">View this file on GitHub</a>
    - Last commit date: 2019-11-30 23:36:31 +0900




## Verified with

* :heavy_check_mark: <a href="../../../verify/test/verify/yosupo-multipoint-evaluation.test.cpp.html">test/verify/yosupo-multipoint-evaluation.test.cpp</a>
* :heavy_check_mark: <a href="../../../verify/test/verify/yosupo-polynomial-interpolation.test.cpp.html">test/verify/yosupo-polynomial-interpolation.test.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
template< typename T >
struct PolyBuf {
  using FPS = FormalPowerSeries< T >;
  const FPS xs;
  using pi = pair< int, int >;
  map< pi, FPS > buf;

  PolyBuf(const FPS &xs) : xs(xs) {}

  const FPS &query(int l, int r) {
    if(buf.count({l, r})) return buf[{l, r}];
    if(l + 1 == r) return buf[{l, r}] = {-xs[l], 1};
    return buf[{l, r}] = query(l, (l + r) >> 1) * query((l + r) >> 1, r);
  }
};


template< typename T >
FormalPowerSeries< T > multipoint_evaluation(const FormalPowerSeries< T > &as, const FormalPowerSeries< T > &xs, PolyBuf< T > &buf) {
  using FPS = FormalPowerSeries< T >;
  FPS ret;
  const int B = 64;
  function< void(FPS, int, int) > rec = [&](FPS a, int l, int r) -> void {
    a %= buf.query(l, r);
    if(a.size() <= B) {
      for(int i = l; i < r; i++) ret.emplace_back(a.eval(xs[i]));
      return;
    }
    rec(a, l, (l + r) >> 1);
    rec(a, (l + r) >> 1, r);
  };
  rec(as, 0, xs.size());
  return ret;
};

template< typename T >
FormalPowerSeries< T > multipoint_evaluation(const FormalPowerSeries< T > &as, const FormalPowerSeries< T > &xs) {
  PolyBuf< T > buff(xs);
  return multipoint_evaluation(as, xs, buff);
}


```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "math/fps/multipoint-evaluation.cpp"
template< typename T >
struct PolyBuf {
  using FPS = FormalPowerSeries< T >;
  const FPS xs;
  using pi = pair< int, int >;
  map< pi, FPS > buf;

  PolyBuf(const FPS &xs) : xs(xs) {}

  const FPS &query(int l, int r) {
    if(buf.count({l, r})) return buf[{l, r}];
    if(l + 1 == r) return buf[{l, r}] = {-xs[l], 1};
    return buf[{l, r}] = query(l, (l + r) >> 1) * query((l + r) >> 1, r);
  }
};


template< typename T >
FormalPowerSeries< T > multipoint_evaluation(const FormalPowerSeries< T > &as, const FormalPowerSeries< T > &xs, PolyBuf< T > &buf) {
  using FPS = FormalPowerSeries< T >;
  FPS ret;
  const int B = 64;
  function< void(FPS, int, int) > rec = [&](FPS a, int l, int r) -> void {
    a %= buf.query(l, r);
    if(a.size() <= B) {
      for(int i = l; i < r; i++) ret.emplace_back(a.eval(xs[i]));
      return;
    }
    rec(a, l, (l + r) >> 1);
    rec(a, (l + r) >> 1, r);
  };
  rec(as, 0, xs.size());
  return ret;
};

template< typename T >
FormalPowerSeries< T > multipoint_evaluation(const FormalPowerSeries< T > &as, const FormalPowerSeries< T > &xs) {
  PolyBuf< T > buff(xs);
  return multipoint_evaluation(as, xs, buff);
}

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

