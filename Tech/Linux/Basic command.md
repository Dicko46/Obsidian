- "echo" perintah dasar di Linux/Unix yang berfungsi untuk **menampilkan teks atau output ke terminal/shell**. Perintah ini terutama digunakan untuk:
	- Menampilkan pesan ke layar
	- Menulis ke file
	- Menampilkan nilai variabel
	- Debugging skrip shell

```bash
echo Hello World # Menampilkan teks Hello World
echo "Hello, Future ME" > message.txt # Membuat message.txt dengan isi "Hello, Future Me"
echo "isi text" >> message.txt # Menambahkan text pada message.txt tanpa menghapus konten didalamnya
```

| Sequence | Arti                 | Contoh                               |
| -------- | -------------------- | ------------------------------------ |
| `\n`     | baris baru / newline | `echo -e "Line1\nLine2"`             |
| `\t`     | Tab horizontal       | `echo -e "Name:\tJohn"`              |
| `\\`     | Backslash            | `echo -e "Path: C:\\Users"`          |
| `\b`     | Backspace            | `echo -e "Hello\bWorld"` → HellWorld |
| `\r`     | Carriage return      | `echo -e "Loading\rDone"`            |
| `\a`     | Alert (bell)         | `echo -e "\a"` (bunyi beep)          |
| `\v`     | Tab vertikal         | `echo -e "Col1\vCol2"`               |
| `\0NNN`  | Karakter octal       | `echo -e "\0111"` (karakter 'o')     |
| `\xHH`   | Karakter hex         | `echo -e "\x48\x65"` (He)            |
- "mkdir" Perintah untuk membuat folder

```bash
mkdir example # Membuat folder baru dengan nama example pada directory saat ini.
```

- "cp" perintah untuk melakukan copy

```bash
cp /dir/namafile /dir/namafile # copy file
cp -a /dir/dir /dir/dir # copy directory source
cp -r dir dir # Copy directory dan memastikan semua content didalamnya tercopy
```

- `"ls"` perintah untuk menampilkan content suatu directory

```bash
ls ~ # Menampilkan isi directory home
ls -l # Menampilkan long listing directory
ls -a # Menampilkan semua file termasuk hidden file .file
ls -l dir # Menampilkan total file pada directory
ls -R # Menampilkan recursive listing
```

- `"rm"` Perintah untuk menghapus suatu file atau directory

```bash
rm namafile.txt # Menghapus namafile.txt
rm -i namafile.txt # Menghapus namafile.txt tapi sebelum itu menampilkan prompt confirmasi (y/n)
rmdir # Menghapus diretory kosong
rm -r dir # Menghapus directory dan isinya (tambahkan f untuk force)
```

- `"apropos"` perintah Linux yang digunakan untuk **mencari dokumentasi sistem (manual pages)** berdasarkan **kata kunci** atau **deskripsi**.

```bash
apropos copy # Menampilkan semua perintah yang deskripsinya mengandung kata "copy" (seperti `cp`, `rsync`, `dd`, dll.)

```

```ad-info
apropos sangat bergantung dengan mandb untuk menampilkan dokumentasi jadi bila apropos tidak menampilkan dokumentasi lakukan runnning mandb terlebih dahulu
```

|    **Opsi**     |                **Fungsi**                 |
| :-------------: | :---------------------------------------: |
|  -w / --exact   |    Mencocokkan kata kunci secara eksak    |
| -w / --wildcard | Menggunakan pola wildcard dalam pencarian |
|   -a / --and    |  Mengharuskan semua kata kunci ditemukan  |
|   -l / --long   |     Menampilkan output tanpa dipotong     |
| -s / --sections |     Mencari di bagian manual tertentu     |
- "echo "Hello LabEx" " Perintah untuk print "Hello Labex"
- "whoami" perintah untuk menampilkan user saat ini
- "id" menampilkan grops dan permission user saat ini
- "id root" menampilkan groups dan permission user root (root bisa dirubah ke user lain)

```ad-hint
  uid=5000(labex) gid=5000(labex) groups=5000(labex),27(sudo),121(ssl-cert),5002(public)

  ```
  
```ad-info
uid : Your User ID (a unique numerical identifier).
gid: Your primary Group ID.
groups: All the groups you are a member of.
```

- "pwd" Perintah untuk menampilkan directory saat ini
- "touch" Perintah untuk membuat empty file.

```bash
touch list.txt # Membuat file kosong bernama list.txt
```

