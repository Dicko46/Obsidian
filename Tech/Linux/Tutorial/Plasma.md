### 1. Kill Plasmashell when crash/freeze
```bash
pkill -9  plasmashell
```

## 2. Menambahkan file theme di plasma dari store.kde.org

```ad-note
# Untuk Plasma Global Theme (Look and Feel)
tar -xf nama-theme.tar.xz -C ~/.local/share/plasma/look-and-feel/

# Untuk Desktop Theme saja
tar -xf nama-theme.tar.xz -C ~/.local/share/plasma/desktoptheme/

# Untuk Window Decorations (Aurorae)
tar -xf nama-theme.tar.xz -C ~/.local/share/aurorae/themes/

# Untuk Kvantum Theme
tar -xf nama-theme.tar.xz -C ~/.local/share/Kvantum/
```
Berikut adalah daftar lengkap path untuk instalasi tema KDE Plasma secara manual:

## Path Tema Global

- **Global Themes**: `~/.local/share/plasma/look-and-feel/`
- **System-wide**: `/usr/share/plasma/look-and-feel/`

## Path Komponen Individual

### Plasma Themes (Desktop Theme)

- **User**: `~/.local/share/plasma/desktoptheme/`
- **System**: `/usr/share/plasma/desktoptheme/`

### Color Schemes

- **User**: `~/.local/share/color-schemes/`
- **System**: `/usr/share/color-schemes/`

### Window Decorations (Aurorae)

- **User**: `~/.local/share/aurorae/themes/`
- **System**: `/usr/share/aurorae/themes/`

### Icons

- **User**: `~/.local/share/icons/`
- **System**: `/usr/share/icons/`

### Cursors

- **User**: `~/.local/share/icons/` atau `~/.icons/`
- **System**: `/usr/share/icons/`

### Wallpapers

- **User**: `~/.local/share/wallpapers/`
- **System**: `/usr/share/wallpapers/`

### SDDM Themes (Login Screen)

- **System**: `/usr/share/sddm/themes/`

### Kvantum Themes

- **User**: `~/.config/Kvantum/`
- **System**: `/usr/share/Kvantum/`

### GTK Themes

- **User**: `~/.local/share/themes/` atau `~/.themes/`
- **System**: `/usr/share/themes/`

### Application Styles

- **System**: `/usr/lib/qt/plugins/styles/` (untuk Qt)
- **User**: Biasanya tidak ada path user untuk ini

### Splash Screens

- **User**: `~/.local/share/plasma/look-and-feel/[theme-name]/contents/splash/`
- **System**: `/usr/share/plasma/look-and-feel/[theme-name]/contents/splash/`

### Konsole Color Schemes

- **User**: `~/.local/share/konsole/`
- **System**: `/usr/share/konsole/`

## Tips Instalasi:

1. Ekstrak file tema ke direktori yang sesuai
2. Pastikan permission yang benar (untuk user path tidak perlu sudo)
3. Restart Plasma jika diperlukan: `plasmashell --replace &`
4. Atau logout dan login kembali

Path `~/.local/share/` adalah yang paling umum digunakan untuk instalasi manual oleh user tanpa memerlukan akses root.