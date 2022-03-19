---
title: "create new site hugo"
date: 2022-03-18T21:10:00+07:00
lastmod: 2022-03-19T07:31:00+0700
author: viridi
draft: false
tags: ['hugo']
url: "0001"
---
Tulisan ini dibuat setelah instalasi Hugo [[1](#r01)] berhasil dilakukan. Proses membuat situs baru mengikuti informasi yang ada [[2](#r02)].


## version
Versi Hugo yang terinstal dapat diperoleh dengan cara berikut ini,

```batch
L:\home>hugo version
hugo v0.95.0-9F2E76AF windows/amd64 BuildDate=2022-03-16T14:20:19Z VendorInfo=gohugoio
```

yang memberikan informasi v0.95.0.


## create a new site
Suatu situs baru dibuat dengan cara berikut ini.

```batch
L:\home>hugo new site new-hugo-site
Congratulations! Your new Hugo site is created in L:\home\new-hugo-site.

Just a few more steps and you're ready to go:

1. Download a theme into the same-named folder.
   Choose a theme from https://themes.gohugo.io/ or
   create your own with the "hugo new theme <THEMENAME>" command.
2. Perhaps you want to add some content. You can add single files
   with "hugo new <SECTIONNAME>\<FILENAME>.<FORMAT>".
3. Start the built-in live server via "hugo server".

Visit https://gohugo.io/ for quickstart guide and full documentation.
```

Sebuah folder bernama `new-hugo-site` telah dibuat.

```batch
L:\home>tree /f new-hugo-site.
Folder PATH listing for volume Linux
Volume serial number is 00000000 XXXX:YYYY
L:\HOME\NEW-HUGO-SITE
│   config.toml
│
├───archetypes
│       default.md
│
├───content
├───data
├───layouts
├───static
└───themes
```

Isi dari folder tersebut adalah seperti di atas, yang diperoleh dengan perintah pada cmd Windows berupa `tree /f`.


## create a github repository
Akses akun GitHub dan buatlah repostori dengan nama `new-hugo-site` tanpa isi apapun.

Lalu kembali ke CLI untuk melakukan inisialisasi repositori.

```batch
$ git init
Initialized empty Git repository in L:/home/new-hugo-site/.git/

$ ls
archetypes/  config.toml  content/  data/  layouts/  static/  themes/
```

Tambahkan berkas-berkas yang dibuat oleh Hugo.

```batch
$ git add .
warning: LF will be replaced by CRLF in archetypes/default.md.
The file will have its original line endings in your working directory
warning: LF will be replaced by CRLF in config.toml.
The file will have its original line endings in your working directory
```

Berikan informasi commit yang dilakukan.

```batch
$ git commit -a -m "initial commit"
[master (root-commit) d8b1738] initial commit
 2 files changed, 9 insertions(+)
 create mode 100644 archetypes/default.md
 create mode 100644 config.toml
```

Tambahkan nama repositori remote dan url repositori tersebut. Lalu periksa keberadaannya.

```batch
$ git remote add origin https://github.com/dudung/new-hugo-site

$ git remote -v
origin  https://github.com/dudung/new-hugo-site (fetch)
origin  https://github.com/dudung/new-hugo-site (push)
```

Push berkas-berkas yang baru ditambahkan.

```batch
$ git push --set-upstream origin master
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 4 threads
Compressing objects: 100% (4/4), done.
Writing objects: 100% (5/5), 451 bytes | 150.00 KiB/s, done.
Total 5 (delta 0), reused 0 (delta 0), pack-reused 0
To https://github.com/dudung/new-hugo-site
 * [new branch]      master -> master
branch 'master' set up to track 'origin/master'.
```

Dengan demikian berkas-berkas awal yang dibuat Hugo telah tersimpan pada sebuah repositori GitHub bernama [new-hugo-site](https://github.com/dudung/new-hugo-site). Setelah ini semua berkas-berkas dapat diunggah ke repositori tersebut.


## unclear information
Ketidakpahaman mengenai GitHub membuat proses untuk mengetahui bagaimana agar berkas-berkas yang nantinya akan dibuat dengan bantuan Hugo dapat tersimpan di sana, cukup melelahkan. Proses membuat situs baru tidak menjelaskannya secara eksplisit [[2](#r02)]. Penambahan remote baru ke suatu repo GitHub hanya menjelaskan dengan menggunakan `git remote add [<options>] <name> <url>` [[3](#r03)], dan perlu dibuat terlebih dahulu reponya di GitHub tanpa isi [[4](#r04)], agar tidak muncul pesan kesalahan [[5](#r05)].

### echo >>
Untuk menambahkan theme ke site configuration digunakan [[2](#r02)]

```batch
echo theme = \"ananke\" >> config.toml
```

di mana dengan `cmd` akan menghasilkan dalam `config.toml` baris

```batch
theme = \"ananke\"
```

yang kemudian akan menghasilkan pesan kesalahan

```batch
Error: "L:\home\new-hugo-site\config.toml:4:9": unmarshal failed: toml: incomplete number
```

di mana hal ini disebabkan kelakuan berbeda pada `cmd` dan Git Bash, serta mungkin juga PowerShell [[6](#r06)].


## add a theme
Sebuah theme, yang dalam hal ini adalah Ananke, dapat ditambahkan dengan cara

```batch
$ git submodule add https://github.com/theNewDynamic/gohugo-theme-ananke.git themes/ananke
Cloning into 'L:/home/new-hugo-site/themes/ananke'...
remote: Enumerating objects: 2395, done.
remote: Counting objects: 100% (418/418), done.
remote: Compressing objects: 100% (224/224), done.
remote: Total 2395 (delta 200), reused 339 (delta 168), pack-reused 1977
Receiving objects: 100% (2395/2395), 4.44 MiB | 952.00 KiB/s, done.
Resolving deltas: 100% (1296/1296), done.
warning: LF will be replaced by CRLF in .gitmodules.
The file will have its original line endings in your working directory
```

dan kemudian dipush ke repo di GitHub

```batch
$ git add .gitmodules config.toml themes/ananke
warning: LF will be replaced by CRLF in .gitmodules.
The file will have its original line endings in your working directory

$ git commit -a -m "add ananke theme"
[master 475ee7e] add ananke theme
 2 files changed, 4 insertions(+)
 create mode 100644 .gitmodules
 create mode 160000 themes/ananke

$ git push
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 4 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (4/4), 476 bytes | 158.00 KiB/s, done.
Total 4 (delta 0), reused 0 (delta 0), pack-reused 0
To https://github.com/dudung/new-hugo-site
   d8b1738..475ee7e  master -> master
```

Dengan demikian berkas yang ada secara lokal telah sama dengan yang ada di remote.


## add new post
Tulisan baru atau post dapat ditambahkan dengan

```batch
hugo new post/new-post-name.md
```

yang akan membuat berkas `new-post-name.md` dalam folder `content/posts`. Untuk saat ini dua buah post telah dibuat di tempat lain dan pindahkan dengan Windows Explorer.

```batch
L:\home\new-hugo-site>tree content /f
Folder PATH listing for volume Linux
Volume serial number is XXXX-YYYY
L:\HOME\NEW-HUGO-SITE\CONTENT
└───posts
        create-new-site-hugo.md
        install-hugo-windows-10.md
```

Di atas adalah informasi mengenai kedua berkas post tersebut.

```batch
$ git add content/posts/

$ git commit -a -m "add two new posts"
[master 7af1be2] add two new posts
 2 files changed, 373 insertions(+)
 create mode 100644 content/posts/create-new-site-hugo.md
 create mode 100644 content/posts/install-hugo-windows-10.md

$ git push
Enumerating objects: 7, done.
Counting objects: 100% (7/7), done.
Delta compression using up to 4 threads
Compressing objects: 100% (5/5), done.
Writing objects: 100% (6/6), 7.08 KiB | 1.42 MiB/s, done.
Total 6 (delta 1), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To https://github.com/dudung/new-hugo-site
   475ee7e..7af1be2  master -> master
```

Update repo di Github pun telah dilakukan.


## run the server
Server Hugo dijalankan dengan

```batch
L:\home\new-hugo-site>hugo server -D
Start building sites …
hugo v0.95.0-9F2E76AF windows/amd64 BuildDate=2022-03-16T14:20:19Z VendorInfo=gohugoio
WARN 2022/03/19 06:10:28 found no layout file for "HTML" for kind "home": You should create a template file which matches Hugo Layouts Lookup Rules for this combination.
WARN 2022/03/19 06:10:28 found no layout file for "HTML" for kind "section": You should create a template file which matches Hugo Layouts Lookup Rules for this combination.
WARN 2022/03/19 06:10:28 found no layout file for "HTML" for kind "page": You should create a template file which matches Hugo Layouts Lookup Rules for this combination.
WARN 2022/03/19 06:10:28 found no layout file for "HTML" for kind "page": You should create a template file which matches Hugo Layouts Lookup Rules for this combination.
WARN 2022/03/19 06:10:28 found no layout file for "HTML" for kind "taxonomy": You should create a template file which matches Hugo Layouts Lookup Rules for this combination.
WARN 2022/03/19 06:10:28 found no layout file for "HTML" for kind "taxonomy": You should create a template file which matches Hugo Layouts Lookup Rules for this combination.

                   | EN
-------------------+-----
  Pages            |  4
  Paginator pages  |  0
  Non-page files   |  0
  Static files     |  0
  Processed images |  0
  Aliases          |  0
  Sitemaps         |  1
  Cleaned          |  0

Built in 98 ms
Watching for changes in L:\home\new-hugo-site\{archetypes,content,data,layouts,static}
Watching for config changes in L:\home\new-hugo-site\config.toml
Environment: "development"
Serving pages from memory
Running in Fast Render Mode. For full rebuilds on change: hugo server --disableFastRender
Web Server is available at http://localhost:1313/ (bind address 127.0.0.1)
Press Ctrl+C to stop
```

di mana `http://localhost:1313/` belum menampilkan apapun. Modifikasi `config.toml` dengan menambahkan baris

```batch
theme = "ananke"
```

yang pada `cmd` akan muncul pesan

```batch
Change of config file detected, rebuilding site.
2022-03-19 06:11:56.968 +0700
Rebuilt in 209 ms
```

dan refresh Google Chrome atau web browser lainnya yang digunakan untuk mengakses <http://localhost:1313/>.

### edit something
Saat mengubah sesuatu pada berkas dalam folder `new-hugo-site`, dalam hal ini dalam folder `content/posts` akan muncul pesan seperti

```batch
Change detected, rebuilding site.
2022-03-19 06:17:25.469 +0700
Source changed "L:\\home\\new-hugo-site\\content\\posts\\create-new-site-hugo.md": WRITE
Total in 63 ms
```

pada jendela **hugo - hugo server -D** yang menggambarkan seberapa cepat situs dibangun. Dan web browser tidak perlu direfresh karena akan secara otomatis terjadi.

### date format
Pada front matter dapat dituliskan

```markdown
date: "2022-03-18T21:10:00+07:00"
lastmod: "2022-03-19T06:24:00+0700"
```

dan pada `config.toml` dicantumkan 

```toml
[params]
	date_format = "Mon, 02 Jan 2006"
```

agar dapat mengatur format tanggal pada post [[7](#r07)]. Dengan theme Ananke yang belum dimodifikasi [[8](#r08)] informasi pada `lastmod` belum dapat dibaca. Untuk itu dapat ditambahkan baris

```toml
[frontmatter]
date = ["lastmod", "publishDate", "date"]
```

pada berkas `config.toml` sehingga informasi tanggal diambil dari `lastmod` [[9](#r09)].


## notes
1. <a name='r01'></a>Hugo Authors, "The world’s fastest framework for building websites", Hugo, url <https://gohugo.io/> [20220318].
2. <a name='r02'></a>"Quick Start", Hugo, url <https://gohugo.io/getting-started/quick-start/> [20220318].
3. <a name='r03'></a>Erika Kuntar, "How to Add a New Remote to your Git Repo", Assembla, 11 Mar 2022, url <https://articles.assembla.com/en/articles/1136998-how-to-add-a-new-remote-to-your-git-repo> [20220318].
4. <a name='r04'></a>Karl Broman, "Start a new git repository", git/github guide, url <https://kbroman.org/github_tutorial/pages/init.html> [20220318].
5. <a name='r05'></a>"Adding locally hosted code to GitHub", GitHub Docs, GitHub, Inc., 2022, url <https://docs.github.com/en/get-started/importing-your-projects-to-github/importing-source-code-to-github/adding-locally-hosted-code-to-github#adding-a-local-repository-to-github-with-github-cli> [20220318].
6. <a name='r06'></a>Chris, "Answer to 'Getting "unmarshal failed" when trying to create first website post in Hugo after installation'", Stack Overflow, 4 Apr 2021, url <https://stackoverflow.com/a/66944649/9475509> [20220319].
7. <a name='r07'></a>dudung, "Answer to 'How to render correct datetime in hugo post?'", Stack Overflow, 19 Mar 2022, url <https://stackoverflow.com/a/71534317/9475509> [20220319].
8. <a name='r08'></a>Ananke contributors (88), "Ananke, A theme for Hugo, a framework for building websites", Github, v2.8.1, 3 Feb 2022, url <https://github.com/theNewDynamic/gohugo-theme-ananke/releases/tag/v2.8.1> [20220319].
9. <a name='r09'></a>Andrew Stevens, "Last Modified Date with Hugo", 31 Mar 2021, url <https://www.andrewjstevens.com/posts/2021/03/last-modified-date-with-hugo/> [20220319].
