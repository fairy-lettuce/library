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


# :x: structure/others/sliding-window-aggregation.cpp

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#40d73e22b7d986e3399449c25c8b23a1">structure/others</a>
* <a href="{{ site.github.repository_url }}/blob/master/structure/others/sliding-window-aggregation.cpp">View this file on GitHub</a>
    - Last commit date: 2019-11-30 22:41:48+09:00




## Verified with

* :x: <a href="../../../verify/test/verify/yosupo-queue-operate-all-composite.test.cpp.html">test/verify/yosupo-queue-operate-all-composite.test.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
template< typename SemiGroup >
struct SlidingWindowAggregation {
  using F = function< SemiGroup(SemiGroup, SemiGroup) >;
 
  struct Node {
    SemiGroup val, sum;
 
    Node(const SemiGroup &val, const SemiGroup &sum) : val(val), sum(sum) {}
  };
 
  SlidingWindowAggregation(F f) : f(f) {}
 
 
  const F f;
  stack< Node > front, back;
 
  bool empty() const {
    return front.empty() && back.empty();
  }
 
  size_t size() const {
    return front.size() + back.size();
  }
 
  SemiGroup fold_all() const {
    if(front.empty()) {
      return back.top().sum;
    } else if(back.empty()) {
      return front.top().sum;
    } else {
      return f(front.top().sum, back.top().sum);
    }
  }
 
  void push(const SemiGroup &x) {
    if(back.empty()) {
      back.emplace(x, x);
    } else {
      back.emplace(x, f(back.top().sum, x));
    }
  }
 
  void pop() {
    if(front.empty()) {
      front.emplace(back.top().val, back.top().val);
      back.pop();
      while(!back.empty()) {
        front.emplace(back.top().val, f(back.top().val, front.top().sum));
        back.pop();
      }
    }
    front.pop();
  }
};

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "structure/others/sliding-window-aggregation.cpp"
template< typename SemiGroup >
struct SlidingWindowAggregation {
  using F = function< SemiGroup(SemiGroup, SemiGroup) >;
 
  struct Node {
    SemiGroup val, sum;
 
    Node(const SemiGroup &val, const SemiGroup &sum) : val(val), sum(sum) {}
  };
 
  SlidingWindowAggregation(F f) : f(f) {}
 
 
  const F f;
  stack< Node > front, back;
 
  bool empty() const {
    return front.empty() && back.empty();
  }
 
  size_t size() const {
    return front.size() + back.size();
  }
 
  SemiGroup fold_all() const {
    if(front.empty()) {
      return back.top().sum;
    } else if(back.empty()) {
      return front.top().sum;
    } else {
      return f(front.top().sum, back.top().sum);
    }
  }
 
  void push(const SemiGroup &x) {
    if(back.empty()) {
      back.emplace(x, x);
    } else {
      back.emplace(x, f(back.top().sum, x));
    }
  }
 
  void pop() {
    if(front.empty()) {
      front.emplace(back.top().val, back.top().val);
      back.pop();
      while(!back.empty()) {
        front.emplace(back.top().val, f(back.top().val, front.top().sum));
        back.pop();
      }
    }
    front.pop();
  }
};

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

