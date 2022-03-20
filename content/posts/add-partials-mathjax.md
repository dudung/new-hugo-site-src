---
title: "add partials mathjax"
date: 2022-03-20T09:36:00+07:00
lastmod: 2022-03-20T09:36:00+0700
author: viridi
draft: false
mathjax: true
math: false
tags: ['hugo', 'partials', 'mathjax']
url: "0003"
---
[[1](#r01)].


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

disimpan pada folder `themes\hugo-theme-codex\layouts\partials` yang dalam hal ini karena digunakan theme Hugo [[1](#r01)].

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
adalah suatu persaaman kuadrat. Nilai-
nilai $a$, $b$, dan $c$ perlu diketahui.
```

yang akan menghasilkan

Persamaan \eqref{eqn:quadratic-equation}
adalah suatu persaaman kuadrat. Nilai-
nilai $a$, $b$, dan $c$ perlu diketahui.


## notes
1. <a name='r01'></a>

1. <a name='r01'></a>Jake Wiesler, "This Site Is Now A Hugo Theme", 4 Jun 2020, url <https://www.jakewiesler.com/blog/hugo-theme-codex> [20220320].




