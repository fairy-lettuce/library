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


# :heavy_check_mark: K-Shortest-Walk <small>(graph/shortest-path/k-shortest-walk.cpp)</small>

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#73feb47c464a017d041247d88424b879">graph/shortest-path</a>
* <a href="{{ site.github.repository_url }}/blob/master/graph/shortest-path/k-shortest-walk.cpp">View this file on GitHub</a>
    - Last commit date: 2020-08-21 01:30:35+09:00


* see: <a href="https://qiita.com/hotman78/items/42534a01c4bd05ed5e1e">https://qiita.com/hotman78/items/42534a01c4bd05ed5e1e</a>


## 概要

頂点 $s$ から $t$ へのウォーク(Walk) のうち, 昇順 $k$ 個のウォークの長さを Eppstein's Algorithm により求める. 

ウォーク(Walk, 歩道, 経路) とは重複して頂点や辺が現れることを許容した頂点 $s$ から $t$ への経路を指す.

ちなみにトレイル(Trail) は同じ辺を通らない経路, 道(Path) は同じ頂点を通らない経路である.

* `k_shotest_walk(g, s, t, k)`: 重み付き有向グラフ `g` の頂点 `s` から `t` へのウォークのうち, 昇順 `k` 個のウォークの長さを返す(ウォークの個数が `k` 個に満たないとき全てを返す).

## 計算量

* $O((V + E) \log V + K \log K)$


## Verified with

* :heavy_check_mark: <a href="../../../verify/test/verify/yosupo-k-shortest-walk.test.cpp.html">test/verify/yosupo-k-shortest-walk.test.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
/**
 * @brief K-Shortest-Walk
 * @docs docs/k-shortest-walk.md
 * @see https://qiita.com/hotman78/items/42534a01c4bd05ed5e1e
 */
template< typename T >
vector< T > k_shortest_walk(const Graph< T > &g, int s, int t, int k) {
  int N = (int) g.size();
  Graph< T > rg(N);
  for(int i = 0; i < N; i++) {
    for(auto &e : g.g[i]) rg.add_directed_edge(e.to, i, e.cost);
  }
  auto dist = dijkstra(rg, t);
  if(dist.from[s] == -1) return {};
  auto &p = dist.dist;
  vector< vector< int > > ch(N);
  for(int i = 0; i < N; i++) {
    if(dist.from[i] >= 0) ch[dist.from[i]].emplace_back(i);
  }
  using PHeap = PersistentLeftistHeap< T >;
  using Node = typename PHeap::Node;
  PHeap heap;
  vector< Node * > h(N, heap.make_root());
  {
    queue< int > que;
    que.emplace(t);
    while(!que.empty()) {
      int idx = que.front();
      que.pop();
      if(dist.from[idx] >= 0) {
        h[idx] = heap.meld(h[idx], h[dist.from[idx]]);
      }
      bool used = true;
      for(auto &e : g.g[idx]) {
        if(e.to != t && dist.from[e.to] == -1) continue;
        if(used && dist.from[idx] == e.to && p[e.to] + e.cost == p[idx]) {
          used = false;
          continue;
        }
        h[idx] = heap.push(h[idx], e.cost - p[idx] + p[e.to], e.to);
      }
      for(auto &to : ch[idx]) que.emplace(to);
    }
  }
  using pi = pair< T, Node * >;
  auto comp = [](const pi &x, const pi &y) { return x.first > y.first; };
  priority_queue< pi, vector< pi >, decltype(comp) > que(comp);
  Node *root = heap.make_root();
  root = heap.push(root, p[s], s);
  que.emplace(p[s], root);
  vector< T > ans;
  while(!que.empty()) {
    T cost;
    Node *cur;
    tie(cost, cur) = que.top();
    que.pop();
    ans.emplace_back(cost);
    if(ans.size() == k) break;
    if(cur->l) que.emplace(cost + cur->l->key - cur->key, cur->l);
    if(cur->r) que.emplace(cost + cur->r->key - cur->key, cur->r);
    if(h[cur->idx]) que.emplace(cost + h[cur->idx]->key, h[cur->idx]);
  }
  return ans;
}

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "graph/shortest-path/k-shortest-walk.cpp"
/**
 * @brief K-Shortest-Walk
 * @docs docs/k-shortest-walk.md
 * @see https://qiita.com/hotman78/items/42534a01c4bd05ed5e1e
 */
template< typename T >
vector< T > k_shortest_walk(const Graph< T > &g, int s, int t, int k) {
  int N = (int) g.size();
  Graph< T > rg(N);
  for(int i = 0; i < N; i++) {
    for(auto &e : g.g[i]) rg.add_directed_edge(e.to, i, e.cost);
  }
  auto dist = dijkstra(rg, t);
  if(dist.from[s] == -1) return {};
  auto &p = dist.dist;
  vector< vector< int > > ch(N);
  for(int i = 0; i < N; i++) {
    if(dist.from[i] >= 0) ch[dist.from[i]].emplace_back(i);
  }
  using PHeap = PersistentLeftistHeap< T >;
  using Node = typename PHeap::Node;
  PHeap heap;
  vector< Node * > h(N, heap.make_root());
  {
    queue< int > que;
    que.emplace(t);
    while(!que.empty()) {
      int idx = que.front();
      que.pop();
      if(dist.from[idx] >= 0) {
        h[idx] = heap.meld(h[idx], h[dist.from[idx]]);
      }
      bool used = true;
      for(auto &e : g.g[idx]) {
        if(e.to != t && dist.from[e.to] == -1) continue;
        if(used && dist.from[idx] == e.to && p[e.to] + e.cost == p[idx]) {
          used = false;
          continue;
        }
        h[idx] = heap.push(h[idx], e.cost - p[idx] + p[e.to], e.to);
      }
      for(auto &to : ch[idx]) que.emplace(to);
    }
  }
  using pi = pair< T, Node * >;
  auto comp = [](const pi &x, const pi &y) { return x.first > y.first; };
  priority_queue< pi, vector< pi >, decltype(comp) > que(comp);
  Node *root = heap.make_root();
  root = heap.push(root, p[s], s);
  que.emplace(p[s], root);
  vector< T > ans;
  while(!que.empty()) {
    T cost;
    Node *cur;
    tie(cost, cur) = que.top();
    que.pop();
    ans.emplace_back(cost);
    if(ans.size() == k) break;
    if(cur->l) que.emplace(cost + cur->l->key - cur->key, cur->l);
    if(cur->r) que.emplace(cost + cur->r->key - cur->key, cur->r);
    if(h[cur->idx]) que.emplace(cost + h[cur->idx]->key, h[cur->idx]);
  }
  return ans;
}

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

