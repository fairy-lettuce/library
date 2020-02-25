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


# :heavy_check_mark: Enumerate-Clique(クリーク全列挙) <small>(graph/others/enumerate-clique.cpp)</small>

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#e557c7f962c39680942b9dada22cabec">graph/others</a>
* <a href="{{ site.github.repository_url }}/blob/master/graph/others/enumerate-clique.cpp">View this file on GitHub</a>
    - Last commit date: 2020-02-25 22:57:51+09:00


* see: <a href="https://www.slideshare.net/wata_orz/ss-12131479">https://www.slideshare.net/wata_orz/ss-12131479</a>


## Verified with

* :heavy_check_mark: <a href="../../../verify/test/verify/aoj-2306.test.cpp.html">test/verify/aoj-2306.test.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
/**
 * @brief Enumerate-Clique(クリーク全列挙)
 * @see https://www.slideshare.net/wata_orz/ss-12131479
 */
vector< vector< int > > enumerate_clique(Matrix< bool > g) {

  int N = (int) g.size(), M = 0;
  vector< int > deg(N);
  vector< vector< int > > edge(N, vector< int >(N));
  for(int i = 0; i < N; i++) {
    for(auto p : g[i]) deg[i] += p;
    M += deg[i];
  }
  int lim = (int) sqrt(M);

  vector< vector< int > > cliques;

  auto add_clique = [&](const vector< int > &rem, bool last) {
    vector< int > neighbor((int) rem.size() - last);
    for(int i = 0; i < (int) neighbor.size(); i++) {
      for(int j = 0; j < (int) neighbor.size(); j++) {
        if(i != j && !g[rem[i]][rem[j]]) neighbor[i] |= 1 << j;
      }
    }
    for(int i = 1 - last; i < (1 << neighbor.size()); i++) {
      bool ok = true;
      for(int j = 0; j < neighbor.size(); j++) {
        if((i >> j) & 1) {
          if(i & neighbor[j]) {
            ok = false;
            break;
          }
        }
      }
      if(ok) {
        vector< int > clique;
        if(last) clique.emplace_back(rem.back());
        for(int j = 0; j < neighbor.size(); j++) {
          if((i >> j) & 1) clique.emplace_back(rem[j]);
        }
        cliques.emplace_back(clique);
      }
    }
  };

  vector< int > used(N);
  queue< int > que;
  for(int i = 0; i < N; i++) {
    if(deg[i] < lim) {
      used[i] = true;
      que.emplace(i);
    }
  }
  while(!que.empty()) {
    int idx = que.front();
    que.pop();
    vector< int > rem;
    for(int k = 0; k < N; k++) {
      if(g[idx][k]) rem.emplace_back(k);
    }
    rem.emplace_back(idx);
    add_clique(rem, true);
    used[idx] = true;
    for(int k = 0; k < N; k++) {
      if(g[idx][k]) {
        g[idx][k] = false;
        g[k][idx] = false;
        --deg[k];
        if(!used[k] && deg[k] < lim) {
          used[k] = true;
          que.emplace(k);
        }
      }
    }
  }
  vector< int > rem;
  for(int i = 0; i < N; i++) {
    if(!used[i]) rem.emplace_back(i);
  }
  add_clique(rem, false);
  return cliques;
}

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "graph/others/enumerate-clique.cpp"
/**
 * @brief Enumerate-Clique(クリーク全列挙)
 * @see https://www.slideshare.net/wata_orz/ss-12131479
 */
vector< vector< int > > enumerate_clique(Matrix< bool > g) {

  int N = (int) g.size(), M = 0;
  vector< int > deg(N);
  vector< vector< int > > edge(N, vector< int >(N));
  for(int i = 0; i < N; i++) {
    for(auto p : g[i]) deg[i] += p;
    M += deg[i];
  }
  int lim = (int) sqrt(M);

  vector< vector< int > > cliques;

  auto add_clique = [&](const vector< int > &rem, bool last) {
    vector< int > neighbor((int) rem.size() - last);
    for(int i = 0; i < (int) neighbor.size(); i++) {
      for(int j = 0; j < (int) neighbor.size(); j++) {
        if(i != j && !g[rem[i]][rem[j]]) neighbor[i] |= 1 << j;
      }
    }
    for(int i = 1 - last; i < (1 << neighbor.size()); i++) {
      bool ok = true;
      for(int j = 0; j < neighbor.size(); j++) {
        if((i >> j) & 1) {
          if(i & neighbor[j]) {
            ok = false;
            break;
          }
        }
      }
      if(ok) {
        vector< int > clique;
        if(last) clique.emplace_back(rem.back());
        for(int j = 0; j < neighbor.size(); j++) {
          if((i >> j) & 1) clique.emplace_back(rem[j]);
        }
        cliques.emplace_back(clique);
      }
    }
  };

  vector< int > used(N);
  queue< int > que;
  for(int i = 0; i < N; i++) {
    if(deg[i] < lim) {
      used[i] = true;
      que.emplace(i);
    }
  }
  while(!que.empty()) {
    int idx = que.front();
    que.pop();
    vector< int > rem;
    for(int k = 0; k < N; k++) {
      if(g[idx][k]) rem.emplace_back(k);
    }
    rem.emplace_back(idx);
    add_clique(rem, true);
    used[idx] = true;
    for(int k = 0; k < N; k++) {
      if(g[idx][k]) {
        g[idx][k] = false;
        g[k][idx] = false;
        --deg[k];
        if(!used[k] && deg[k] < lim) {
          used[k] = true;
          que.emplace(k);
        }
      }
    }
  }
  vector< int > rem;
  for(int i = 0; i < N; i++) {
    if(!used[i]) rem.emplace_back(i);
  }
  add_clique(rem, false);
  return cliques;
}

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

