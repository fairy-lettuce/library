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


# :heavy_check_mark: math/fps/polynomial-interpolation.cpp

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#1201bfd5f7a5d1c5bfa65e9be4237f63">math/fps</a>
* <a href="{{ site.github.repository_url }}/blob/master/math/fps/polynomial-interpolation.cpp">View this file on GitHub</a>
    - Last commit date: 2019-11-30 23:36:31+09:00




## Verified with

* :heavy_check_mark: <a href="../../../verify/test/verify/yosupo-polynomial-interpolation.test.cpp.html">test/verify/yosupo-polynomial-interpolation.test.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
template< class T >
FormalPowerSeries< T > polynomial_interpolation(const FormalPowerSeries< T > &xs, const vector< T > &ys) {
  assert(xs.size() == ys.size());
  using FPS = FormalPowerSeries< T >;
  PolyBuf< T > buf(xs);
  FPS w = buf.query(0, xs.size()).diff();
  auto vs = multipoint_evaluation(w, xs, buf);
  function< FPS(int, int) > rec = [&](int l, int r) -> FPS {
    if(r - l == 1) return {ys[l] / vs[l]};
    int m = (l + r) >> 1;
    return rec(l, m) * buf.query(m, r) + rec(m, r) * buf.query(l, m);
  };
  return rec(0, xs.size());
}

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "math/fps/polynomial-interpolation.cpp"
template< class T >
FormalPowerSeries< T > polynomial_interpolation(const FormalPowerSeries< T > &xs, const vector< T > &ys) {
  assert(xs.size() == ys.size());
  using FPS = FormalPowerSeries< T >;
  PolyBuf< T > buf(xs);
  FPS w = buf.query(0, xs.size()).diff();
  auto vs = multipoint_evaluation(w, xs, buf);
  function< FPS(int, int) > rec = [&](int l, int r) -> FPS {
    if(r - l == 1) return {ys[l] / vs[l]};
    int m = (l + r) >> 1;
    return rec(l, m) * buf.query(m, r) + rec(m, r) * buf.query(l, m);
  };
  return rec(0, xs.size());
}

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

