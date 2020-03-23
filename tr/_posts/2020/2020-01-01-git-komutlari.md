---
layout: post
title: "Git Komutları"
date: 2020-01-02 02:38:19 Thursday
author: semih
comments: true
lang: tr
lang-ref: git-commands
categories: [git]
tags: [git, source control management, scm]
---
Yazılan koddaki satır sayısı arttıkça kodu yönetmek zorlaşır. Bu nedenle bazı ihtiyaçlar ortaya çıkmıştır. Bu ihtiyaçlardan biri depolama, diğeri versiyonlamadır. Depolama, kodların bir veya birden fazla sunucuda, herhangi bir yerde saklanması işlemidir. Versiyonlama ise kodun geçirdiği evrimi bize anlatır. Bu yüzden yazılımcılar daha önceden yapılan geliştirmeleri görebilmek ve yeni yaptıkları geliştirmeleri etiketleyebilmek için sürüm kontrol ve kaynak kod yönetimi araçlarına ihtiyaç duymuşlardır.

Git, SubVersion, CVS, TFS, ClearCase, Mercurial gibi sürüm kontrol kaynak kod yönetim (SCM) araçları da zamanla ortaya çıkmış olup günümüzde kullanılmaktadır. Bu yazıda bu araçlardan biri olan Git'ten bahsedeceğiz. Git, modern dağıtık bir sürüm kontrol sistemidir. En yararlı Git komutlarını ve neden bu komutları kullanmamız gerektiğini anlatacağım. Örneklerdeki her adımı açıklayacağım.
<br/>

Git'te 3 durum vardır:
- Working directory (Çalışma alanı)
- Staging area (Bekleme alanı)
- Commit (İşletim alanı)

<br/>
![Temel Git İş Akışı Yaşam Döngüsü](/assets/images/basic-git-workflow-lifecycle.png)

<br/>
### Konfigürasyon
Bilgisayarda Git yüklüyse kullanıcı adı, email, sürüm bilgilerini öğrenmek ve güncellemek için aşağıdaki komutları çalıştırırız.

```shell
~ $ git version
   git version 2.17.2
```
git global kullanıcı adı ve e-posta konfigürasyonu
```shell
~ $ git config --global user.name "username"
~ $ git config --global user.email "email"
~ $ git config --global --list
```
<br/>
### Örnek Uygulama
Şimdi örnek bir uygulama yapalım ve git ile ilk komutlarımızı çalıştıralım. Öncelikle Github'da "github-repo" ismiyle yeni bir repository oluşturalım. Ardından oluşuturduğumuz bu repository'yi bilgisayarımızda herhangi bir yerde oluşuturduğumuz bir workspace klasörü içine klonlayalım.

Uzak repository'yi bilgisayarındaki bir(workspace) klasöre klonla.
```shell
~ $ git clone https://github.com/semih/github-demo.git
~ $ cd github-demo/
```
READMED.md dosyası ekle ve commitle.
```shell
~ $ git init
~ $ git add README.md
~ $ git commit -m "first commit"
```

Uzak branch'e yeni eklediğin veya uzak branch'te değiştirdiğin dosyaları push et, yani gönder.
```shell
~ $ git remote add origin https://github.com/semih/github-demo.git
~ $ git push -u origin master
```

Bir dosya oluşturduk ve içine bir şeyler yazdık. `git status` komutunu kullanarak, çalıştığımız branch üstünde working directory, staging area, local repository ve remote repository arasında herhangi bir fark olup olmadığını göreceğiz. Takip etmek için `git add <file>...` komutunu kullanabiliriz.
```shell
~ $ echo "Test Git Quick Start Demo" >> start.txt
~ $ ls
.git		README.md	start.txt
~ $ cat start.txt
Test Git Quick Start Demo
~ $ git status
On branch master
Your branch is up to date with 'origin/master'.
Untracked files:
  (use "git add <file>..." to include in what will be committed)
	start.txt
nothing added to commit but untracked files present (use "git add" to track)
```

`git add <file>...`  komutunu çalıştırdığımızda, Git bize staging area'da yeni bir dosya olduğunu söyler. "Changes to be commited" uyarısı ile commit edilmemiş dosya olduğu anlaşılır. Bu dosya staging area'da commit edilmek üzere bekler.
```shell
~ $ git add start.txt 
~ $ git status
On branch master
Your branch is up to date with 'origin/master'.
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)
	new file:   start.txt
```

`git commit` komutunu çalıştırıp durumu tekrar kontrol ediyoruz. 
Sonuç olarak, yeni dosya staging area'dan local repository'ye taşındı. Bekleyen başka değişiklik olmadığından Git, çalışma dizinini temiz olarak işaretler. Ancak dosyamız henüz Github'da değil.
```shell
~ $ git add .
~ $ git commit -m "git-commands"
[master 2cd0af0] git-commands
 1 file changed, 1 insertion(+)
 create mode 100644 start.txt
~ $ git status
On branch master
Your branch is up to date with 'origin/master'.
nothing to commit, working tree clean
```

Yapmamız gereken son bir adım var ve bu da push etme işlemi. `git push origin master` komutunuyla değişiklikleri push ederiz. "origin", depomuzun Github kopyasını ifade eder. "master", depodaki branch adını ifade eder. Her şeyi doğru şekilde yaptıysak yeni dosya, repository'mizin Github kopyasında olmalıdır.
```shell
~ $ git push origin master
Counting objects: 3, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 299 bytes | 299.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To https://github.com/semih/github-demo.git
   785389b..2cd0af0  master -> master
```
<br/>
### Başlıca Git Komutları
- Yeni Bir Proje Başlangıcı
	- Sıfırdan (Henüz hiç kodu olmayan)
	- Localinde Kodu Olan
	- Github Projesi (fork ve clone)
- Temel İş Akışı (add, commit, push, pull)
- Dosyalarla Çalışmak (rename, move & delete)
- Git Tarihçe ve Takma Adlar
- Gönderilmek İstenmeyen Dosyalar

<br/>
#### Yeni Bir Proje Başlangıcı (Sıfırdan)
"git init" komutuyla yeni bir proje oluştur.
```shell
workspace $ git init fresh-project
Initialized empty Git repository in /Users/semih/workspace/fresh-project/.git/
workspace $ ls
fresh-project
workspace $cd fresh-project/
fresh-project $ ls -al
total 0
drwxr-xr-x  3 semih  staff   96  7 Oca 00:58 .
drwxr-xr-x  6 semih  staff  192  7 Oca 00:58 ..
drwxr-xr-x  9 semih  staff  288  7 Oca 00:58 .git
fresh-project $cd .git/
.git $ls
HEAD		description	info		refs
config		hooks		objects
```

`git status` komutu bize master branch'inde olduğumuzu söyler.
```shell
.git $ cd ..
fresh-project $ git status
On branch master
No commits yet
nothing to commit (create/copy files and use "git add" to track)
```

Git, izlenmeyen dosyaları yakalar.
```shell
fresh-project $ mate hipster.txt
fresh-project $ git status
On branch master
No commits yet
Untracked files:
  (use "git add <file>..." to include in what will be committed)
	hipster.txt
nothing added to commit but untracked files present (use "git add" to track)
```

Changes to be commited (yapılan değişiklikler) bu yeni dosya ("hipster.txt") anlamına gelir ve artık Git staging alanındadır. Commit edilmeyi bekleyen bir dosyamız vardır, ancak henüz işlenmemiştir.
```shell
fresh-project $ git add hipster.txt 
fresh-project $ git status
On branch master
No commits yet
Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
	new file:   hipster.txt
```

Yalnızca `git commit` yazarsak editör commit edilen değişiklikleri listeler ve dosyanın üst satırlarına commit mesajını yazıp kaydedebilirim.
```shell
fresh-project $ git commit (file is opening here with our default text editor)
[master (root-commit) 2296291] Adding new file
 1 file changed, 1 insertion(+)
 create mode 100644 hipster.txt
fresh-project $ git status
On branch master
nothing to commit, working tree clean
```
<br/>
#### Yeni Bir Proje Başlangıcı (Localinde Kodu Olan)
Proje klasöründeyken `git init` komutunu çalıştırırız. Her şeyden önce izlenmeyen dosyaları görürüz. `git add .` komutu dosyaları staging area'ya gönderir. `git commit` komutu kullanarak onları commit ederiz ve `git push` komutu kullanarak da push ederiz.
```shell
project-folder $ git init
Initialized empty Git repository in /Users/semih/workspace/initializr/.git/
project-folder $ git status
On branch master
No commits yet
Untracked files:
  (use "git add <file>..." to include in what will be committed)
	.htaccess
	404.html
	apple-touch-icon.png
	browserconfig.xml
	crossdomain.xml
	css/
	favicon.ico
	fonts/
	humans.txt
	index.html
	js/
	robots.txt
	tile-wide.png
	tile.png
nothing added to commit but untracked files present (use "git add" to track)
project-folder $ git add .
project-folder $ git commit -m "my first commit message"
```
<br/>
#### Yeni Bir Proje Başlangıcı (fork ve clone)
Bu bölüm, Github'da varolan bir projeye nasıl katkıda bulunulacağıyla ilgilidir.
Github sayfasında (https://github.com/scm-ninja/starter-web) Fork butonuna tıklanır.
Son olarak, `git clone` komutu çalıştırılır.

```shell
~ $ git clone https://github.com/semih/starter-web.git
Cloning into 'starter-web'...
remote: Enumerating objects: 39, done.
remote: Total 39 (delta 0), reused 0 (delta 0), pack-reused 39
Unpacking objects: 100% (39/39), done.
~ $ cd starter-web
starter-web $ 
starter-web $ ls
404.html				fonts
README.md				humans.txt
apple-touch-icon-precomposed.png	index.html
crossdomain.xml				js
css					robots.txt
favicon.ico				simple.html
```
<br/>
#### Temel İş Akışı (dosyayla çalışma)
* `git add -A`
* `git add -U`

<br/>
#### Temel İş Akışı (dosyayı bırakma)
Bilindiği üzere, git add komutu kullanarak dosyaları staging area'ya taşırız. Bazen bu dosyaları gerçekten taşımak istemeyiz veya yanlışlıkla taşımış olabiliriz. Bütün ihtiyacımız olan şey `git reset HEAD <file>...` komutunu çalıştırmak ve dosyaların unstage olmasını sağlamak. Bunun yanında `git checkout -- <file>...` komutu working directory'yi temizler ve değişiklikleri iptal eder.

<br/>
#### Dosyalarla Çalışmak (dosya silme)
`git rm <file>...`
`git reset HEAD <file>...` ve `git checkout -- <file>...` komutlarını sırasıyla kullanarak, silinen dosyaları geri alabiliriz.

<br/>
#### Dosyalarla Çalışmak (klasör silme)
`git rm -rf <folder>...`

<br/>
> İzlenmemiş, stage(stage'e alınmış) ve unstage(stage'e alınmamış) değişiklikler arasındaki farklar özetle: 
- İzlenmemiş değişiklikler Git'te değildir. 
- Stage'e alınmamış değişiklikler Git'te ancak commit için işaretlenmemiş. 
- Stage'e alınmış değişiklikler ise Git'te ve commit için işaretlenmiştir.

<br/>
#### Git Tarihçe
* `git help log`
* `git log`
* `git log --abbrev-commit`
* `git log --oneline --graph --decorate`
* `git log --all --graph --decorate --oneline`
* `git log --since="3 days ago"`
* `git log -- <file>`
* `git log --follow -- <file>`

<br/>
#### Git Takma Adlar
Bu komutu çalıştırdıktan sonra `git hist` kısayolu kullanılır.
`git config --global alias.hist "log --all --graph --decorate --oneline"`
Kısayollar .gitconfig dosyasından kontrol edilebilir.

`mate ~/.gitconfig`
<br/>
#### Gönderilmek İstenmeyen Dosyalar ve Klasörler
.DS Store gibi bazı dosyaları göndermek istemiyoruz. `ls -al` komutu nokta dosyaları ve klasörler dahil tüm dosyaları listeler. Bunun için ".gitignore" dosyası yaratmalıyız. `mate .gitignore` komutuyla oluşturabilir ve kaydedebiliriz. Yine bu dosyaya .DS_Store yazmamız gerekiyor. Daha sonra `git add .gitignore` komutuyla ekliyoruz.

.gitignore dosyasında * ifadesini kullanabiliriz. Örneğin, .log uzantılı log dosyalarımız olabilir. Bu dosyaları push etmek istemiyorsak, * .log deyimiyle hariç tutabiliriz veya workspace'te log klasörümüz olduğunda ve log klasörüne herhangi bir dosya göndermek istemediğimizde, doğrudan .gitignore dosyasına `log /` satırı eklemeliyiz. Aşağıdaki komutları çalıştırdıktan sonra, log klasörünün push edilmediği(aktarılmadığı) görülür.

* `git add .`
* `git status`
* `git commit -am "Excluding log file directory"`


[Kaynağı İndir](/assets/files/BasicWorkflow.pdf)<br/>
Bu yazıyı beğendiyseniz lütfen yorum bırakın! <br/>
Bir sonraki yazıda görüşmek üzere...
