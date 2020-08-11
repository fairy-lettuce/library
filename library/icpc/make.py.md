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


# :warning: icpc/make.py

<a href="../../index.html">Back to top page</a>

* category: <a href="../../index.html#2d899f8d163502b12eb4a60069f80c1c">icpc</a>
* <a href="{{ site.github.repository_url }}/blob/master/icpc/make.py">View this file on GitHub</a>
    - Last commit date: 1970-01-01 00:00:00+00:00




## Code

<a id="unbundled"></a>
{% raw %}
```cpp
import os

print("ICPC Library @ tapu")

for f in os.listdir(".."):
  if not os.path.isdir("../"+f):
    continue
  if f[0] == '.':
    continue
  if f == "icpc":
    continue

  print("-"*50)
  l = (50 - len(f)-2)//2
  r = (50 - len(f)-2)-l
  print("|"+" "*l+f+" "*r+"|")
  print("-"*50)
  print()

  for g in os.listdir("../"+f):
   name = g
   fp = "../" + f + "/" + g
   if not os.path.isfile(fp):
     continue

   print("#"*50)

   l = (50-len(name)-2)//2
   r = (50-len(name)-2)-l

   print("#"*l+" "+name+" "+"#"*r)
   print("#"*50)
   print("")
   with open(fp) as tap:
     print(tap.read())
   print("")

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
Traceback (most recent call last):
  File "/opt/hostedtoolcache/Python/3.8.5/x64/lib/python3.8/site-packages/onlinejudge_verify/docs.py", line 349, in write_contents
    bundled_code = language.bundle(self.file_class.file_path, basedir=pathlib.Path.cwd())
  File "/opt/hostedtoolcache/Python/3.8.5/x64/lib/python3.8/site-packages/onlinejudge_verify/languages/python.py", line 84, in bundle
    raise NotImplementedError
NotImplementedError

```
{% endraw %}

<a href="../../index.html">Back to top page</a>

