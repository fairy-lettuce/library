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


# :heavy_check_mark: Dinic-Capacity-Scaling(最大流) <small>(graph/flow/dinic-capacity-scaling.cpp)</small>

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#2af6c4bb6ad7cfa010303133dc15971f">graph/flow</a>
* <a href="{{ site.github.repository_url }}/blob/master/graph/flow/dinic-capacity-scaling.cpp">View this file on GitHub</a>
    - Last commit date: 2020-08-20 17:25:40+09:00




## 概要

最大流を求めるアルゴリズム.

すべての辺の容量が整数の場合, スケーリングを用いて Dinic の計算量を $O(EV \log U)$ に落とすことが出来る($U$ は辺の容量の最大値).

具体的には, フローを残余グラフ上で $k$ が大きい方から $2^k$ 単位で流すようにする.


## 使い方

* `DinicCapacityScaling(V)`: 頂点数 `V` で初期化する.
* `add_edge(from, to, cap, idx = -1)`: 頂点 `from` から `to` に容量 `cap` の辺を追加する.
* `max_flow(s, t)`: 頂点 `s` から `t` に最大流を流し, その流量を返す.

## 計算量

$O(EV \log U)$

$U$ は辺の容量の最大値


## Verified with

* :heavy_check_mark: <a href="../../../verify/test/verify/aoj-grl-6-a-4.test.cpp.html">test/verify/aoj-grl-6-a-4.test.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
/**
 * @brief Dinic-Capacity-Scaling(最大流)
 * @docs docs/dinic-capacity-scaling.md
 */
template< typename flow_t >
struct DinicCapacityScaling {
  static_assert(is_integral< flow_t >::value, "template parameter flow_t must be integral type");

  const flow_t INF;

  struct edge {
    int to;
    flow_t cap;
    int rev;
    bool isrev;
    int idx;
  };

  vector< vector< edge > > graph;
  vector< int > min_cost, iter;
  flow_t max_cap;

  explicit DinicCapacityScaling(int V) : INF(numeric_limits< flow_t >::max()), graph(V), max_cap(0) {}

  void add_edge(int from, int to, flow_t cap, int idx = -1) {
    max_cap = max(max_cap, cap);
    graph[from].emplace_back((edge) {to, cap, (int) graph[to].size(), false, idx});
    graph[to].emplace_back((edge) {from, 0, (int) graph[from].size() - 1, true, idx});
  }

  bool build_augment_path(int s, int t, const flow_t &base) {
    min_cost.assign(graph.size(), -1);
    queue< int > que;
    min_cost[s] = 0;
    que.push(s);
    while(!que.empty() && min_cost[t] == -1) {
      int p = que.front();
      que.pop();
      for(auto &e : graph[p]) {
        if(e.cap >= base && min_cost[e.to] == -1) {
          min_cost[e.to] = min_cost[p] + 1;
          que.push(e.to);
        }
      }
    }
    return min_cost[t] != -1;
  }

  flow_t find_augment_path(int idx, const int t, flow_t base, flow_t flow) {
    if(idx == t) return flow;
    flow_t sum = 0;
    for(int &i = iter[idx]; i < graph[idx].size(); i++) {
      edge &e = graph[idx][i];
      if(e.cap >= base && min_cost[idx] < min_cost[e.to]) {
        flow_t d = find_augment_path(e.to, t, base, min(flow - sum, e.cap));
        if(d > 0) {
          e.cap -= d;
          graph[e.to][e.rev].cap += d;
          sum += d;
          if(flow - sum < base) break;
        }
      }
    }
    return sum;
  }

  flow_t max_flow(int s, int t) {
    if(max_cap == flow_t(0)) return flow_t(0);
    flow_t flow = 0;
    for(int i = 63 - __builtin_clzll(max_cap); i >= 0; i--) {
      flow_t now = flow_t(1) << i;
      while(build_augment_path(s, t, now)) {
        iter.assign(graph.size(), 0);
        flow += find_augment_path(s, t, now, INF);
      }
    }
    return flow;
  }

  void output() {
    for(int i = 0; i < graph.size(); i++) {
      for(auto &e : graph[i]) {
        if(e.isrev) continue;
        auto &rev_e = graph[e.to][e.rev];
        cout << i << "->" << e.to << " (flow: " << rev_e.cap << "/" << e.cap + rev_e.cap << ")" << endl;
      }
    }
  }
};

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "graph/flow/dinic-capacity-scaling.cpp"
/**
 * @brief Dinic-Capacity-Scaling(最大流)
 * @docs docs/dinic-capacity-scaling.md
 */
template< typename flow_t >
struct DinicCapacityScaling {
  static_assert(is_integral< flow_t >::value, "template parameter flow_t must be integral type");

  const flow_t INF;

  struct edge {
    int to;
    flow_t cap;
    int rev;
    bool isrev;
    int idx;
  };

  vector< vector< edge > > graph;
  vector< int > min_cost, iter;
  flow_t max_cap;

  explicit DinicCapacityScaling(int V) : INF(numeric_limits< flow_t >::max()), graph(V), max_cap(0) {}

  void add_edge(int from, int to, flow_t cap, int idx = -1) {
    max_cap = max(max_cap, cap);
    graph[from].emplace_back((edge) {to, cap, (int) graph[to].size(), false, idx});
    graph[to].emplace_back((edge) {from, 0, (int) graph[from].size() - 1, true, idx});
  }

  bool build_augment_path(int s, int t, const flow_t &base) {
    min_cost.assign(graph.size(), -1);
    queue< int > que;
    min_cost[s] = 0;
    que.push(s);
    while(!que.empty() && min_cost[t] == -1) {
      int p = que.front();
      que.pop();
      for(auto &e : graph[p]) {
        if(e.cap >= base && min_cost[e.to] == -1) {
          min_cost[e.to] = min_cost[p] + 1;
          que.push(e.to);
        }
      }
    }
    return min_cost[t] != -1;
  }

  flow_t find_augment_path(int idx, const int t, flow_t base, flow_t flow) {
    if(idx == t) return flow;
    flow_t sum = 0;
    for(int &i = iter[idx]; i < graph[idx].size(); i++) {
      edge &e = graph[idx][i];
      if(e.cap >= base && min_cost[idx] < min_cost[e.to]) {
        flow_t d = find_augment_path(e.to, t, base, min(flow - sum, e.cap));
        if(d > 0) {
          e.cap -= d;
          graph[e.to][e.rev].cap += d;
          sum += d;
          if(flow - sum < base) break;
        }
      }
    }
    return sum;
  }

  flow_t max_flow(int s, int t) {
    if(max_cap == flow_t(0)) return flow_t(0);
    flow_t flow = 0;
    for(int i = 63 - __builtin_clzll(max_cap); i >= 0; i--) {
      flow_t now = flow_t(1) << i;
      while(build_augment_path(s, t, now)) {
        iter.assign(graph.size(), 0);
        flow += find_augment_path(s, t, now, INF);
      }
    }
    return flow;
  }

  void output() {
    for(int i = 0; i < graph.size(); i++) {
      for(auto &e : graph[i]) {
        if(e.isrev) continue;
        auto &rev_e = graph[e.to][e.rev];
        cout << i << "->" << e.to << " (flow: " << rev_e.cap << "/" << e.cap + rev_e.cap << ")" << endl;
      }
    }
  }
};

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

