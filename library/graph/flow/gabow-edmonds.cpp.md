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


# :warning: graph/flow/gabow-edmonds.cpp
<a href="../../../index.html">Back to top page</a>

* category: graph/flow
* <a href="{{ site.github.repository_url }}/blob/master/graph/flow/gabow-edmonds.cpp">View this file on GitHub</a>
    - Last commit date: 2019-11-30 23:02:43 +0900




## Code
{% raw %}
```cpp
// https://qiita.com/Kutimoti_T/items/5b579773e0a24d650bdf
struct GabowEdmonds {

  struct edge {
    int to, idx;
  };

  vector< vector< edge > > g;
  vector< pair< int, int > > edges;
  vector< int > mate, label, first;
  queue< int > que;

  GabowEdmonds(int n) : g(n + 1), mate(n + 1), label(n + 1, -1), first(n + 1) {}

  void add_edge(int u, int v) {
    ++u, ++v;
    g[u].push_back((edge) {v, (int) (edges.size() + g.size())});
    g[v].push_back((edge) {u, (int) (edges.size() + g.size())});
    edges.emplace_back(u, v);
  }

  int find(int x) {
    if(label[first[x]] < 0) return first[x];
    first[x] = find(first[x]);
    return first[x];
  }

  void rematch(int v, int w) {
    int t = mate[v];
    mate[v] = w;
    if(mate[t] != v) return;
    if(label[v] < g.size()) {
      mate[t] = label[v];
      rematch(label[v], t);
    } else {
      int x = edges[label[v] - g.size()].first;
      int y = edges[label[v] - g.size()].second;
      rematch(x, y);
      rematch(y, x);
    }
  }

  void assign_label(int x, int y, int num) {
    int r = find(x);
    int s = find(y);
    int join = 0;
    if(r == s) return;
    label[r] = -num;
    label[s] = -num;
    while(true) {
      if(s != 0) swap(r, s);
      r = find(label[mate[r]]);
      if(label[r] == -num) {
        join = r;
        break;
      }
      label[r] = -num;
    }
    int v = first[x];
    while(v != join) {
      que.push(v);
      label[v] = num;
      first[v] = join;
      v = first[label[mate[v]]];
    }
    v = first[y];
    while(v != join) {
      que.push(v);
      label[v] = num;
      first[v] = join;
      v = first[label[mate[v]]];
    }
  }

  bool augment_check(int u) {
    que = queue< int >();
    first[u] = 0;
    label[u] = 0;
    que.push(u);
    while(!que.empty()) {
      int x = que.front();
      que.pop();
      for(auto e : g[x]) {
        int y = e.to;
        if(mate[y] == 0 && y != u) {
          mate[y] = x;
          rematch(x, y);
          return true;
        } else if(label[y] >= 0) {
          assign_label(x, y, e.idx);
        } else if(label[mate[y]] < 0) {
          label[mate[y]] = x;
          first[mate[y]] = y;
          que.push(mate[y]);
        }
      }
    }
    return false;
  }

  vector< pair< int, int > > max_matching() {
    for(int i = 1; i < g.size(); i++) {
      if(mate[i] != 0) continue;
      if(augment_check(i)) label.assign(g.size(), -1);
    }
    vector< pair< int, int > > ret;
    for(int i = 1; i < g.size(); i++) {
      if(i < mate[i]) ret.emplace_back(i - 1, mate[i] - 1);
    }
    return ret;
  }
};

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

