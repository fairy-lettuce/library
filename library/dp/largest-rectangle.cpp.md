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


# :heavy_check_mark: Largest-Rectangle(最大長方形) <small>(dp/largest-rectangle.cpp)</small>

<a href="../../index.html">Back to top page</a>

* category: <a href="../../index.html#95687afb5d9a2a9fa39038f991640b0c">dp</a>
* <a href="{{ site.github.repository_url }}/blob/master/dp/largest-rectangle.cpp">View this file on GitHub</a>
    - Last commit date: 2020-08-04 00:02:11+09:00




## 概要

ヒストグラム中の最大長方形の面積を求める.

ヒストグラムを左から見る. スタックに自分より左にあるヒストグラムの高さと位置を単調増加になるように管理すると効率的に解ける.

* `largest_rectangle(height)`: ヒストグラムが `height` のとき最大長方形の面積を返す.

## 計算量

* $O(N)$


## Verified with

* :heavy_check_mark: <a href="../../verify/test/verify/aoj-dpl-3-c.test.cpp.html">test/verify/aoj-dpl-3-c.test.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
/**
 * @brief Largest-Rectangle(最大長方形)
 * @docs docs/largest-rectangle.md
 */	
template< typename T >
int64_t largest_rectangle(vector< T > height)
{
  stack< int > st;
  height.push_back(0);
  vector< int > left(height.size());
  int64_t ret = 0;
  for(int i = 0; i < height.size(); i++) {
    while(!st.empty() && height[st.top()] >= height[i]) {
      ret = max(ret, (int64_t) (i - left[st.top()] - 1) * height[st.top()]);
      st.pop();
    }
    left[i] = st.empty() ? -1 : st.top();
    st.emplace(i);
  }
  return (ret);
}

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "dp/largest-rectangle.cpp"
/**
 * @brief Largest-Rectangle(最大長方形)
 * @docs docs/largest-rectangle.md
 */	
template< typename T >
int64_t largest_rectangle(vector< T > height)
{
  stack< int > st;
  height.push_back(0);
  vector< int > left(height.size());
  int64_t ret = 0;
  for(int i = 0; i < height.size(); i++) {
    while(!st.empty() && height[st.top()] >= height[i]) {
      ret = max(ret, (int64_t) (i - left[st.top()] - 1) * height[st.top()]);
      st.pop();
    }
    left[i] = st.empty() ? -1 : st.top();
    st.emplace(i);
  }
  return (ret);
}

```
{% endraw %}

<a href="../../index.html">Back to top page</a>

