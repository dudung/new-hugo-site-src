---
title: "install hugo windows 10"
date: 2022-03-18T18:45:00Z
lastmod: 2022-03-18T21:10:00+07:00
author: viridi
draft: false
tags: ['hugo', 'install', 'windows']
url: "0000"
---
Tulisan ini dibuat sebelum instalasi Hugo [[1](#r01)] dilakukan, sehingga untuk melihat hasilnya saat disunting menggunakan Notepad++ [[2](#r02)] digunakan Markdown Viewer [[3](#r03)] pada Google Chrome [[4](#r04)]. Proses instalasi Hugo dilakukan mengikuti langkah-langkah yang diberikan untuk sistem operasi Windows [[5](#r05)]. Saat ini digunakan sistem operasi Microsoft Windows 10 Home versi 10.0.19042 Build 19042.


## download
Program Hugo yang dapat dijalankan (exe) dan terimpan dalam berkas terkompresi (zip) dapat diperoleh dari halaman [Hugo Releases](https://github.com/gohugoio/hugo/releases). Versi terakhir adalah v0.95.0 yang dirilis pada 16 Maret 20220 atau dua hari yang lalu saat bagian ini dituliskan. Berkas yang dipilih adalah [hugo_0.95.0_Windows-64bit.zip](https://github.com/gohugoio/hugo/releases/download/v0.95.0/hugo_0.95.0_Windows-64bit.zip) dengan ukuran 15.5 MB. Unduh dan simpan pada tempat instalasi yang diinginkan dalam komputer yang digunakan.


## install
Dengan menggunakan Windows Explorer ikon `hugo_0.95.0_Windows-64bit.zip` dapat diklik dan dilihat isinya yang terdiri dari tiga berkas sebagai berikut.

Name | Type | Compressed size
:- | :- | :-
hugo.exe | Application | 15,828 KB
LICENSE | File | 4 KB
README.md | MD File | 5 KB

Salin berkas-berkas di atas ke folder `C:\Hugo\bin`. Ukuran ketiga berkas menjadi lebih besar setelah disalin ke folder tujuan.

Name | Type | Size
:- | :- | :-
hugo.exe | Application | 49,832 KB
LICENSE | File | 12 KB
README.md | MD File | 11 KB

Selain dengan cara di atas dapat juga dilakukan klik kanan pada `hugo_0.95.0_Windows-64bit.zip` untuk melakukan proses ekstraksi.

```batch
C:\>dir /s  C:\Hugo
 Volume in drive C is Windows
 Volume Serial Number is XXXX-YYYY

 Directory of C:\Hugo

2022-03-18  07:36 PM    <DIR>          .
2022-03-18  07:36 PM    <DIR>          ..
2022-03-18  07:36 PM    <DIR>          bin
               0 File(s)              0 bytes

 Directory of C:\Hugo\bin

2022-03-18  07:36 PM    <DIR>          .
2022-03-18  07:36 PM    <DIR>          ..
2022-03-16  02:35 PM        51,027,456 hugo.exe
2022-03-16  02:14 PM            11,357 LICENSE
2022-03-16  02:14 PM            10,423 README.md
               3 File(s)     51,049,236 bytes

     Total Files Listed:
               3 File(s)     51,049,236 bytes
               5 Dir(s)  76,478,054,400 bytes free
```

Informasi di atas memastikan bahwa Hugo telah tersimpan pada folder `C:\Hugo\bin`.


## setup
Langkah berikutnya adalah menambahkan Hugo ke setting Windows PATH. Untuk pengguna Windows 10 caranya adalah seperti berikut ini [[5](#r05)].
+ Klik kanan pada tombol **Start**.
+ Pilih **Sistem** dan akan terbukan jendela **Settings**.
+ Pilih **Advanced system settings** di sebelah kanan setelah gulung layar ke bawah. Akan terbuka jendela **System Properties**.
+ Pilih tombol **Environment Variables..** di bagian bawah.
+ Sorot baris dengan label **Path** dan klik tombol **Edit..**.
+ Tekan tombol **Browse..** dan navigasi ke folder instalasi Hugo, yaitu `C:\Hugo\bin`. Akan muncul pada baris lokasi folder tersebut.
+ Tekan tombol **OK** dan akan kembali ke jendela sebelumnya dan pada baris dengan label **Path** isinya telah diawali dengan folder tempat instalasi Hugo.
+ Tekan tombol **OK** untuk selesai dan menutup jendela **Enviroment Variables**.
+ Tekan tombol **OK** untuk selesai dan menutup jendela **System Properties**.
+ Tampilan akan kembali ke jendela **Settings** yang dapat ditutup dengan menekan ikon &times; pada sudut kanan atas.


## check
Untuk memeriksa apakah Hugo dapat dijalankan lakukan langkah-langkah berikut ini.
+ Navigasi ke folder untuk menyimpan berkas-berkas situs yang akan dibuat dengan Hugo. Di sini digunakan 'L:\home' yang merupakan instalasi Linux menggunakan Cygwin [[6](#r06)]. Cara yang umum adalah melakukan navigasi ke folder `C:\Hugo`.
+ Klik kanan pada tempat kosong dan pilih **New** > **Shortcut**.
+ Jendela **Create Shortcut** akan terbuka. Tidak perlu menekan tombol **Browse..**, cukup isikan `cmd` pada kolom yang tersedia, lalu tekan tombol **Next**.
+ Ganti nama `cmd.exe` dengan `hugo` dan akhiri dengan menekan tombol **Finish**.
+ Akan muncul ikon `Hugo` di dalam folder `L:\home`. Klik kanan icon tersebut dan pilih **Properties**, yang akan membuak jendela **hugo Properties**.
+ Terdapat isi pada baris **Start in:** berupa `C:\WINDOWS\system32`. Hapus isi tersebut.
+ Tekan tombol **OK** untuk selesai dan menutup jendela **hugo Properties**.
+ Klik pada ikon `hugo`, yang merupakan suatu shortcut sehingga dapat disalin dan ditempelkan pada folder apapun yang diingikan, akan terbuka jendela cmd dengan nama **hugo**.
+ Ketik `hugo help` dan tekan tombol enter pada keyboard.

```batch
L:\home>hugo help
hugo is the main command, used to build your Hugo site.

Hugo is a Fast and Flexible Static Site Generator
built with love by spf13 and friends in Go.

Complete documentation is available at http://gohugo.io/.

Usage:
  hugo [flags]
  hugo [command]

Available Commands:
  completion  Generate the autocompletion script for the specified shell
  config      Print the site configuration
  convert     Convert your content to different formats
  deploy      Deploy your site to a Cloud provider.
  env         Print Hugo version and environment info
  gen         A collection of several useful generators.
  help        Help about any command
  import      Import your site from others.
  list        Listing out various types of content
  mod         Various Hugo Modules helpers.
  new         Create new content for your site
  server      A high performance webserver
  version     Print the version number of Hugo

Flags:
  -b, --baseURL string             hostname (and path) to the root, e.g. http://spf13.com/
  -D, --buildDrafts                include content marked as draft
  -E, --buildExpired               include expired content
  -F, --buildFuture                include content with publishdate in the future
      --cacheDir string            filesystem path to cache directory. Defaults: $TMPDIR/hugo_cache/
      --cleanDestinationDir        remove files from destination not found in static directories
      --config string              config file (default is path/config.yaml|json|toml)
      --configDir string           config dir (default "config")
  -c, --contentDir string          filesystem path to content directory
      --debug                      debug output
  -d, --destination string         filesystem path to write files to
      --disableKinds strings       disable different kind of pages (home, RSS etc.)
      --enableGitInfo              add Git revision, date, author, and CODEOWNERS info to the pages
  -e, --environment string         build environment
      --forceSyncStatic            copy all files when static is changed.
      --gc                         enable to run some cleanup tasks (remove unused cache files) after the build
  -h, --help                       help for hugo
      --ignoreCache                ignores the cache directory
      --ignoreVendorPaths string   ignores any _vendor for module paths matching the given Glob pattern
  -l, --layoutDir string           filesystem path to layout directory
      --log                        enable Logging
      --logFile string             log File path (if set, logging enabled automatically)
      --minify                     minify any supported output format (HTML, XML etc.)
      --noChmod                    don't sync permission mode of files
      --noTimes                    don't sync modification time of files
      --panicOnWarning             panic on first WARNING log
      --poll string                set this to a poll interval, e.g --poll 700ms, to use a poll based approach to watch for file system changes
      --printI18nWarnings          print missing translations
      --printMemoryUsage           print memory usage to screen at intervals
      --printPathWarnings          print warnings on duplicate target paths etc.
      --printUnusedTemplates       print warnings on unused templates.
      --quiet                      build in quiet mode
      --renderToMemory             render to memory (only useful for benchmark testing)
  -s, --source string              filesystem path to read files relative from
      --templateMetrics            display metrics about template executions
      --templateMetricsHints       calculate some improvement hints when combined with --templateMetrics
  -t, --theme strings              themes to use (located in /themes/THEMENAME/)
      --themesDir string           filesystem path to themes directory
      --trace file                 write trace to file (not useful in general)
  -v, --verbose                    verbose output
      --verboseLog                 verbose logging
  -w, --watch                      watch filesystem for changes and recreate as needed

Use "hugo [command] --help" for more information about a command.

L:\home>
```

Informasi di atas menggambarkan bahwa setup Hugo telah berhasil. Baris terakhir `L:\home>` menandakan folder yang tempat `cmd` dijalankan. Bila menggunakan folder `C:\Hugo` akan tampak menjadi `C:\Hugo>`.


## notes
1. <a name='r01'></a>Hugo Authors, "The world’s fastest framework for building websites", Hugo, url <https://gohugo.io/> [20220318].
2. <a name='r02'></a>Don Ho, "What is Notepad++", url <https://notepad-plus-plus.org/> [20220318].
3. <a name='r03'></a>Simeon Velichkov, "Markdown Viewer",  Chrome web Store, version 4.0, 24 Dec 2020, url <https://chrome.google.com/webstore/detail/ckkdlimhmcjmikdlpkmbgfkaikojcbjk> [20220318].
4. <a name='r04'></a>"Der Browser von Google", Google, url <https://www.google.com/intl/de/chrome/> [20220318].
5. <a name='r04'></a>"Install Hugo", Hugo, url <https://gohugo.io/getting-started/installing> [20220318]. 
5. <a name='r04'></a>Cygwin authors, "This is the home of the Cygwin project", Cygwin, url <https://www.cygwin.com/> [20220318].
