## 1. Memindahkan file / folder

```bash
sudo cp -r -v FileCentipede /opt
```

```bash
sudo mv -r -v FileCentipede /opt
```

```bash
mv dokumen.txt /home/dicko/Documents/
```

📋 Penjelasan:
- `sudo` → Menjalankan dengan hak akses root (karena `/opt` butuh izin admin).
- `cp` → Perintah untuk menyalin file atau folder.
- `mv` → Perintah untuk memindahkan file atau folder
- `-r` → Recursive, agar seluruh isi folder ikut disalin.
- `-v` → Verbose, menampilkan proses penyalinan.  
- `FileCentipede` → Folder sumber di direktori saat ini.
- `dokumen.txt` → Filw sumber di direktori saat ini.
- `/opt` → Tujuan penyalinan.
- `cat -n` → Digunakan untuk print text pada terminal dengan line number
- `cat -n1` → Digunakan untuk print text pada terminal dengan line number pertama
- `head -c1` → Digunakan untuk print text pada terminal dengan hanya character pertama saja
- `diff file1 file2` → Menampilkan perbedaan isi dalam 2 file tersebut
- `diff -r ~/Desktop ~/Code` → Menampilkan perbedaan antara subdirectory

- You used `cat` to view the entire contents of a file.
- You learned how to use `cat -n` to view file contents with line numbers.
- You used `head` to view the beginning of a file, both by lines and by bytes.
- You used `tail` to view the end of a file, both by lines and by bytes.
- You learned how to use `diff` to compare the contents of files.
- Finally, you used `diff -r` to compare entire directories.