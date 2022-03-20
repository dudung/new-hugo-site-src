---
title: "add partials mathjax"
date: 2022-03-20T09:36:00+07:00
lastmod: 2022-03-20T11:27:00+0700
author: viridi
draft: false
mathjax: true
tags: ['hugo', 'partials', 'mathjax']
url: "0003"
---
Salah satu theme Hugo yang disebut Codex telah dapat menampilkan formula matematika dengan MathJax [[1](#r01)]. Implementasi yang dilakukan belum memuncukan nomor persamaan dan masih menggunakan MathJax versi 2.7.2 [[2](#r02)]. Cara Untuk memunculkan penomoran persamaan terdapat cara yang berbeda pada MathJax 3 [[3](#r03)] dibandingkan dengan pada versi sebelumnya.


## mathjax.html
Suatu berkas `mathjax.html`  berisikan

```html
<!-- layouts/partials/mathjax.html -->

<script>
  MathJax = {
    tex: {
      inlineMath: [['$', '$'], ['\\(', '\\)']],
      displayMath: [['$$','$$'], ['\\[', '\\]']],
      processEscapes: true,
      processEnvironments: true,
      tags: 'ams',
    },
    options: {
      skipHtmlTags: [
        'script',
        'noscript',
        'style',
        'textarea',
        'pre'
      ]
    }
  };
</script>

<script
  type="text/javascript"
  id="MathJax-script"
  async 
  src="https://cdn.jsdelivr.net/npm/\
  mathjax@3/es5/tex-mml-chtml.js"
>
</script>
```

disimpan pada folder `themes/hugo-theme-codex/layouts/partials`, yang dalam hal ini karena digunakan theme Hugo Codex [[1](#r01)]. Kemudian untuk menyisipkannya dalam setiap artikel (post) dibuat perlu ditambahkan

```go
{{ if or .Params.mathjax .Site.Params.mathjax }}
    {{ partial "mathjax.html" . }}
{{ end }}
```

pada berkas `themes/hugo-theme-codex/layouts/_default/single.html`.


## result
Kode $\LaTeX$ berikut

```
\begin{equation}\label{eqn:quadratic-equation}
y = ax^2 + bx + c
\end{equation}
```

akan menghasilkan

\begin{equation}\label{eqn:quadratic-equation}
y = ax^2 + bx + c.
\end{equation}

Persamaan di atas dapat dirujuk dengan, misalnya dengan

```
Persamaan \eqref{eqn:quadratic-equation}
adalah suatu persaaman kuadrat.
Nilai-nilai $a$, $b$, dan $c$ perlu diketahui.
```

yang akan menghasilkan

Persamaan \eqref{eqn:quadratic-equation}
adalah suatu persaaman kuadrat.
Nilai-nilai $a$, $b$, dan $c$ perlu diketahui.


## math libs
MathJax versi 3 sudah lebih cepat dibandingkan versi 2.7, akan tetapi masih sedikit lebih lambat dibandingkan dengan KaTex [[4](#r04)] yang saat ini telah mendukung bebagai fungsi [[5](#r05)].


## notes
1. <a name='r01'></a>Jake Wiesler, "This Site Is Now A Hugo Theme", 4 Jun 2020, url <https://www.jakewiesler.com/blog/hugo-theme-codex> [20220320].
2. <a name='r02'></a>Chuxin Huang, "add math", GitHub, 5 Jun 2020, url <https://github.com/jakewies/hugo-theme-codex/commit/63546f792f15e18da966cdcdce1bf7a6c465c016#diff-25f0c449e004eb6cb00227f5b5ace367c223dbc50d2fb5528642590574c851ee> [20220320].
3. <a name='r03'></a>"Automatic Equation Numbering", MathJax, The MathJax Consortium Revision e40ff4a5, 2021, url <https://docs.mathjax.org/en/latest/input/tex/eqnumbers.html> [20220320].
4. <a name='r04'></a>Murray Bourne, "KaTeX and MathJax Comparison Demo", IntMath.com, 29 Apr 2020, url <https://www.intmath.com/cg5/katex-mathjax-comparison.php> [20220320].
5. <a name='r05'></a>Khan Academy and other contributors, "Supported Functions", KaTeX, 2022, url <https://katex.org/docs/supported.html> [20220320].
