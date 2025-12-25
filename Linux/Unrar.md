## 1. Cara menggunakan unrar dengan terminal
- Extract file dengan mempertahankan struktur folder asli (direkomendasikan untuk file dengan subfolder)

 ```bash
 unrar -x file.rar # gunakan -p untuk password
 ```

- Extract semua file ke folder saat ini tanpa struktur folder (lebih sederhana untuk file tunggal)

```bash
unrar -e file.rar # gunakan -p untuk password
```

- Lihat isi file RAR tanpa extract (untuk cek dulu)

```bash
unrar l file.rar
```
