Berikut list command lengkap `udisksctl`:

---

### Mount ISO

bash

```bash
udisksctl loop-setup -f /path/ke/file.iso
```

### Cek Loop Device yang Aktif

bash

```bash
udisksctl status
```

atau

bash

```bash
losetup -l
```

### Unmount & Hapus Loop Device

bash

```bash
udisksctl loop-delete -b /dev/loop0
```

### Mount Block Device (USB/HDD)

bash

```bash
udisksctl mount -b /dev/sdb1
```

### Unmount Block Device

bash

```bash
udisksctl unmount -b /dev/sdb1
```

### Power Off Device (aman cabut USB)

bash

```bash
udisksctl power-off -b /dev/sdb
```

### Info Detail Sebuah Device

bash

```bash
udisksctl info -b /dev/loop0
```

### Dump Semua Info Device

bash

````bash
udisksctl dump
```

---

**Tips:** Setelah `loop-setup`, perhatikan output-nya karena akan muncul nama loop device yang dipakai, contoh:
```
Mapped file /home/user/file.iso as /dev/loop0.
````

Catat `/dev/loop0` itu untuk dipakai saat unmount.