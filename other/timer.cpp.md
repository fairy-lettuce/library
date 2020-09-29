---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith: []
  _pathExtension: cpp
  _verificationStatusIcon: ':warning:'
  attributes:
    _deprecated_at_docs: docs/timer.md
    document_title: "Timer(\u30BF\u30A4\u30DE\u30FC)"
    links: []
  bundledCode: "#line 1 \"other/timer.cpp\"\n/**\n * @brief Timer(\u30BF\u30A4\u30DE\
    \u30FC)\n * @docs docs/timer.md\n */\nconstexpr uint64_t CYCLES_PER_SEC = 3000000000;\
    \ // AtCoder\n// constexpr uint64_t CYCLES_PER_SEC = 3600000000; // Codeforces\n\
    // constexpr uint64_t CYCLES_PER_SEC = 2300000000; // yukicoder\nstruct Timer\
    \ {\n  uint64_t start;\n\n  Timer() : start{} { reset(); }\n\n  void reset() {\
    \ start = get_cycle(); }\n\n  inline double get_second() const { return (double)\
    \ get_cycle() / CYCLES_PER_SEC; }\n\n  inline uint64_t get_cycle() const {\n \
    \   unsigned low, high;\n    __asm__ volatile (\"rdtsc\" : \"=a\" (low), \"=d\"\
    \ (high));\n    return (((uint64_t) low) | ((uint64_t) high << 32ull)) - start;\n\
    \  }\n};\n"
  code: "/**\n * @brief Timer(\u30BF\u30A4\u30DE\u30FC)\n * @docs docs/timer.md\n\
    \ */\nconstexpr uint64_t CYCLES_PER_SEC = 3000000000; // AtCoder\n// constexpr\
    \ uint64_t CYCLES_PER_SEC = 3600000000; // Codeforces\n// constexpr uint64_t CYCLES_PER_SEC\
    \ = 2300000000; // yukicoder\nstruct Timer {\n  uint64_t start;\n\n  Timer() :\
    \ start{} { reset(); }\n\n  void reset() { start = get_cycle(); }\n\n  inline\
    \ double get_second() const { return (double) get_cycle() / CYCLES_PER_SEC; }\n\
    \n  inline uint64_t get_cycle() const {\n    unsigned low, high;\n    __asm__\
    \ volatile (\"rdtsc\" : \"=a\" (low), \"=d\" (high));\n    return (((uint64_t)\
    \ low) | ((uint64_t) high << 32ull)) - start;\n  }\n};\n"
  dependsOn: []
  isVerificationFile: false
  path: other/timer.cpp
  requiredBy: []
  timestamp: '2020-07-10 00:47:43+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: other/timer.cpp
layout: document
redirect_from:
- /library/other/timer.cpp
- /library/other/timer.cpp.html
title: "Timer(\u30BF\u30A4\u30DE\u30FC)"
---
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

