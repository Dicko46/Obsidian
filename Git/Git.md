# 1. Cara membuat repository git

Pertama buat repo terlebih dahulu di folder yang sudah ditentukan

```bash
git init
```

Masukkan username dan email github (global/local)

```bash
git config --global user.email "example@example.com" # Membuat useremail secara global
git config --global user.name "Dicko46" # Membuat username secara global
git config --local user.email "example@example.com" # Membuat useremail secara local
git config --local user.name "Dicko46" # Membuat username secara local
git config --global --list # Menampilkan semua username/useremail pada global
git config --local --list # Menampilkan semua username/useremail pada local
```

Merubah warna ui git secara menyeluruh dengan otomatis

```bash
git config --global color.ui auto
```

Set code editor default git

```bash
git config --global core.editor nano
```

Menyinkronkan timeline

```bash
git config --global core.autocrlf input
```

Menambahkan alias

```bash
git config --global alias.st status # Membuat alias st untuk status
git st # menjalankan hasil alias diatas
git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"
```

Lihat status git

```bash
git status
```

```ad-info
diecko46@codesaya:/code$ git status

on branch master  
Initial commit  
  
Untracked files:  # Ini menujukkan bahwa index.php tidak masuk dalam repo
(use "git add <file>..." to include in what will be committed)  
  
index.php  
  
nothing added to commit but untracked files present (use "git add" to track)
```

Index php (Untracked files) masuk dalam kategori modified dan belumm masuk ke fase staged, jadi untuk masuk ke fase selanjutnya lakukan :

```bash
git add index.php # Menambahkan index.php ke staged
```

Untuk unstage file

```bash
git restore --staged namafile
git rm --cached namafile
```

setelah melakukan ini, index.php akan menjadi newfile dan sudah masuk fase staged.
Selanjutnya adalah menambahkan commit (Pesan penanda) pada code yang sudah dibuat (staged)

```bash
git commit -m "commit"
```

untuk cek log commit (save point)

```bash
git log # menampilkan semua log
git log --author='authorname' # Menampilkan log dari author tertentu
git log --oneline # Menampilkan log secara singkat
git log namafile # Untuk melihat commit apa saja yang sudah dirubah didalam file tersebut
```

untuk melihat perubahan pada file

```bash
git diff # melihat perubahan secara global
git diff --staged # Melihat perubahan pada staged
git diff namafile # Melihan perubahan sesuai nama file
```

Jika revisi anda belum staged ataupun committed, anda bisa mengembalikannya menggunakan 
```bash
git checkout nama_file.html
```

jika revisi anda sudah masuk staged, anda bisa membuatnya menjadi modified dengan cara `git reset nama_file.html` dan setelahnya anda bisa lakukan `git checkout nama_file.html`.

Mengembalikan file commit sebelumnya

```bash
git checkout HEAD-3 namafile.php # Mengembalikan file 3 commit sebelumnya
git revert nomorcommit -n # Merubah semuam file ke nomor commit tertentu (Dan semua file tersebut memiliki status staged. Jika anda tidak menggunakan `-n`, maka semua file tersebut statusnya langsung jadi committed)
```

Untuk menambahkan cabang

```bash
git branch namacabang
git checkout namacabang # Untuk pindah ke cabang
```

Untuk menggabungkan cabang ke master

```bash
git merge namabranch # sebelumnya pindah dulu ke master baru merge
```

Untuk menambahkan repo remote

```shell
git remote add nama 'url github'
git remote -v # check repo tersedia
git remote rename namalama namabaru # untuk rename nama repo
git remote rm nama # untuk hapus repo
```

Mengambil commit dari repo

```bash
git pull namarepo namabranch
```

Mengimpor semua commit dari repo

```bash
git fetch namarepo
git log namarepo/namabranch # untuk cek log commit
git merge bendera/master #untuk merge cabang repo lokal ke remote
```

Untuk upload ke repo

```bash
git push namarepo namabranch # cara terbaik untuk push adalah menggunakan ssh
```

Untuk cloning

```bash
git clone urlgithhub
```

cara membuat keyssh

```bash
ssh-keygen -t ed25519 -C "dickorahmansyah@gmail.com"
```

Untuk contribute repo orang lain :
1. Clone repo tersebut
2. buat branch baru agar tidak conflict
3. setelah data selesai pergi ke repo fork
4. masuk ke branch baru
5. pilih opsi pull request

Untuk memunculkan dokumentasi command

```bash
git command --help
git --help
```
