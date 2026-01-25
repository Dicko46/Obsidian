## 1. 📚 Dasar Konsep Flakes

### **Apa itu Flakes?**

- Sistem reproducible build dan dependency management
    
- Menggantikan traditional channels (nix-channel)
    
- Deterministic package versions
    
- Lock file untuk version pinning

### Enable Flakes (jika belum)**

### /etc/nixos/configuration.nix
nix.settings.experimental-features = [ "nix-command" "flakes" ];

```ad-note
Tambahkan code diatas untuk mengaktifkan fitur experimental flakes
```

## 🏗️ Struktur Flake Basic

```nix
{
  description = "My NixOS Configuration";

  inputs = {
    nixpkgs.url = "github:nixos/nixpkgs/nixos-unstable";
    home-manager.url = "github:nix-community/home-manager";
    home-manager.inputs.nixpkgs.follows = "nixpkgs";
  };

  outputs = { self, nixpkgs, home-manager, ... }@inputs: {
    nixosConfigurations = {
      "my-hostname" = nixpkgs.lib.nixosSystem {
        system = "x86_64-linux";
        modules = [
          ./configuration.nix
          home-manager.nixosModules.home-manager
          {
            home-manager.useGlobalPkgs = true;
            home-manager.useUserPackages = true;
            home-manager.users.username = import ./home.nix;
          }
        ];
      };
    };
  };
}
```


## 🔄 Workflow Update & Maintenance

### **Update Semua Inputs**

bash

# Update semua packages ke versi terbaru

```bash
nix flake update --flake /home/dicko/myFlakes # Masukkan path yang sesuai
```

# Update specific input

```bash
nix flake lock --update-input nixpgs --flake /home/dicko/myFlakes#nixos
```
# Preview update (tanpa apply)

```bash
nix flake update --dry-run --flake /home/dicko/myFlakes
```

# Build dan switch

```bash
sudo nixos-rebuild switch --flake /home/dicko/myFlakes#nixos
```

# Build saja (testing)

```bash
sudo nixos-rebuild build --flake /home/dicko/myFlakes#nixos
```

# Test mode (hilang setelah reboot)

```bash
sudo nixos-rebuild test --flake /home/dicko/myFlakes#nixos
```

# Rollback ke generation sebelumnya

```bash
sudo nixos-rebuild switch --rollbaack
```
# List semua generation

```bash
nixos-rebuild list-generations
```
# Switch ke generation tertentu

```bash
sudo nixos-rebuild switch --generation 12
```
# Hapus old generations

```bash
sudo nix-collect-garbage -d
```

***
---

## 2. 🏠 Home-Manager Deep Dive

### **Struktur Home Configuration**
#### home.nix
```nix
{ config, pkgs, ... }:

{
  # User info
  home.username = "myuser";
  home.homeDirectory = "/home/myuser";
  
  # State version (WAJIB!)
  home.stateVersion = "23.11";

  # Packages
  home.packages = with pkgs; [
    neovim
    git
    htop
    ripgrep
    fzf
  ];

  # Dotfiles configuration
  programs.git = {
    enable = true;
    userName = "My Name";
    userEmail = "email@example.com";
  };

  programs.bash = {
    enable = true;
    shellAliases = {
      ll = "ls -l";
      update = "sudo nixos-rebuild switch --flake .#";
    };
  };

  # Services
  services = {
    gpg-agent = {
      enable = true;
      defaultCacheTtl = 1800;
    };
  };
}
```

# Build home configuration

```bash
home-manager build --flake /home/dicko/myFlakes#nixos
```
# Apply home configuration

```bash
home-manager switch --flake /home/dicko/myFlakes#nixos
```
# Update home-manager

```bash
nix flake update --update-input home-manager
```
# Rollback home-manager

```bash
home-manager generations
home-manager switch --generation13
```

## ⚡ Advanced Flake Patterns

### **Multi-Machine Setup**

```nix
{
  outputs = { self, nixpkgs, ... }@inputs: {
    nixosConfigurations = {
      # Desktop
      "desktop" = nixpkgs.lib.nixosSystem {
        system = "x86_64-linux";
        modules = [ ./hosts/desktop ];
      };
      
      # Laptop  
      "laptop" = nixpkgs.lib.nixosSystem {
        system = "x86_64-linux";
        modules = [ ./hosts/laptop ];
      };
    };
  };
}

```

### **Custom Packages & Overlays**

```nix
{
  inputs = {
    nixpkgs.url = "github:nixos/nixpkgs/nixos-unstable";
    custom-pkgs.url = "github:user/custom-packages";
  };

  outputs = { self, nixpkgs, custom-pkgs, ... }:
    let
      system = "x86_64-linux";
      pkgs = import nixpkgs {
        inherit system;
        overlays = [ custom-pkgs.overlays.default ];
      };
    in {
      nixosConfigurations.hostname = nixpkgs.lib.nixosSystem {
        inherit system;
        modules = [ 
          ({ config, pkgs, ... }: {
            environment.systemPackages = with pkgs; [
              custom-package
            ];
          })
        ];
      };
    };
}

```

## 🛡️ Error Prevention & Best Practices

### **1. State Version Management**

nix

# SELALU set state version, jangan di-update sembarangan
system.stateVersion = "23.11"; # Tanggal install pertama
home.stateVersion = "23.11";   # Sama dengan system

### **2. Modular Configuration**

```ad-note
├── flake.nix
├── configuration.nix
├── hosts/
│   ├── desktop.nix
│   └── laptop.nix
├── modules/
│   ├── networking.nix
│   ├── desktop.nix
│   └── development.nix
└── home/
    ├── default.nix
    ├── shell.nix
    └── editors.nix
```

### **3. Safe Testing Workflow**

bash

# 1. Test build dulu
sudo nixos-rebuild build --flake .#

# 2. Jika berhasil, test boot
sudo nixos-rebuild boot --flake .#

# 3. Terakhir apply
sudo nixos-rebuild switch --flake .#

# Atau menggunakan test (temporary)
sudo nixos-rebuild test --flake .#

### **4. Backup Strategy**

bash

# Backup flake lock
cp flake.lock flake.lock.backup

# Backup generation sebelum update
sudo nixos-rebuild switch --flake .# --backup-to /backup/location

# Git untuk version control
git add .
git commit -m "Before major update"

## 🔧 Troubleshooting Common Issues

### **Build Failures**

bash

# Clean build
sudo nixos-rebuild switch --flake .# --option sandbox false

# Check dependencies
nix why-depends /run/current-system /nix/store/package-hash

# Debug dengan trace
nixos-rebuild build --flake .# --show-trace

### **Recovery dari Broken State**

bash

# Boot ke generation sebelumnya dari boot menu
# Atau dari live USB:
sudo nixos-rebuild switch --flake /mnt/etc/nixos#hostname

### **GC Issues**

bash

# Hapus unused packages
nix-store --gc

# Hapus old generations
sudo nix-collect-garbage -d

# Optimize store
nix-store --optimise

## 🚀 Pro Tips untuk Power Users

### **1. Automated Updates**

nix

# Dalam configuration.nix
system.autoUpgrade = {
  enable = true;
  flake = "/etc/nixos";
  flags = [ "--update-input" "nixpkgs" ];
  dates = "daily";
};

### **2. Cached Builds**

nix

# Gunakan cachix untuk build caching
nix.settings = {
  substituters = ["https://cache.nixos.org/" "https://my-cache.cachix.org"];
  trusted-public-keys = ["cache.nixos.org-1:...", "my-cache.cachix.org-1:..."];
};

### **3. Development Environments**

nix

# devShell untuk project-specific environments
{
  devShells.x86_64-linux = {
    default = pkgs.mkShell {
      buildInputs = with pkgs; [ 
        nodejs 
        python3 
        git 
      ];
      shellHook = ''
        echo "Welcome to dev environment!"
      '';
    };
  };
}

### **4. Secret Management**

nix

# Gunakan sops-nix atau agenix untuk secrets
{
  sops.defaultSopsFile = ./secrets.yaml;
  sops.age.keyFile = "/home/user/.config/sops/age/keys.txt";
}

# Daily workflow

```bash
nix flake update                    # Update packages
sudo nixos-rebuild switch --flake .#  # Apply system
home-manager switch --flake .#        # Apply user config
```

# Recovery

```bash
sudo nixos-rebuild switch --rollback  # Rollback system
home-manager switch --generation X    # Rollback home
```

# Maintenance

```bash
nix-collect-garbage -d              # Cleanup
nix-store --optimise                # Optimize
```


```ad-info
Dengan menguasai Flakes + Home-Manager, Anda mendapatkan:
- ✅ **Reproducible builds**
    
- ✅ **Easy rollbacks**
    
- ✅ **Multi-machine management**
    
- ✅ **Dotfiles as code**
    
- ✅ **Atomic updates**
    
- ✅ **Version controlled configuration
```

#nixos #flakes #home-manager