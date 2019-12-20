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


# :heavy_check_mark: graph/flow/hopcroft-karp.cpp

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#2af6c4bb6ad7cfa010303133dc15971f">graph/flow</a>
* <a href="{{ site.github.repository_url }}/blob/master/graph/flow/hopcroft-karp.cpp">View this file on GitHub</a>
    - Last commit date: 2019-11-30 23:02:43+09:00




## Verified with

* :heavy_check_mark: <a href="../../../verify/test/verify/aoj-grl-7-a-2.test.cpp.html">test/verify/aoj-grl-7-a-2.test.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
struct HopcroftKarp {
  vector< vector< int > > graph;
  vector< int > dist, match;
  vector< bool > used, vv;

  HopcroftKarp(int n, int m) : graph(n), match(m, -1), used(n) {}

  void add_edge(int u, int v) {
    graph[u].push_back(v);
  }

  void bfs() {
    dist.assign(graph.size(), -1);
    queue< int > que;
    for(int i = 0; i < graph.size(); i++) {
      if(!used[i]) {
        que.emplace(i);
        dist[i] = 0;
      }
    }

    while(!que.empty()) {
      int a = que.front();
      que.pop();
      for(auto &b : graph[a]) {
        int c = match[b];
        if(c >= 0 && dist[c] == -1) {
          dist[c] = dist[a] + 1;
          que.emplace(c);
        }
      }
    }
  }

  bool dfs(int a) {
    vv[a] = true;
    for(auto &b : graph[a]) {
      int c = match[b];
      if(c < 0 || (!vv[c] && dist[c] == dist[a] + 1 && dfs(c))) {
        match[b] = a;
        used[a] = true;
        return (true);
      }
    }
    return (false);
  }

  int bipartite_matching() {
    int ret = 0;
    while(true) {
      bfs();
      vv.assign(graph.size(), false);
      int flow = 0;
      for(int i = 0; i < graph.size(); i++) {
        if(!used[i] && dfs(i)) ++flow;
      }
      if(flow == 0) return (ret);
      ret += flow;
    }
  }

  void output() {
    for(int i = 0; i < match.size(); i++) {
      if(~match[i]) {
        cout << match[i] << "-" << i << endl;
      }
    }
  }
};

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "graph/flow/hopcroft-karp.cpp"
struct HopcroftKarp {
  vector< vector< int > > graph;
  vector< int > dist, match;
  vector< bool > used, vv;

  HopcroftKarp(int n, int m) : graph(n), match(m, -1), used(n) {}

  void add_edge(int u, int v) {
    graph[u].push_back(v);
  }

  void bfs() {
    dist.assign(graph.size(), -1);
    queue< int > que;
    for(int i = 0; i < graph.size(); i++) {
      if(!used[i]) {
        que.emplace(i);
        dist[i] = 0;
      }
    }

    while(!que.empty()) {
      int a = que.front();
      que.pop();
      for(auto &b : graph[a]) {
        int c = match[b];
        if(c >= 0 && dist[c] == -1) {
          dist[c] = dist[a] + 1;
          que.emplace(c);
        }
      }
    }
  }

  bool dfs(int a) {
    vv[a] = true;
    for(auto &b : graph[a]) {
      int c = match[b];
      if(c < 0 || (!vv[c] && dist[c] == dist[a] + 1 && dfs(c))) {
        match[b] = a;
        used[a] = true;
        return (true);
      }
    }
    return (false);
  }

  int bipartite_matching() {
    int ret = 0;
    while(true) {
      bfs();
      vv.assign(graph.size(), false);
      int flow = 0;
      for(int i = 0; i < graph.size(); i++) {
        if(!used[i] && dfs(i)) ++flow;
      }
      if(flow == 0) return (ret);
      ret += flow;
    }
  }

  void output() {
    for(int i = 0; i < match.size(); i++) {
      if(~match[i]) {
        cout << match[i] << "-" << i << endl;
      }
    }
  }
};

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

