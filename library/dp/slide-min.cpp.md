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


# :warning: dp/slide-min.cpp
* category: dp


[Back to top page](../../index.html)



## Code
```cpp
template< typename T >
vector< T > slide_min(const vector< T > &v, int k)
{
  deque< int > deq;
  vector< T > ret;
  for(int i = 0; i < v.size(); i++) {
    while(!deq.empty() && v[deq.back()] >= v[i]) {
      deq.pop_back();
    }
    deq.push_back(i);
    if(i - k + 1 >= 0) {
      ret.emplace_back(v[deq.front()]);
      if(deq.front() == i - k + 1) deq.pop_front();
    }
  }
  return ret;
}

```

[Back to top page](../../index.html)

