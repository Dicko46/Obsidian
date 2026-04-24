Berdasarkan file konfigurasi yang Anda kirimkan, berikut adalah perubahan yang harus dilakukan pada baris `GRUB_CMDLINE_LINUX` untuk mengatasi masalah _stuttering_ pada Ryzen 7 6800H Anda:

### Edit File `/etc/default/grub`

Cukup tambahkan parameter tersebut di dalam tanda kutip setelah kata `quiet`. Hasil akhirnya akan terlihat seperti ini:

Bash

```
GRUB_TIMEOUT=5
GRUB_DISTRIBUTOR="$(sed 's, release .*$,,g' /etc/system-release)"
GRUB_DEFAULT=saved
GRUB_DISABLE_SUBMENU=true
GRUB_TERMINAL_OUTPUT="console"
# Perubahan pada baris di bawah ini:
GRUB_CMDLINE_LINUX="rhgb quiet amdgpu.dcdebugmask=0x10"
GRUB_DISABLE_RECOVERY="true"
GRUB_ENABLE_BLSCFG=true
```

---

### Langkah Eksekusi di Terminal Fedora

Setelah Anda menyimpan perubahan di atas menggunakan `sudo nano /etc/default/grub`, Anda **wajib** menjalankan perintah ini agar Fedora memperbarui menu _boot_-nya:

1. **Update Grub:**
    
    Bash
    
    ```
    sudo grub2-mkconfig -o /boot/grub2/grub.cfg
    ```
    
2. **Reboot Sistem:**
    
    Bash
    
    ```
    reboot
    ```
    

### Mengapa Parameter Ini Membantu?

Sesuai dengan log yang Anda unggah sebelumnya, terdapat error **Async Flip** dan **Wayland Connection Broke**. Pada arsitektur Ryzen 6000 (Rembrandt), fitur hemat daya bernama _Panel Self Refresh_ (PSR) sering kali menyebabkan sinkronisasi gambar tersendat selama 1-2 detik saat transisi dari kondisi idle ke aktif. Parameter `amdgpu.dcdebugmask=0x10` secara khusus menonaktifkan fitur PSR tersebut agar aliran data ke layar tetap stabil dan tidak macet saat Anda bermain game atau bekerja.

+3

**Satu tips tambahan:** Melihat banyaknya error `PreviewJob` pada log Anda terkait file video yang tidak ditemukan di penyimpanan eksternal (`/run/media/diecko/...`), saya sangat menyarankan untuk membersihkan cache _thumbnail_ setelah reboot agar sistem tidak terus-menerus "mencari" file yang hilang tersebut:

+2

Bash

```
rm -rf ~/.cache/thumbnails/*
```