# 1. Upgrade semua package ke versi terbaru

```bash
sudo dnf upgrade --refresh
```

# 2. Download update package untuk versi yang akan digunakan

```bash
sudo dnf system-upgrade download --releasever=43
```

"43" disini adalah versi fedora terbaru atau fedora yang akan diupgrade

atau gunakan :

```bash
sudo dnf system-upgrade download --releasever=43 --allowerasing
```

Jika terdapat conflict dengan package pada fedora sebelumnya

# 3. Reboot Upgrade

Setelah selesai download package maka akan tampil perintah untuk

```bash
dnf5 offline reboot
```
 
 Diatas adalah perintah untuk melakukan upgrade setelah reboot, maka lakukan perintah diatas jika sudah yakin untuk melanjutkan upgrade atau juga bisa gunakan perintah
 
```bash
sudo dnf5 offline clean
```

Untuk menghapus hasil download package yang dilakukan tadi dan mengcancel upgrade versi fedora