Cara paling aman untuk menguji Snapper adalah dengan menghapus file yang **terlihat penting bagi sistem** tetapi sebenarnya bisa dibuat ulang atau tidak menyebabkan komputer mati total (gagal boot) saat itu juga.

Berikut adalah beberapa skenario pengujian dari yang paling aman hingga yang sedikit "menantang":

---

### 1. Level Aman: Menghapus File di `/etc/` yang Spesifik

Daripada menghapus seluruh folder `/etc`, cobalah hapus satu file konfigurasi yang akan langsung terasa dampaknya jika hilang.

- **Target:** `/etc/hostname` (File ini berisi nama komputer kamu).
    
- **Cara Uji:**
    
    1. Cek nama komputermu sekarang: `hostname`.
        
    2. Buat snapshot manual: `sudo snapper create -d "Sebelum hapus hostname"`.
        
    3. Hapus filenya: `sudo rm /etc/hostname`.
        
    4. Coba jalankan perintah `hostname` lagi atau buka terminal baru. Biasanya akan muncul pesan error atau nama "localhost".
        
    5. **Restore:** Jalankan `sudo snapper rollback <nomor_snapshot>` atau gunakan `snapper undochange`.
        
    6. Cek kembali: File `/etc/hostname` akan muncul lagi.
        

### 2. Level Menengah: Menghapus Folder Wallpaper Sistem

Ini akan membuktikan bahwa Snapper bisa mengembalikan data berukuran besar di folder sistem (`/usr`).

- **Target:** `/usr/share/backgrounds/` (atau folder wallpaper bawaan distro).
    
- **Cara Uji:**
    
    1. Buka folder tersebut di File Manager, pastikan wallpaper-nya ada.
        
    2. Buat snapshot: `sudo snapper create -d "Sebelum hapus wallpaper"`.
        
    3. Hapus foldernya: `sudo rm -rf /usr/share/backgrounds/`.
        
    4. Cek di File Manager; folder tersebut hilang.
        
    5. **Restore:** Lakukan rollback.
        
    6. Cek kembali: Seluruh gambar wallpaper akan kembali utuh tanpa kamu perlu download ulang.
        

### 3. Level "Simulasi Kerusakan": Menghapus Konfigurasi Shell

Ini menarik karena akan merusak tampilan terminal kamu.

- **Target:** `/etc/bashrc` atau `/etc/zshrc` (tergantung shell yang kamu gunakan).
    
- **Cara Uji:**
    
    1. Buat snapshot.
        
    2. Hapus filenya: `sudo rm /etc/bashrc`.
        
    3. Buka tab terminal baru. Kamu akan melihat tampilan terminal jadi sangat polos (hanya teks putih tanpa warna dan tanpa nama user) karena konfigurasinya hilang.
        
    4. **Restore:** Rollback menggunakan Snapper.
        
    5. Buka terminal baru lagi; tampilan cantik terminalmu akan kembali.
        

---

### Cara Melakukan Restore (Tanpa Reboot)

Jika kamu hanya menghapus file kecil dan sistem masih bisa masuk ke desktop, kamu tidak perlu reboot ke menu GRUB. Cukup gunakan perintah:

Bash

```
# Untuk melihat daftar perubahan antara sistem sekarang dan snapshot tertentu
sudo snapper status <nomor_snapshot>..0

# Untuk mengembalikan perubahan secara instan
sudo snapper undochange <nomor_snapshot>..0
```

_Angka `0` di sini artinya "kondisi sistem saat ini"._

---

### Tips Pengujian yang Bertanggung Jawab:

1. **Jangan hapus `/boot`** kecuali kamu sudah menginstal `grub-btrfs` dan sudah tes masuk ke menu snapshot di GRUB sebelumnya.
    
2. **Gunakan Deskripsi:** Selalu gunakan flag `-d "deskripsi"` saat membuat snapshot agar kamu tidak bingung saat melihat daftar di `snapper list`.
    
3. **Cek Space:** Pastikan kamu tidak menghapus file 10GB lalu membuat 10 snapshot baru dalam waktu singkat jika penyimpananmu terbatas.
    

Mau saya bantu buatkan _cheat sheet_ perintah Snapper yang paling sering digunakan agar kamu bisa menempelnya di catatan/terminal?