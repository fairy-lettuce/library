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
<script type="text/javascript" src="../../assets/js/copy-button.js"></script>
<link rel="stylesheet" href="../../assets/css/copy-button.css" />


# :warning: Timer(タイマー) <small>(other/timer.cpp)</small>

<a href="../../index.html">Back to top page</a>

* category: <a href="../../index.html#795f3202b17cb6bc3d4b771d8c6c9eaf">other</a>
* <a href="{{ site.github.repository_url }}/blob/master/other/timer.cpp">View this file on GitHub</a>
    - Last commit date: 2020-07-10 00:47:43+09:00




## 概要
rdtsc (Read Time Stamp Counter) 命令を用いると CPU クロックごとに加算される 64 bit のタイムスタンプカウンタの値を得ることができる. マラソンするときにタイマーとしてよく用いられるらしい.

CPUのクロック周波数がわかれば, カウンタの値から実行時間を推定することができる. 参考までにAtCoder では 3.00GHz, Codeforces では 3.60GHz, yukicoder では 2.3GHz (2020/06/30現在).

## ベンチマーク
$10^8$ 回呼び出したときの実行時間の比較. 間違っていたらごめんなさい.

AtCoder:

- `clock()`: inf
- `chrono::high_resolution_clock::now()`: 2150 ms
- `rdtsc`: 750 ms

Codeforces:

- `clock()`: 870 ms 
- `chrono::high_resolution_clock::now()`: 1660 ms
- `rdtsc`: 700 ms

yukicoder:

- `clock()`: inf 
- `chrono::high_resolution_clock::now()`: 3330 ms
- `rdtsc`: 1020 ms



## Code

<a id="unbundled"></a>
{% raw %}
```cpp
/**
 * @brief Timer(タイマー)
 * @docs docs/timer.md
 */
constexpr uint64_t CYCLES_PER_SEC = 3000000000; // AtCoder
// constexpr uint64_t CYCLES_PER_SEC = 3600000000; // Codeforces
// constexpr uint64_t CYCLES_PER_SEC = 2300000000; // yukicoder
struct Timer {
  uint64_t start;

  Timer() : start{} { reset(); }

  void reset() { start = get_cycle(); }

  inline double get_second() const { return (double) get_cycle() / CYCLES_PER_SEC; }

  inline uint64_t get_cycle() const {
    unsigned low, high;
    __asm__ volatile ("rdtsc" : "=a" (low), "=d" (high));
    return (((uint64_t) low) | ((uint64_t) high << 32ull)) - start;
  }
};

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "other/timer.cpp"
/**
 * @brief Timer(タイマー)
 * @docs docs/timer.md
 */
constexpr uint64_t CYCLES_PER_SEC = 3000000000; // AtCoder
// constexpr uint64_t CYCLES_PER_SEC = 3600000000; // Codeforces
// constexpr uint64_t CYCLES_PER_SEC = 2300000000; // yukicoder
struct Timer {
  uint64_t start;

  Timer() : start{} { reset(); }

  void reset() { start = get_cycle(); }

  inline double get_second() const { return (double) get_cycle() / CYCLES_PER_SEC; }

  inline uint64_t get_cycle() const {
    unsigned low, high;
    __asm__ volatile ("rdtsc" : "=a" (low), "=d" (high));
    return (((uint64_t) low) | ((uint64_t) high << 32ull)) - start;
  }
};

```
{% endraw %}

<a href="../../index.html">Back to top page</a>

