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


# :warning: other/dice.cpp
* category: other


[Back to top page](../../index.html)



## Code
```cpp
struct Dice
{
  // int x, y;
  int l, r, f, b, d, u;

  void RollN()
  {
    //  --y;
    int buff = d;
    d = f;
    f = u;
    u = b;
    b = buff;
  }

  void RollS()
  {
    // ++y;
    int buff = d;
    d = b;
    b = u;
    u = f;
    f = buff;
  }

  void RollL() // ----->
  {
    int buff = f;
    f = l;
    l = b;
    b = r;
    r = buff;
  }

  void RollR() // <------
  {
    int buff = f;
    f = r;
    r = b;
    b = l;
    l = buff;
  }

  void RollE() // .o -> o.
  {
    // --x;
    int buff = d;
    d = l;
    l = u;
    u = r;
    r = buff;
  }


  void RollW() // o. -> .o
  {
    //  ++x;
    int buff = d;
    d = r;
    r = u;
    u = l;
    l = buff;
  }


  vector< Dice > makeDice()
  {
    vector< Dice > ret;
    for(int i = 0; i < 6; i++) {
      Dice d(*this);
      if(i == 1) d.RollN();
      if(i == 2) d.RollS();
      if(i == 3) d.RollS(), d.RollS();
      if(i == 4) d.RollL();
      if(i == 5) d.RollR();
      for(int j = 0; j < 4; j++) {
        ret.emplace_back(d);
        d.RollE();
      }
    }
    return (ret);
  }
};

```

[Back to top page](../../index.html)

