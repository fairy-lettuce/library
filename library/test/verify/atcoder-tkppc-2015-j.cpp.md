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


# :warning: test/verify/atcoder-tkppc-2015-j.cpp
<a href="../../../index.html">Back to top page</a>

* category: test/verify
* <a href="{{ site.github.repository_url }}/blob/master/test/verify/atcoder-tkppc-2015-j.cpp">View this file on GitHub</a>
    - Last commit date: 2019-11-30 22:41:48 +0900




## Code
{% raw %}
```cpp
template< typename T, typename Compare = less< T > >
struct PQ {
  priority_queue< T, vector< T >, Compare > que1, que2;
 
  PQ() = default;
 
  void push(T k) {
    que1.emplace(k);
  }
 
  void pop(T k) {
    que2.emplace(k);
  }
 
  inline void modify() {
    while(que2.size() && que2.top() == que1.top()) {
      que2.pop();
      que1.pop();
    }
  }
 
  bool empty() {
    modify();
    return que1.empty();
  }
 
  T top() {
    modify();
    return que1.top();
  }
};
 
int main() {
 
  struct Farthest {
    PQ< int64 > pq;
    int64 c_max, p_max, length;
 
    Farthest() : c_max(-infll), p_max(-infll), length(0) {}
 
    void merge(int64 key, const Farthest &parent, const Farthest &child) {
      p_max = max(child.p_max, child.length + key + max(pq.empty() ? 0 : pq.top(), parent.p_max));
      c_max = max(parent.c_max, parent.length + key + max(pq.empty() ? 0 : pq.top(), child.c_max));
      length = parent.length + key + child.length;
    }
 
    void toggle() {
      swap(c_max, p_max);
    }
 
    void add(const Farthest &child) {
      pq.push(child.c_max);
    }
 
    void erase(const Farthest &child) {
      pq.pop(child.c_max);
    }
  } e;
 
  int Q;
  cin >> Q;
 
  using LCT = LinkCutTreeSubtree< Farthest, int64 >;
  LCT lct(e);
  vector< LCT::Node * > ev(500001), ee(500001);
  ev[0] = lct.make_node(0);
 
  int num = 1;
  for(int i = 0; i < Q; i++) {
    int t, a, b;
    cin >> t >> a >> b;
    if(t == 1) {
      ev[num] = lct.make_node(0);
      ee[num] = lct.make_node(b);
      lct.link(ee[num], ev[a]);
      lct.link(ev[num], ee[num]);
      ++num;
    } else if(t == 2) {
      lct.set_key(ee[a], b);
    } else {
      lct.evert(ev[a]);
      cout << ev[a]->sum.c_max << "\n";
    }
  }
}

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

