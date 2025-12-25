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
