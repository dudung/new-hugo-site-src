---
title: "host hugo site on github"
date: 2022-03-19T08:30:00+07:00
lastmod: 2022-03-19T21:33:00+0700
author: viridi
draft: false
tags: ['hugo', 'github', 'host']
url: "0002"
---
Proses deploy situs yang dibuat dengan Hugo sebagai suatu proyek GitHub Pages dapat dilakukan secara otomatis dengan GitHub Action Workflow [[1](#r01)]. Dapat pula dilakukan secara manual dengan selalu memperbarui berkas-berkas pada folder `public` dan mengaturnya pada setting GitHub Pages atau melakukan otomatisasi semuanya [[2](#r02)]. Dapat juga dilakukan dengan bantuan Bash script untuk memperbarui, akan tetapi hasilnya agar dapat dilihat perlu dilakukan clone, instal Hugo, dan dibaca secara lokal [[3](#r03)]. Terdapat pula cara membuat branch `gh-pages` yang merupakan orphan branch [[4](#r04)]. Proses host situs yang dibuat dengan Hugo di GitHub tidak terlalu jelas, terutama saat melakukan proses build untuk branch `gh-pages` [[1](#r01)] dan juga telah dicoba bila branch `gh-pages` merupakan orphan branch [[4](#r04)], yang sayangnya keduanya tetap tidak berhasil. Antara tidak terjadi proses build dan deploy atau terjadi tetapi tidak ada halaman yang muncul.


## extended version
Saat melakukan proses build situs secara lokal diperoleh pesan kesalahan

```
L:\home\new-hugo-site>hugo
Start building sites …
hugo v0.95.0-9F2E76AF windows/amd64 BuildDate=2022-03-16T14:20:19Z VendorInfo=gohugoio
Error: Error building site: TOCSS: failed to transform "ananke/css/main.css" (text/css). Check your Hugo installation; you need the extended version to build SCSS/SASS.: this feature is not available in your current Hugo version, see https://goo.gl/YMrWcn for more information
Total in 3281 ms
```

yang dapat dipecahkan dengan mengunduh versi extended yang disarankan dari <https://github.com/gohugoio/hugo/releases/download/v0.95.0/hugo_extended_0.95.0_Windows-64bit.zip>

dan diinstal. Setelah itu pesan kesalahan di atas akan hilang.


## running the server
Server Hugo dapat dijalankan untuk membantun situs secara lokal

```
L:\home\new-hugo-site>hugo server -D
Start building sites …
hugo v0.95.0-9F2E76AF+extended windows/amd64 BuildDate=2022-03-16T14:20:19Z VendorInfo=gohugoio

                   | EN
-------------------+-----
  Pages            | 22
  Paginator pages  |  0
  Non-page files   |  0
  Static files     |  1
  Processed images |  0
  Aliases          |  1
  Sitemaps         |  1
  Cleaned          |  0

Built in 393 ms
Watching for changes in L:\home\new-hugo-site\{archetypes,content,themes}
Watching for config changes in L:\home\new-hugo-site\config.toml, L:\home\new-hugo-site\themes\ananke\config.yaml
Environment: "development"
Serving pages from memory
Running in Fast Render Mode. For full rebuilds on change: hugo server --disableFastRender
Web Server is available at http://localhost:1313/new-hugo-site/ (bind address 127.0.0.1)
Press Ctrl+C to stop
```

dengan

```toml
baseURL = 'https://dudung.github.io/new-hugo-site/'
languageCode = 'en-us'
title = 'new hugo site'
theme = 'ananke'

[frontmatter]
date = ['lastmod', 'publishDate', 'date']

[params]
date_format = "Mon, 02 Jan 2006"
```

adalah isi berkas `config.toml`. Situs yang dibuat Hugo dapat diakses di <http://localhost:1313/new-hugo-site/>.


## build the site
Proses build situs Hugo dilakukan dengan

```
L:\home\new-hugo-site>hugo
Start building sites …
hugo v0.95.0-9F2E76AF+extended windows/amd64 BuildDate=2022-03-16T14:20:19Z VendorInfo=gohugoio

                   | EN
-------------------+-----
  Pages            | 22
  Paginator pages  |  0
  Non-page files   |  0
  Static files     |  1
  Processed images |  0
  Aliases          |  1
  Sitemaps         |  1
  Cleaned          |  0

Total in 428 ms
```

yang akan menghasilkan

```
L:\home\new-hugo-site>tree public /f
Folder PATH listing for volume Linux
Volume serial number is ABCD-1234
L:\HOME\NEW-HUGO-SITE\PUBLIC
│   404.html
│   index.html
│   index.xml
│   sitemap.xml
│
├───0000
│       index.html
│
├───0001
│       index.html
│
├───0002
│       index.html
│
├───ananke
│   └───css
│           main.css.map
│           main.min.css
│
├───categories
│       index.html
│       index.xml
│
├───images
│       gohugo-default-sample-hero-image.jpg
│
├───posts
│   │   index.html
│   │   index.xml
│   │
│   └───page
│       └───1
│               index.html
│
└───tags
    │   index.html
    │   index.xml
    │
    ├───github
    │       index.html
    │       index.xml
    │
    ├───host
    │       index.html
    │       index.xml
    │
    ├───hugo
    │       index.html
    │       index.xml
    │
    ├───install
    │       index.html
    │       index.xml
    │
    └───windows
            index.html
            index.xml
```

dalam folder `public`.


## push public and github pages
Berkas-berkas yang terdapat pada folder `public` akan diunggah ke suatu repo di GitHub dengan fitur GitHub Pages aktif sehingga sekaligus melakukan proses hosting.

Sebelumnya perlu dibuat dulu repo `new-hugo-site` melalui <https://github.com/new>. Tidak perlu diisi berkas apapun.

Kemudian lakukan langkah-langkah berikut ini.

```
MINGW64 /l/home/new-hugo-site (master)
$ cd public/

MINGW64 /l/home/new-hugo-site/public (master)
$ git init
Initialized empty Git repository in L:/home/new-hugo-site/public/.git/

MINGW64 /l/home/new-hugo-site/public (master)
$ git remote add origin https://github.com/dudung/new-hugo-site.git

MINGW64 /l/home/new-hugo-site/public (master)
$ git add .
warning: LF will be replaced by CRLF in 0000/index.html.
The file will have its original line endings in your working directory
warning: LF will be replaced by CRLF in 0001/index.html.
The file will have its original line endings in your working directory
warning: LF will be replaced by CRLF in 0002/index.html.
The file will have its original line endings in your working directory
warning: LF will be replaced by CRLF in 404.html.
The file will have its original line endings in your working directory
warning: LF will be replaced by CRLF in ananke/css/main.css.map.
The file will have its original line endings in your working directory
warning: LF will be replaced by CRLF in categories/index.html.
The file will have its original line endings in your working directory
warning: LF will be replaced by CRLF in categories/index.xml.
The file will have its original line endings in your working directory
warning: LF will be replaced by CRLF in index.html.
The file will have its original line endings in your working directory
warning: LF will be replaced by CRLF in index.xml.
The file will have its original line endings in your working directory
warning: LF will be replaced by CRLF in posts/index.html.
The file will have its original line endings in your working directory
warning: LF will be replaced by CRLF in posts/index.xml.
The file will have its original line endings in your working directory
warning: LF will be replaced by CRLF in posts/page/1/index.html.
The file will have its original line endings in your working directory
warning: LF will be replaced by CRLF in sitemap.xml.
The file will have its original line endings in your working directory
warning: LF will be replaced by CRLF in tags/github/index.html.
The file will have its original line endings in your working directory
warning: LF will be replaced by CRLF in tags/github/index.xml.
The file will have its original line endings in your working directory
warning: LF will be replaced by CRLF in tags/host/index.html.
The file will have its original line endings in your working directory
warning: LF will be replaced by CRLF in tags/host/index.xml.
The file will have its original line endings in your working directory
warning: LF will be replaced by CRLF in tags/hugo/index.html.
The file will have its original line endings in your working directory
warning: LF will be replaced by CRLF in tags/hugo/index.xml.
The file will have its original line endings in your working directory
warning: LF will be replaced by CRLF in tags/index.html.
The file will have its original line endings in your working directory
warning: LF will be replaced by CRLF in tags/index.xml.
The file will have its original line endings in your working directory
warning: LF will be replaced by CRLF in tags/install/index.html.
The file will have its original line endings in your working directory
warning: LF will be replaced by CRLF in tags/install/index.xml.
The file will have its original line endings in your working directory
warning: LF will be replaced by CRLF in tags/windows/index.html.
The file will have its original line endings in your working directory
warning: LF will be replaced by CRLF in tags/windows/index.xml.
The file will have its original line endings in your working directory

MINGW64 /l/home/new-hugo-site/public (master)
$ git commit -m "Initial commit"
[master (root-commit) d8e8d80] Initial commit
 27 files changed, 2882 insertions(+)
 create mode 100644 0000/index.html
 create mode 100644 0001/index.html
 create mode 100644 0002/index.html
 create mode 100644 404.html
 create mode 100644 ananke/css/main.css.map
 create mode 100644 ananke/css/main.min.css
 create mode 100644 categories/index.html
 create mode 100644 categories/index.xml
 create mode 100644 images/gohugo-default-sample-hero-image.jpg
 create mode 100644 index.html
 create mode 100644 index.xml
 create mode 100644 posts/index.html
 create mode 100644 posts/index.xml
 create mode 100644 posts/page/1/index.html
 create mode 100644 sitemap.xml
 create mode 100644 tags/github/index.html
 create mode 100644 tags/github/index.xml
 create mode 100644 tags/host/index.html
 create mode 100644 tags/host/index.xml
 create mode 100644 tags/hugo/index.html
 create mode 100644 tags/hugo/index.xml
 create mode 100644 tags/index.html
 create mode 100644 tags/index.xml
 create mode 100644 tags/install/index.html
 create mode 100644 tags/install/index.xml
 create mode 100644 tags/windows/index.html
 create mode 100644 tags/windows/index.xml

MINGW64 /l/home/new-hugo-site/public (master)
$ git push --set-upstream origin master
remote: Repository not found.
fatal: repository 'https://github.com/dudung/new-hugo-site.git/' not found

MINGW64 /l/home/new-hugo-site/public (master)
$ git push --set-upstream origin master
Enumerating objects: 45, done.
Counting objects: 100% (45/45), done.
Delta compression using up to 4 threads
Compressing objects: 100% (39/39), done.
Writing objects: 100% (45/45), 333.80 KiB | 4.39 MiB/s, done.
Total 45 (delta 17), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (17/17), done.
To https://github.com/dudung/new-hugo-site.git
 * [new branch]      master -> master
branch 'master' set up to track 'origin/master'.
```

Fitur GitHub Pages dapat diaktifkan dengan mengakses halaman <https://github.com/dudung/new-hugo-site/settings/pages> pada bagian **Source**. Ganti nilai `None` menjadi `master` dan klik tombol **Save**. Tunggu beberapa saat dan situs web <https://dudung.github.io/new-hugo-site/> telah jalan.


## push code to separate repo
Kode dan isi dari situs Hugo yang dibuat akan disimpan dalam repo terpisah di GitHub.

```
$ cd ..

MINGW64 /l/home/new-hugo-site (master)
$ echo "public/" >> .gitignore

MINGW64 /l/home/new-hugo-site (master)
$ git init
Initialized empty Git repository in L:/home/new-hugo-site/.git/
```


## notes
1. <a name='r01'></a>"Host on GitHub", Hugo, 2 Feb 2022, url <https://gohugo.io/hosting-and-deployment/hosting-on-github/> [20220319].
2. <a name='r02'></a>Carlos Pons, "Create and host a blog with Hugo and GitHub Pages in less than 30 minutes", my tech rahmblings, 21 Jun 2020, url <https://www.mytechramblings.com/posts/create-a-website-with-hugo-and-gh/> [20220319].
3. <a name='r03'></a>Ahmad Muhardian, "Cara Hosting/Deploy Hugo di Github", Petani Kode, 13 Mar 2022, url <https://www.petanikode.com/hugo-hosting-github/> [20220319].
4. <a name='r04'></a>Jia Fu Low, "Create gh-pages branch in existing repo", Github, 9 Jul 2020, url <https://jiafulow.github.io/blog/2020/07/09/create-gh-pages-branch-in-existing-repo/> [20220319].
