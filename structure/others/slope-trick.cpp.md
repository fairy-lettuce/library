---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith: []
  _isVerificationFailed: false
  _pathExtension: cpp
  _verificationStatusIcon: ':warning:'
  attributes:
    document_title: Slope-Trick
    links:
    - https://maspypy.com/slope-trick-1-%E8%A7%A3%E8%AA%AC%E7%B7%A8
  bundledCode: "#line 1 \"structure/others/slope-trick.cpp\"\n/**\n * @brief Slope-Trick\n\
    \ * @see https://maspypy.com/slope-trick-1-%E8%A7%A3%E8%AA%AC%E7%B7%A8\n */\n\
    template< typename T >\nstruct LazySplayTree {\npublic:\n\n  struct Node {\n \
    \   Node *l, *r, *p;\n    T key, sum;\n    size_t sz;\n    T add;\n\n    bool\
    \ is_root() const {\n      return !p || (p->l != this && p->r != this);\n    }\n\
    \n    Node(const T &key, const T &add) :\n        key(key), sum(key), sz(1), add(add),\
    \ l(nullptr), r(nullptr), p(nullptr) {}\n  };\n\n  LazySplayTree() = default;\n\
    \n  inline size_t count(const Node *t) { return t ? t->sz : 0; }\n\n  Node *alloc(const\
    \ T &key, const T &add = T()) {\n    return new Node(key, add);\n  }\n\n  void\
    \ splay(Node *t) {\n    push(t);\n    while(!t->is_root()) {\n      auto *q =\
    \ t->p;\n      if(q->is_root()) {\n        push(q), push(t);\n        if(q->l\
    \ == t) rotr(t);\n        else rotl(t);\n      } else {\n        auto *r = q->p;\n\
    \        push(r), push(q), push(t);\n        if(r->l == q) {\n          if(q->l\
    \ == t) rotr(q), rotr(t);\n          else rotl(t), rotr(t);\n        } else {\n\
    \          if(q->r == t) rotl(q), rotl(t);\n          else rotr(t), rotl(t);\n\
    \        }\n      }\n    }\n  }\n\n  Node *erase(Node *t) {\n    splay(t);\n \
    \   Node *x = t->l, *y = t->r;\n    delete t;\n    if(!x) {\n      t = y;\n  \
    \    if(t) t->p = nullptr;\n    } else if(!y) {\n      t = x;\n      t->p = nullptr;\n\
    \    } else {\n      x->p = nullptr;\n      t = get_right(x);\n      splay(t);\n\
    \      t->r = y;\n      y->p = t;\n    }\n    return t;\n  }\n\n  Node *get_left(Node\
    \ *t) const {\n    while(t->l) t = t->l;\n    return t;\n  }\n\n  Node *get_right(Node\
    \ *t) const {\n    while(t->r) t = t->r;\n    return t;\n  }\n\n  void set_propagate(Node\
    \ *t, const T &add) {\n    splay(t);\n    propagate(t, add);\n    push(t);\n \
    \ }\n\n  pair< Node *, Node * > split(Node *t, int k) {\n    if(!t) return {nullptr,\
    \ nullptr};\n    push(t);\n    if(k <= count(t->l)) {\n      auto x = split(t->l,\
    \ k);\n      t->l = x.second;\n      t->p = nullptr;\n      if(x.second) x.second->p\
    \ = t;\n      return {x.first, update(t)};\n    } else {\n      auto x = split(t->r,\
    \ k - count(t->l) - 1);\n      t->r = x.first;\n      t->p = nullptr;\n      if(x.first)\
    \ x.first->p = t;\n      return {update(t), x.second};\n    }\n  }\n\n  tuple<\
    \ Node *, Node *, Node * > split3(Node *t, int a, int b) {\n    splay(t);\n  \
    \  auto x = split(t, a);\n    auto y = split(x.second, b - a);\n    return make_tuple(x.first,\
    \ y.first, y.second);\n  }\n\n  pair< Node *, Node * > split_lower_bound(Node\
    \ *t, const T &key) {\n    if(!t) return {nullptr, nullptr};\n    push(t);\n \
    \   if(key <= t->key) {\n      auto x = split_lower_bound(t->l, key);\n      t->l\
    \ = x.second;\n      t->p = nullptr;\n      if(x.second) x.second->p = t;\n  \
    \    return {x.first, update(t)};\n    } else {\n      auto x = split_lower_bound(t->r,\
    \ key);\n      t->r = x.first;\n      t->p = nullptr;\n      if(x.first) x.first->p\
    \ = t;\n      return {update(t), x.second};\n    }\n  }\n\n  Node *merge_wuh(Node\
    \ *t1, Node *t2) {\n    if(!t1 and !t2) return nullptr;\n    if(!t1) return splay(t2),\
    \ t2;\n    if(!t2) return splay(t1), t1;\n    splay(t1), splay(t2);\n    if(count(t1)\
    \ < count(t2)) swap(t1, t2);\n    auto[t2l, v, t2r] = split3(t2, count(t2) / 2,\
    \ count(t2) / 2 + 1);\n    auto[t1l, t1r] = split_lower_bound(t1, v->key);\n \
    \   return merge(merge_wuh(t1l, t2l), v, merge_wuh(t1r, t2r));\n  }\n\n  template<\
    \ typename ... Args >\n  Node *merge(Node *l, Args ...rest) {\n    Node *r = merge(rest...);\n\
    \    if(!l && !r) return nullptr;\n    if(!l) return splay(r), r;\n    if(!r)\
    \ return splay(l), l;\n    splay(l), splay(r);\n    l = get_right(l);\n    splay(l);\n\
    \    l->r = r;\n    r->p = l;\n    update(l);\n    return l;\n  }\n\n  Node *insert_lower_bound(Node\
    \ *t, const T &v) {\n    if(t) {\n      splay(t);\n      auto x = split_lower_bound(t,\
    \ v);\n      return merge(merge(x.first, alloc(v)), x.second);\n    } else {\n\
    \      return alloc(v);\n    }\n  }\n\n  Node *update(Node *t) {\n    t->sz =\
    \ 1;\n    t->sum = t->key;\n    if(t->l) t->sz += t->l->sz, t->sum += t->l->sum;\n\
    \    if(t->r) t->sz += t->r->sz, t->sum += t->r->sum;\n    return t;\n  }\n\n\
    \  void propagate(Node *t, const T &x) {\n    t->add += x;\n    t->sum += count(t)\
    \ * x;\n    t->key += x;\n  }\n\n  void push(Node *t) {\n    if(t->add) {\n  \
    \    if(t->l) propagate(t->l, t->add);\n      if(t->r) propagate(t->r, t->add);\n\
    \      t->add = 0;\n    }\n  }\n\nprivate:\n  void rotr(Node *t) {\n    auto *x\
    \ = t->p, *y = x->p;\n    if((x->l = t->r)) t->r->p = x;\n    t->r = x, x->p =\
    \ t;\n    update(x), update(t);\n    if((t->p = y)) {\n      if(y->l == x) y->l\
    \ = t;\n      if(y->r == x) y->r = t;\n      update(y);\n    }\n  }\n\n  void\
    \ rotl(Node *t) {\n    auto *x = t->p, *y = x->p;\n    if((x->r = t->l)) t->l->p\
    \ = x;\n    t->l = x, x->p = t;\n    update(x), update(t);\n    if((t->p = y))\
    \ {\n      if(y->l == x) y->l = t;\n      if(y->r == x) y->r = t;\n      update(y);\n\
    \    }\n  }\n\n  Node *merge(Node *l) {\n    return l;\n  }\n};\n\ntemplate< typename\
    \ T >\nstruct SlopeTrick {\n\n  const T INF = numeric_limits< T >::max() / 3;\n\
    \n  T min_f;\n  LazySplayTree< T > st;\n  typename LazySplayTree< T >::Node *L,\
    \ *R;\nprivate:\n  void push_R(const T &a) {\n    R = st.insert_lower_bound(R,\
    \ a);\n  }\n\n  T top_R() {\n    if(R) {\n      st.splay(R = st.get_left(R));\n\
    \      return R->key;\n    } else {\n      return INF;\n    }\n  }\n\n  T pop_R()\
    \ {\n    T val = top_R();\n    if(R) R = st.erase(R);\n    return val;\n  }\n\n\
    \  void push_L(const T &a) {\n    L = st.insert_lower_bound(L, a);\n  }\n\n  T\
    \ top_L() {\n    if(L) {\n      st.splay(L = st.get_right(L));\n      return L->key;\n\
    \    } else {\n      return -INF;\n    }\n\n  }\n\n  T pop_L() {\n    T val =\
    \ top_L();\n    if(L) L = st.erase(L);\n    return val;\n  }\n\n  size_t size()\
    \ {\n    return st.count(L) + st.count(R);\n  }\n\npublic:\n  SlopeTrick() : min_f(0),\
    \ L(nullptr), R(nullptr) {}\n\n  struct Query {\n    T lx, rx, min_f;\n  };\n\n\
    \  // return min f(x)\n  Query query() {\n    return (Query) {top_L(), top_R(),\
    \ min_f};\n  }\n\n  // f(x) += a\n  void add_all(const T &a) {\n    min_f += a;\n\
    \  }\n\n  // add \\_\n  // f(x) += max(a - x, 0)\n  void add_a_minus_x(const T\
    \ &a) {\n    min_f += max(T(0), a - top_R());\n    push_R(a);\n    push_L(pop_R());\n\
    \  }\n\n  // add _/\n  // f(x) += max(x - a, 0)\n  void add_x_minus_a(const T\
    \ &a) {\n    min_f += max(T(0), top_L() - a);\n    push_L(a);\n    push_R(pop_L());\n\
    \  }\n\n  // add \\/\n  // f(x) += abs(x - a)\n  void add_abs(const T &a) {\n\
    \    add_a_minus_x(a);\n    add_x_minus_a(a);\n  }\n\n  // \\/ -> \\_\n  // f_{new}\
    \ (x) = min f(y) (y <= x)\n  void clear_right() {\n    R = nullptr;\n  }\n\n \
    \ // \\/ -> _/\n  // f_{new} (x) = min f(y) (y >= x)\n  void clear_left() {\n\
    \    L = nullptr;\n  }\n\n  // \\/ -> \\_/\n  // f_{new} (x) = min f(y) (x-b <=\
    \ y <= x-a)\n  void shift(const T &a, const T &b) {\n    assert(a <= b);\n   \
    \ if(L) st.set_propagate(L, a);\n    if(R) st.set_propagate(R, b);\n  }\n\n  //\
    \ \\/. -> .\\/\n  // f_{new} (x) = f(x - a)\n  void shift(const T &a) {\n    shift(a,\
    \ a);\n  }\n\n  // return f(x) L, R \u3092\u7834\u58CA\u3059\u308B\n  T get(const\
    \ T &x) {\n    T ret = min_f;\n    {\n      auto[l, r] = st.split_lower_bound(L,\
    \ x);\n      if(r) {\n        ret += r->sum;\n        ret -= x * (T) st.count(r);\n\
    \      }\n      L = st.merge(l, r);\n    }\n    {\n      auto[l, r] = st.split_lower_bound(R,\
    \ x);\n      if(l) {\n        ret += x * (T) st.count(r);\n        ret -= l->sum;\n\
    \      }\n      R = st.merge(l, r);\n    }\n    return ret;\n  }\n\n  // f(x)\
    \ += g(x)\n  void merge(SlopeTrick &g) {\n    L = st.merge_wuh(L, g.L);\n    R\
    \ = st.merge_wuh(R, g.R);\n    min_f += g.min_f;\n  }\n};\n"
  code: "/**\n * @brief Slope-Trick\n * @see https://maspypy.com/slope-trick-1-%E8%A7%A3%E8%AA%AC%E7%B7%A8\n\
    \ */\ntemplate< typename T >\nstruct LazySplayTree {\npublic:\n\n  struct Node\
    \ {\n    Node *l, *r, *p;\n    T key, sum;\n    size_t sz;\n    T add;\n\n   \
    \ bool is_root() const {\n      return !p || (p->l != this && p->r != this);\n\
    \    }\n\n    Node(const T &key, const T &add) :\n        key(key), sum(key),\
    \ sz(1), add(add), l(nullptr), r(nullptr), p(nullptr) {}\n  };\n\n  LazySplayTree()\
    \ = default;\n\n  inline size_t count(const Node *t) { return t ? t->sz : 0; }\n\
    \n  Node *alloc(const T &key, const T &add = T()) {\n    return new Node(key,\
    \ add);\n  }\n\n  void splay(Node *t) {\n    push(t);\n    while(!t->is_root())\
    \ {\n      auto *q = t->p;\n      if(q->is_root()) {\n        push(q), push(t);\n\
    \        if(q->l == t) rotr(t);\n        else rotl(t);\n      } else {\n     \
    \   auto *r = q->p;\n        push(r), push(q), push(t);\n        if(r->l == q)\
    \ {\n          if(q->l == t) rotr(q), rotr(t);\n          else rotl(t), rotr(t);\n\
    \        } else {\n          if(q->r == t) rotl(q), rotl(t);\n          else rotr(t),\
    \ rotl(t);\n        }\n      }\n    }\n  }\n\n  Node *erase(Node *t) {\n    splay(t);\n\
    \    Node *x = t->l, *y = t->r;\n    delete t;\n    if(!x) {\n      t = y;\n \
    \     if(t) t->p = nullptr;\n    } else if(!y) {\n      t = x;\n      t->p = nullptr;\n\
    \    } else {\n      x->p = nullptr;\n      t = get_right(x);\n      splay(t);\n\
    \      t->r = y;\n      y->p = t;\n    }\n    return t;\n  }\n\n  Node *get_left(Node\
    \ *t) const {\n    while(t->l) t = t->l;\n    return t;\n  }\n\n  Node *get_right(Node\
    \ *t) const {\n    while(t->r) t = t->r;\n    return t;\n  }\n\n  void set_propagate(Node\
    \ *t, const T &add) {\n    splay(t);\n    propagate(t, add);\n    push(t);\n \
    \ }\n\n  pair< Node *, Node * > split(Node *t, int k) {\n    if(!t) return {nullptr,\
    \ nullptr};\n    push(t);\n    if(k <= count(t->l)) {\n      auto x = split(t->l,\
    \ k);\n      t->l = x.second;\n      t->p = nullptr;\n      if(x.second) x.second->p\
    \ = t;\n      return {x.first, update(t)};\n    } else {\n      auto x = split(t->r,\
    \ k - count(t->l) - 1);\n      t->r = x.first;\n      t->p = nullptr;\n      if(x.first)\
    \ x.first->p = t;\n      return {update(t), x.second};\n    }\n  }\n\n  tuple<\
    \ Node *, Node *, Node * > split3(Node *t, int a, int b) {\n    splay(t);\n  \
    \  auto x = split(t, a);\n    auto y = split(x.second, b - a);\n    return make_tuple(x.first,\
    \ y.first, y.second);\n  }\n\n  pair< Node *, Node * > split_lower_bound(Node\
    \ *t, const T &key) {\n    if(!t) return {nullptr, nullptr};\n    push(t);\n \
    \   if(key <= t->key) {\n      auto x = split_lower_bound(t->l, key);\n      t->l\
    \ = x.second;\n      t->p = nullptr;\n      if(x.second) x.second->p = t;\n  \
    \    return {x.first, update(t)};\n    } else {\n      auto x = split_lower_bound(t->r,\
    \ key);\n      t->r = x.first;\n      t->p = nullptr;\n      if(x.first) x.first->p\
    \ = t;\n      return {update(t), x.second};\n    }\n  }\n\n  Node *merge_wuh(Node\
    \ *t1, Node *t2) {\n    if(!t1 and !t2) return nullptr;\n    if(!t1) return splay(t2),\
    \ t2;\n    if(!t2) return splay(t1), t1;\n    splay(t1), splay(t2);\n    if(count(t1)\
    \ < count(t2)) swap(t1, t2);\n    auto[t2l, v, t2r] = split3(t2, count(t2) / 2,\
    \ count(t2) / 2 + 1);\n    auto[t1l, t1r] = split_lower_bound(t1, v->key);\n \
    \   return merge(merge_wuh(t1l, t2l), v, merge_wuh(t1r, t2r));\n  }\n\n  template<\
    \ typename ... Args >\n  Node *merge(Node *l, Args ...rest) {\n    Node *r = merge(rest...);\n\
    \    if(!l && !r) return nullptr;\n    if(!l) return splay(r), r;\n    if(!r)\
    \ return splay(l), l;\n    splay(l), splay(r);\n    l = get_right(l);\n    splay(l);\n\
    \    l->r = r;\n    r->p = l;\n    update(l);\n    return l;\n  }\n\n  Node *insert_lower_bound(Node\
    \ *t, const T &v) {\n    if(t) {\n      splay(t);\n      auto x = split_lower_bound(t,\
    \ v);\n      return merge(merge(x.first, alloc(v)), x.second);\n    } else {\n\
    \      return alloc(v);\n    }\n  }\n\n  Node *update(Node *t) {\n    t->sz =\
    \ 1;\n    t->sum = t->key;\n    if(t->l) t->sz += t->l->sz, t->sum += t->l->sum;\n\
    \    if(t->r) t->sz += t->r->sz, t->sum += t->r->sum;\n    return t;\n  }\n\n\
    \  void propagate(Node *t, const T &x) {\n    t->add += x;\n    t->sum += count(t)\
    \ * x;\n    t->key += x;\n  }\n\n  void push(Node *t) {\n    if(t->add) {\n  \
    \    if(t->l) propagate(t->l, t->add);\n      if(t->r) propagate(t->r, t->add);\n\
    \      t->add = 0;\n    }\n  }\n\nprivate:\n  void rotr(Node *t) {\n    auto *x\
    \ = t->p, *y = x->p;\n    if((x->l = t->r)) t->r->p = x;\n    t->r = x, x->p =\
    \ t;\n    update(x), update(t);\n    if((t->p = y)) {\n      if(y->l == x) y->l\
    \ = t;\n      if(y->r == x) y->r = t;\n      update(y);\n    }\n  }\n\n  void\
    \ rotl(Node *t) {\n    auto *x = t->p, *y = x->p;\n    if((x->r = t->l)) t->l->p\
    \ = x;\n    t->l = x, x->p = t;\n    update(x), update(t);\n    if((t->p = y))\
    \ {\n      if(y->l == x) y->l = t;\n      if(y->r == x) y->r = t;\n      update(y);\n\
    \    }\n  }\n\n  Node *merge(Node *l) {\n    return l;\n  }\n};\n\ntemplate< typename\
    \ T >\nstruct SlopeTrick {\n\n  const T INF = numeric_limits< T >::max() / 3;\n\
    \n  T min_f;\n  LazySplayTree< T > st;\n  typename LazySplayTree< T >::Node *L,\
    \ *R;\nprivate:\n  void push_R(const T &a) {\n    R = st.insert_lower_bound(R,\
    \ a);\n  }\n\n  T top_R() {\n    if(R) {\n      st.splay(R = st.get_left(R));\n\
    \      return R->key;\n    } else {\n      return INF;\n    }\n  }\n\n  T pop_R()\
    \ {\n    T val = top_R();\n    if(R) R = st.erase(R);\n    return val;\n  }\n\n\
    \  void push_L(const T &a) {\n    L = st.insert_lower_bound(L, a);\n  }\n\n  T\
    \ top_L() {\n    if(L) {\n      st.splay(L = st.get_right(L));\n      return L->key;\n\
    \    } else {\n      return -INF;\n    }\n\n  }\n\n  T pop_L() {\n    T val =\
    \ top_L();\n    if(L) L = st.erase(L);\n    return val;\n  }\n\n  size_t size()\
    \ {\n    return st.count(L) + st.count(R);\n  }\n\npublic:\n  SlopeTrick() : min_f(0),\
    \ L(nullptr), R(nullptr) {}\n\n  struct Query {\n    T lx, rx, min_f;\n  };\n\n\
    \  // return min f(x)\n  Query query() {\n    return (Query) {top_L(), top_R(),\
    \ min_f};\n  }\n\n  // f(x) += a\n  void add_all(const T &a) {\n    min_f += a;\n\
    \  }\n\n  // add \\_\n  // f(x) += max(a - x, 0)\n  void add_a_minus_x(const T\
    \ &a) {\n    min_f += max(T(0), a - top_R());\n    push_R(a);\n    push_L(pop_R());\n\
    \  }\n\n  // add _/\n  // f(x) += max(x - a, 0)\n  void add_x_minus_a(const T\
    \ &a) {\n    min_f += max(T(0), top_L() - a);\n    push_L(a);\n    push_R(pop_L());\n\
    \  }\n\n  // add \\/\n  // f(x) += abs(x - a)\n  void add_abs(const T &a) {\n\
    \    add_a_minus_x(a);\n    add_x_minus_a(a);\n  }\n\n  // \\/ -> \\_\n  // f_{new}\
    \ (x) = min f(y) (y <= x)\n  void clear_right() {\n    R = nullptr;\n  }\n\n \
    \ // \\/ -> _/\n  // f_{new} (x) = min f(y) (y >= x)\n  void clear_left() {\n\
    \    L = nullptr;\n  }\n\n  // \\/ -> \\_/\n  // f_{new} (x) = min f(y) (x-b <=\
    \ y <= x-a)\n  void shift(const T &a, const T &b) {\n    assert(a <= b);\n   \
    \ if(L) st.set_propagate(L, a);\n    if(R) st.set_propagate(R, b);\n  }\n\n  //\
    \ \\/. -> .\\/\n  // f_{new} (x) = f(x - a)\n  void shift(const T &a) {\n    shift(a,\
    \ a);\n  }\n\n  // return f(x) L, R \u3092\u7834\u58CA\u3059\u308B\n  T get(const\
    \ T &x) {\n    T ret = min_f;\n    {\n      auto[l, r] = st.split_lower_bound(L,\
    \ x);\n      if(r) {\n        ret += r->sum;\n        ret -= x * (T) st.count(r);\n\
    \      }\n      L = st.merge(l, r);\n    }\n    {\n      auto[l, r] = st.split_lower_bound(R,\
    \ x);\n      if(l) {\n        ret += x * (T) st.count(r);\n        ret -= l->sum;\n\
    \      }\n      R = st.merge(l, r);\n    }\n    return ret;\n  }\n\n  // f(x)\
    \ += g(x)\n  void merge(SlopeTrick &g) {\n    L = st.merge_wuh(L, g.L);\n    R\
    \ = st.merge_wuh(R, g.R);\n    min_f += g.min_f;\n  }\n};\n"
  dependsOn: []
  isVerificationFile: false
  path: structure/others/slope-trick.cpp
  requiredBy: []
  timestamp: '2021-04-25 21:55:44+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: structure/others/slope-trick.cpp
layout: document
redirect_from:
- /library/structure/others/slope-trick.cpp
- /library/structure/others/slope-trick.cpp.html
title: Slope-Trick
---
