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


# :heavy_check_mark: Fibonacchi-Heap(フィボナッチヒープ) <small>(structure/heap/fibonacchi-heap.cpp)</small>

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#36999f024b84f3ad86db908172fedb57">structure/heap</a>
* <a href="{{ site.github.repository_url }}/blob/master/structure/heap/fibonacchi-heap.cpp">View this file on GitHub</a>
    - Last commit date: 2020-08-20 17:25:40+09:00


* see: <a href="https://www.cs.princeton.edu/~wayne/teaching/fibonacci-heap.pdf">https://www.cs.princeton.edu/~wayne/teaching/fibonacci-heap.pdf</a>


## Verified with

* :heavy_check_mark: <a href="../../../verify/test/verify/aoj-grl-1-a-2.test.cpp.html">test/verify/aoj-grl-1-a-2.test.cpp</a>
* :heavy_check_mark: <a href="../../../verify/test/verify/aoj-grl-2-a-4.test.cpp.html">test/verify/aoj-grl-2-a-4.test.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
/**
 * @brief Fibonacchi-Heap(フィボナッチヒープ)
 * @see https://www.cs.princeton.edu/~wayne/teaching/fibonacci-heap.pdf
 */
template< typename key_t, typename val_t >
struct FibonacchiHeap {
  struct Node {
    key_t key;
    val_t val;
    Node *left, *right, *child, *par;
    int sz;
    bool mark;

    Node(const key_t &key, const val_t &val)
        : key(key), val(val), left(this), right(this), par(nullptr), child(nullptr), sz(0), mark(false) {}
  };

  Node *root;
  size_t sz;
  vector< Node * > rank;

  FibonacchiHeap() : root(nullptr), sz(0) {}

  size_t size() const {
    return sz;
  }

  bool empty() const {
    return sz == 0;
  }

  void update_min(Node *t) {
    if(!root || t->key < root->key) {
      root = t;
    }
  }

  void concat(Node *&r, Node *t) {
    if(!r) {
      r = t;
    } else {
      t->left->right = r->right;
      r->right->left = t->left;
      t->left = r;
      r->right = t;
    }
  }

  void delete_node(Node *t) {
    t->left->right = t->right;
    t->right->left = t->left;
    t->left = t;
    t->right = t;
  }

  Node *push(const key_t &key, const val_t &val) {
    ++sz;
    auto node = new Node(key, val);
    concat(root, node);
    update_min(node);
    return node;
  }


  Node *consolidate(Node *s, Node *t) {
    if(root == s || s->key < t->key) {
      delete_node(t);
      ++s->sz;
      t->par = s;
      concat(s->child, t);
      return s;
    } else {
      delete_node(s);
      ++t->sz;
      s->par = t;
      concat(t->child, s);
      return t;
    }
  }


  pair< key_t, val_t > pop() {
    --sz;

    Node *rem = root;


    auto ret = make_pair(rem->key, rem->val);

    {
      root = root->left == root ? nullptr : root->left;
      delete_node(rem);
    }


    if(rem->child) {
      concat(root, rem->child);
    }


    if(root) {

      {
        Node *base = root, *cur = base;
        do {
          cur->par = nullptr;
          update_min(cur);
          cur = cur->right;
        } while(cur != base);
      }


      {
        Node *base = root;
        int last = -1;
        do {
          Node *nxt = base->right;
          while(base->sz < rank.size() && rank[base->sz]) {
            Node *u = rank[base->sz];
            rank[base->sz] = nullptr;
            base = consolidate(u, base);
          }
          if(base->sz >= rank.size()) rank.resize(base->sz + 1);
          last = max(last, base->sz);
          rank[base->sz] = base;
          base = nxt;
        } while(base != root);

        for(int i = last; i >= 0; i--) rank[i] = nullptr;
      }
    }

    return ret;
  }

  inline void mark_dfs(Node *t) {
    if(!t->par) {
      t->mark = false;
    } else if(t->mark) {
      mark_dfs(t->par);
      t->par->child = t->left == t ? nullptr : t->left;
      delete_node(t);
      t->sz--;
      t->mark = false;
      t->par = nullptr;
      concat(root, t);
    } else {
      t->mark = true;
      t->sz--;
    }
  }


  void decrease_key(Node *t, const key_t &d) {
    t->key -= d;

    if(!t->par) {
      update_min(t);
      return;
    }

    if(t->par->key <= t->key) {
      return;
    }

    t->sz++;
    t->mark = true;
    mark_dfs(t);
    update_min(t);
  }
};

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "structure/heap/fibonacchi-heap.cpp"
/**
 * @brief Fibonacchi-Heap(フィボナッチヒープ)
 * @see https://www.cs.princeton.edu/~wayne/teaching/fibonacci-heap.pdf
 */
template< typename key_t, typename val_t >
struct FibonacchiHeap {
  struct Node {
    key_t key;
    val_t val;
    Node *left, *right, *child, *par;
    int sz;
    bool mark;

    Node(const key_t &key, const val_t &val)
        : key(key), val(val), left(this), right(this), par(nullptr), child(nullptr), sz(0), mark(false) {}
  };

  Node *root;
  size_t sz;
  vector< Node * > rank;

  FibonacchiHeap() : root(nullptr), sz(0) {}

  size_t size() const {
    return sz;
  }

  bool empty() const {
    return sz == 0;
  }

  void update_min(Node *t) {
    if(!root || t->key < root->key) {
      root = t;
    }
  }

  void concat(Node *&r, Node *t) {
    if(!r) {
      r = t;
    } else {
      t->left->right = r->right;
      r->right->left = t->left;
      t->left = r;
      r->right = t;
    }
  }

  void delete_node(Node *t) {
    t->left->right = t->right;
    t->right->left = t->left;
    t->left = t;
    t->right = t;
  }

  Node *push(const key_t &key, const val_t &val) {
    ++sz;
    auto node = new Node(key, val);
    concat(root, node);
    update_min(node);
    return node;
  }


  Node *consolidate(Node *s, Node *t) {
    if(root == s || s->key < t->key) {
      delete_node(t);
      ++s->sz;
      t->par = s;
      concat(s->child, t);
      return s;
    } else {
      delete_node(s);
      ++t->sz;
      s->par = t;
      concat(t->child, s);
      return t;
    }
  }


  pair< key_t, val_t > pop() {
    --sz;

    Node *rem = root;


    auto ret = make_pair(rem->key, rem->val);

    {
      root = root->left == root ? nullptr : root->left;
      delete_node(rem);
    }


    if(rem->child) {
      concat(root, rem->child);
    }


    if(root) {

      {
        Node *base = root, *cur = base;
        do {
          cur->par = nullptr;
          update_min(cur);
          cur = cur->right;
        } while(cur != base);
      }


      {
        Node *base = root;
        int last = -1;
        do {
          Node *nxt = base->right;
          while(base->sz < rank.size() && rank[base->sz]) {
            Node *u = rank[base->sz];
            rank[base->sz] = nullptr;
            base = consolidate(u, base);
          }
          if(base->sz >= rank.size()) rank.resize(base->sz + 1);
          last = max(last, base->sz);
          rank[base->sz] = base;
          base = nxt;
        } while(base != root);

        for(int i = last; i >= 0; i--) rank[i] = nullptr;
      }
    }

    return ret;
  }

  inline void mark_dfs(Node *t) {
    if(!t->par) {
      t->mark = false;
    } else if(t->mark) {
      mark_dfs(t->par);
      t->par->child = t->left == t ? nullptr : t->left;
      delete_node(t);
      t->sz--;
      t->mark = false;
      t->par = nullptr;
      concat(root, t);
    } else {
      t->mark = true;
      t->sz--;
    }
  }


  void decrease_key(Node *t, const key_t &d) {
    t->key -= d;

    if(!t->par) {
      update_min(t);
      return;
    }

    if(t->par->key <= t->key) {
      return;
    }

    t->sz++;
    t->mark = true;
    mark_dfs(t);
    update_min(t);
  }
};

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

