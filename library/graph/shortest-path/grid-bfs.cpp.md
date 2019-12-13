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


# :warning: graph/shortest-path/grid-bfs.cpp
<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#73feb47c464a017d041247d88424b879">graph/shortest-path</a>
* <a href="{{ site.github.repository_url }}/blob/master/graph/shortest-path/grid-bfs.cpp">View this file on GitHub</a>
    - Last commit date: 2019-11-30 23:02:43 +0900




## Code
{% raw %}
```cpp
vector< vector< int > > grid_bfs(vector< string > &s, char start, const string &wall = "#") {
  const int vx[] = {0, 1, 0, -1}, vy[] = {1, 0, -1, 0};
  vector< vector< int > > min_cost(s.size(), vector< int >(s[0].size(), -1));
  queue< pair< int, int > > que;
  for(int i = 0; i < s.size(); i++) {
    for(int j = 0; j < s[i].size(); j++) {
      if(s[i][j] == start) {
        que.emplace(i, j);
        min_cost[i][j] = 0;
      }
    }
  }
  while(!que.empty()) {
    auto p = que.front();
    que.pop();
    for(int i = 0; i < 4; i++) {
      int ny = p.first + vy[i], nx = p.second + vx[i];
      if(nx < 0 || ny < 0 || nx >= s[0].size() || ny >= s.size()) continue;
      if(min_cost[ny][nx] != -1) continue;
      if(wall.find(s[ny][nx]) != string::npos) continue;
      min_cost[ny][nx] = min_cost[p.first][p.second] + 1;
      que.emplace(ny, nx);
    }
  }
  return min_cost;
}

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

