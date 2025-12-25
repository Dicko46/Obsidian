## 1. Download .Deb files
---
Download files deb dan buat folder yang sesuai dengan package yang akan diinstal

```ad-hint
1. freedownloadmanager.deb
2. buat folder dengan nama **freedownloadmanager** agar mudah dipahami
```

## 2. Extract files Deb kedalam folder yang sudah dibuat
---

```bash
cd freedownloadmanager
ar x ../freedownloadmanager.deb
```

Penjelasan rincinya:

- `ar` adalah singkatan dari "archiver," sebuah utilitas command line di Linux untuk membuat, memodifikasi, dan mengekstrak arsip berformat .ar, yang juga digunakan sebagai format pembungkus paket Debian (.deb).
- `x` adalah opsi untuk `ar` yang berarti "extract" atau mengekstrak semua isi file arsip.
- `../freedownloadmanager.deb` menunjukkan file paket Debian yang akan diekstrak, dalam hal ini file bernama freedownloadmanager.deb yang berada di direktori induk (`..`) dari lokasi terminal saat ini.

```ad-note
ar x ../freedownloadmanager.deb # berarti file deb yang akan diinstal berada di luar folder sebelum "freedownload" jadi kita menggunakan ".." pada eksekusinya
```

## 3. Extract hasil dari deb files ke folder yang sesuai
---
![[Pasted image 20251104222604.png]]

```ad-note
Pada gambar diatas menghasilkan 3 files yaitu control.tar.xz data.tar.xz dan debian-binary
```

![[Pasted image 20251104223232.png]]
```ad-note
Pada gambar diatas didapatkan data pada folder /etc, /opt, dan /usr yang semua folder tersebut terletak pada directory /
```

jadi selanjutnya yang dilakukan adalah mengekstract file diatas sesuai directory dengan menggunakan command

```bash
sudo tar -xvJf data.tar.xz -C /
```

Yang fungsinya:

- `sudo`: Menjalankan perintah dengan hak akses administrator (root), karena ekstraksi akan dilakukan ke direktori root `/` yang butuh izin khusus.
- `tar`: Perintah untuk mengelola arsip file (.tar).
- `-x`: Opsi untuk mengekstrak (extract) isi arsip.
- `-v`: Opsi verbose, menampilkan proses file yang sedang diekstrak secara rinci di terminal.
- `-J`: Opsi untuk mengekstrak file yang dikompresi dengan `xz` (format kompresi `.xz`).
- `-f data.tar.xz`: Menentukan nama file arsip yang akan diekstrak, yaitu `data.tar.xz`.
- `-C /`: Menentukan target direktori tujuan ekstraksi, yaitu ke direktori root `/`.

Jadi, perintah ini mengekstrak isi arsip `data.tar.xz` yang dikompresi dengan `xz` ke direktori root `/`, dengan menampilkan file-file yang sedang diekstrak, menggunakan hak akses administrator supaya dapat menulis ke direktori sistem.

```bash
sudo update-desktop-database
```

Perintah `sudo update-desktop-database` berfungsi untuk memperbarui database cache yang berisi informasi tentang tipe MIME yang didukung oleh file desktop (*.desktop) di Linux. File desktop ini biasanya berisi informasi tentang aplikasi dan jenis file yang bisa dibuka oleh aplikasi tersebut.

#debinstall #tar

