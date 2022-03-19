---
title: "host hugo site on github"
date: 2022-03-19T08:30:00+07:00
lastmod: 2022-03-19T22:50:00+0700
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

$ echo "public/" >> .gitignore

$ git init
Initialized empty Git repository in L:/home/new-hugo-site/.git/

$ git add .
warning: LF will be replaced by CRLF in .gitignore.
The file will have its original line endings in your working directory
warning: LF will be replaced by CRLF in .gitmodules.
The file will have its original line endings in your working directory

$ git commit -m "Add site files"
[master (root-commit) e5be59c] Add site files
 129 files changed, 4218 insertions(+)
 create mode 100644 .gitignore
 create mode 100644 .gitmodules
 create mode 100644 .hugo_build.lock
 create mode 100644 archetypes/default.md
 create mode 100644 config.toml
 create mode 100644 content/posts/create-new-site-hugo.md
 create mode 100644 content/posts/host-hugo-site-on-github.md
 create mode 100644 content/posts/install-hugo-windows-10.md
 create mode 100644 resources/_gen/assets/css/new-hugo-site/ananke/css/main.css_bb5467e0521bbea6b1e66429f6ec028e.content
 create mode 100644 resources/_gen/assets/css/new-hugo-site/ananke/css/main.css_bb5467e0521bbea6b1e66429f6ec028e.json
 create mode 100644 themes/ananke/.gitignore
 create mode 100644 themes/ananke/CHANGELOG.md
 create mode 100644 themes/ananke/LICENSE.md
 create mode 100644 themes/ananke/README.md
 create mode 100644 themes/ananke/archetypes/default.md
 create mode 100644 themes/ananke/assets/ananke/css/_code.css
 create mode 100644 themes/ananke/assets/ananke/css/_hugo-internal-templates.css
 create mode 100644 themes/ananke/assets/ananke/css/_social-icons.css
 create mode 100644 themes/ananke/assets/ananke/css/_styles.css
 create mode 100644 themes/ananke/assets/ananke/css/_tachyons.css
 create mode 100644 themes/ananke/assets/ananke/dist/main.css_5c99d70a7725bacd4c701e995b969fea.css
 create mode 100644 themes/ananke/assets/ananke/socials/facebook.svg
 create mode 100644 themes/ananke/assets/ananke/socials/github.svg
 create mode 100644 themes/ananke/assets/ananke/socials/gitlab.svg
 create mode 100644 themes/ananke/assets/ananke/socials/instagram.svg
 create mode 100644 themes/ananke/assets/ananke/socials/keybase.svg
 create mode 100644 themes/ananke/assets/ananke/socials/linkedin.svg
 create mode 100644 themes/ananke/assets/ananke/socials/mastodon.svg
 create mode 100644 themes/ananke/assets/ananke/socials/medium.svg
 create mode 100644 themes/ananke/assets/ananke/socials/rss.svg
 create mode 100644 themes/ananke/assets/ananke/socials/slack.svg
 create mode 100644 themes/ananke/assets/ananke/socials/stackoverflow.svg
 create mode 100644 themes/ananke/assets/ananke/socials/tiktok.svg
 create mode 100644 themes/ananke/assets/ananke/socials/twitter.svg
 create mode 100644 themes/ananke/assets/ananke/socials/youtube.svg
 create mode 100644 themes/ananke/config.yaml
 create mode 100644 themes/ananke/exampleSite/config.toml
 create mode 100644 themes/ananke/exampleSite/content/en/_index.md
 create mode 100644 themes/ananke/exampleSite/content/en/about/index.md
 create mode 100644 themes/ananke/exampleSite/content/en/contact.md
 create mode 100644 themes/ananke/exampleSite/content/en/post/_index.md
 create mode 100644 themes/ananke/exampleSite/content/en/post/chapter-1.md
 create mode 100644 themes/ananke/exampleSite/content/en/post/chapter-2.md
 create mode 100644 themes/ananke/exampleSite/content/en/post/chapter-3.md
 create mode 100644 themes/ananke/exampleSite/content/en/post/chapter-4.md
 create mode 100644 themes/ananke/exampleSite/content/en/post/chapter-5.md
 create mode 100644 themes/ananke/exampleSite/content/en/post/chapter-6.md
 create mode 100644 themes/ananke/exampleSite/content/fr/_index.md
 create mode 100644 themes/ananke/exampleSite/content/fr/contact.md
 create mode 100644 themes/ananke/exampleSite/content/fr/post/_index.md
 create mode 100644 themes/ananke/exampleSite/content/fr/post/chapter-1.md
 create mode 100644 themes/ananke/exampleSite/go.mod
 create mode 100644 themes/ananke/exampleSite/go.sum
 create mode 100644 themes/ananke/exampleSite/static/images/Pope-Edouard-de-Beaumont-1844.jpg
 create mode 100644 themes/ananke/exampleSite/static/images/Victor_Hugo-Hunchback.jpg
 create mode 100644 themes/ananke/exampleSite/static/images/esmeralda.jpg
 create mode 100644 themes/ananke/exampleSite/static/images/notebook.jpg
 create mode 100644 themes/ananke/go.mod
 create mode 100644 themes/ananke/i18n/bg.toml
 create mode 100644 themes/ananke/i18n/de.toml
 create mode 100644 themes/ananke/i18n/en.toml
 create mode 100644 themes/ananke/i18n/es.toml
 create mode 100644 themes/ananke/i18n/fi.toml
 create mode 100644 themes/ananke/i18n/fr.toml
 create mode 100644 themes/ananke/i18n/hi.toml
 create mode 100644 themes/ananke/i18n/hu.toml
 create mode 100644 themes/ananke/i18n/it.toml
 create mode 100644 themes/ananke/i18n/nl.toml
 create mode 100644 themes/ananke/i18n/no.toml
 create mode 100644 themes/ananke/i18n/pt.toml
 create mode 100644 themes/ananke/i18n/ru.toml
 create mode 100644 themes/ananke/i18n/sv.toml
 create mode 100644 themes/ananke/i18n/tr.toml
 create mode 100644 themes/ananke/i18n/uk.toml
 create mode 100644 themes/ananke/i18n/zh-tw.toml
 create mode 100644 themes/ananke/i18n/zh.toml
 create mode 100644 themes/ananke/images/screenshot.png
 create mode 100644 themes/ananke/images/tn.png
 create mode 100644 themes/ananke/layouts/404.html
 create mode 100644 themes/ananke/layouts/_default/baseof.html
 create mode 100644 themes/ananke/layouts/_default/list.html
 create mode 100644 themes/ananke/layouts/_default/single.html
 create mode 100644 themes/ananke/layouts/_default/summary-with-image.html
 create mode 100644 themes/ananke/layouts/_default/summary.html
 create mode 100644 themes/ananke/layouts/_default/taxonomy.html
 create mode 100644 themes/ananke/layouts/_default/terms.html
 create mode 100644 themes/ananke/layouts/index.html
 create mode 100644 themes/ananke/layouts/page/single.html
 create mode 100644 themes/ananke/layouts/partials/commento.html
 create mode 100644 themes/ananke/layouts/partials/func/GetFeaturedImage.html
 create mode 100644 themes/ananke/layouts/partials/func/socials/Get.html
 create mode 100644 themes/ananke/layouts/partials/func/socials/GetBuiltInServicesDefaults.html
 create mode 100644 themes/ananke/layouts/partials/func/socials/GetRegisteredServices.html
 create mode 100644 themes/ananke/layouts/partials/func/socials/GetServiceData.html
 create mode 100644 themes/ananke/layouts/partials/func/socials/GetServiceIcon.html
 create mode 100644 themes/ananke/layouts/partials/func/style/GetMainCSS.html
 create mode 100644 themes/ananke/layouts/partials/func/style/GetResource.html
 create mode 100644 themes/ananke/layouts/partials/func/warn.html
 create mode 100644 themes/ananke/layouts/partials/head-additions.html
 create mode 100644 themes/ananke/layouts/partials/i18nlist.html
 create mode 100644 themes/ananke/layouts/partials/menu-contextual.html
 create mode 100644 themes/ananke/layouts/partials/new-window-icon.html
 create mode 100644 themes/ananke/layouts/partials/page-header.html
 create mode 100644 themes/ananke/layouts/partials/site-favicon.html
 create mode 100644 themes/ananke/layouts/partials/site-footer.html
 create mode 100644 themes/ananke/layouts/partials/site-header.html
 create mode 100644 themes/ananke/layouts/partials/site-navigation.html
 create mode 100644 themes/ananke/layouts/partials/site-scripts.html
 create mode 100644 themes/ananke/layouts/partials/site-style.html
 create mode 100644 themes/ananke/layouts/partials/social-follow.html
 create mode 100644 themes/ananke/layouts/partials/social-share.html
 create mode 100644 themes/ananke/layouts/partials/summary-with-image.html
 create mode 100644 themes/ananke/layouts/partials/summary.html
 create mode 100644 themes/ananke/layouts/partials/svg/new-window.svg
 create mode 100644 themes/ananke/layouts/partials/svg/tiktok.svg
 create mode 100644 themes/ananke/layouts/partials/tags.html
 create mode 100644 themes/ananke/layouts/post/list.html
 create mode 100644 themes/ananke/layouts/post/summary.html
 create mode 100644 themes/ananke/layouts/robots.txt
 create mode 100644 themes/ananke/layouts/shortcodes/form-contact.html
 create mode 100644 themes/ananke/package.hugo.json
 create mode 100644 themes/ananke/package.json
 create mode 100644 themes/ananke/resources/_gen/assets/css/ananke/css/main.css_5c99d70a7725bacd4c701e995b969fea.content
 create mode 100644 themes/ananke/resources/_gen/assets/css/ananke/css/main.css_5c99d70a7725bacd4c701e995b969fea.json
 create mode 100644 themes/ananke/resources/_gen/assets/css/ananke/css/main.css_bb5467e0521bbea6b1e66429f6ec028e.content
 create mode 100644 themes/ananke/resources/_gen/assets/css/ananke/css/main.css_bb5467e0521bbea6b1e66429f6ec028e.json
 create mode 100644 themes/ananke/stackbit.yaml
 create mode 100644 themes/ananke/static/images/gohugo-default-sample-hero-image.jpg
 create mode 100644 themes/ananke/theme.toml
 ```

Buat terlebih dahulu repo `new-hugo-site-src` melalui <https://github.com/new>. Kemudian lanjutkan langkah-langkah berikut ini.

```
MINGW64 /l/home/new-hugo-site (master)
$ git remote add origin https://github.com/dudung/new-hugo-site-src.git

MINGW64 /l/home/new-hugo-site (master)
$ git push --set-upstream origin master
Enumerating objects: 174, done.
Counting objects: 100% (174/174), done.
Delta compression using up to 4 threads
Compressing objects: 100% (149/149), done.
Writing objects: 100% (174/174), 2.61 MiB | 101.00 KiB/s, done.
Total 174 (delta 14), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (14/14), done.
To https://github.com/dudung/new-hugo-site-src.git
 * [new branch]      master -> master
branch 'master' set up to track 'origin/master'.
```

Sekarang telah terdapat repo untuk menyimpan isi (post) dan kode-kode untuk membuat situs dengan Hugo.

## github action
Langkah terakhir adalah membangun suatu GitHub Action. Hal ini dapat dilakkan dengan mengakses <https://github.com/dudung/new-hugo-site-src/actions/new> dan pilih **set up a workflow yourself**. Dan ganti isi berkas 'main.yml' dengan 'hugo CI' [[2](#r02)]. Klik tombol **Start commit** dan lalu **Commit new file**. Berkas `./github/workflows/main.yml` telah berhasil dibuat.

### push something
Tulisan ini telah diubah sambil proses yang didokumentasikan dilakukan. Dicoba apakah update `new-hugo-site-src` akan menjalankan GitHub Action yang telah dibuat.

Masih gagal dan coba ganti

```
secrets.GITHUB_TOKEN
```

dengan

```
secrets.ACTIONS_DEPLOY_KEY
```

seperti di [[5](#r05)]. Sayangnya masih belum berhasil juga dan 

```
 Error: Action failed with "not found deploy key or tokens"
```

adalah pesan kesalahan yang diperoleh.


## notes
1. <a name='r01'></a>"Host on GitHub", Hugo, 2 Feb 2022, url <https://gohugo.io/hosting-and-deployment/hosting-on-github/> [20220319].
2. <a name='r02'></a>Carlos Pons, "Create and host a blog with Hugo and GitHub Pages in less than 30 minutes", my tech rahmblings, 21 Jun 2020, url <https://www.mytechramblings.com/posts/create-a-website-with-hugo-and-gh/> [20220319].
3. <a name='r03'></a>Ahmad Muhardian, "Cara Hosting/Deploy Hugo di Github", Petani Kode, 13 Mar 2022, url <https://www.petanikode.com/hugo-hosting-github/> [20220319].
4. <a name='r04'></a>Jia Fu Low, "Create gh-pages branch in existing repo", Github, 9 Jul 2020, url <https://jiafulow.github.io/blog/2020/07/09/create-gh-pages-branch-in-existing-repo/> [20220319].
5. <a name='r05'></a>Andrej Friesen, "gh-pages.yml", GitHub, 10 May 2021, url <https://github.com/ajfriesen/ajfriesen.com/blob/bc85030fc8307928efdfef0716bd94907254f7d1/.github/workflows/gh-pages.yml> [20220319].
