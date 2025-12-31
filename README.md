

# Ultimate Linux Dev Setup Guide

Tutorial instalasi environment programming di Linux (Ubuntu/Debian base). Tanpa Snapd, menggunakan repository resmi dan tarball installer.

**Format:** 1 Blok Kode = 1 Perintah. Copy dan jalankan secara berurutan.

---

## Daftar Isi
0. [Foundation Tools](#0-foundation-tools)
1. [Git](#1-git)
2. [Visual Studio Code](#2-visual-studio-code)
3. [Android Studio](#3-android-studio)
4. [Python](#4-python)
5. [Golang](#5-golang)
6. [Rust](#6-rust)
7. [Node.js](#7-nodejs)
8. [PHP](#8-php)
9. [Composer](#9-composer)
10. [MySQL](#10-mysql)
11. [phpMyAdmin](#11-phpmyadmin)
12. [XAMPP (LAMPP)](#12-xampp-lampp)
13. [Docker](#13-docker)
14. [R Language](#14-r-language)
15. [Flutter](#15-flutter)
16. [Jupyter](#16-jupyter)
17. [Postman](#17-postman)

---

## 0. Foundation Tools

Instalasi dasar yang wajib ada sebelum menginstall aplikasi lain (Compiler, Make, dll).

### 1. Update Sistem

```bash
sudo apt update && sudo apt upgrade -y
```

### 2. Install Build Essential & Tools

> Paket ini wajib untuk mengcompile kode C/C++ yang digunakan oleh Python, NodeJS, Rust, dll.

```bash
sudo apt install build-essential git wget curl unzip software-properties-common apt-transport-https -y
```

---

## 1. Git

### 1. Install Git

```bash
sudo apt install git -y
```

### 2. Set Username Global

*Ganti "Nama Anda" dengan nama asli.*

```bash
git config --global user.name "Nama Anda"
```

### 3. Set Email Global

*Ganti dengan email GitHub/GitLab Anda.*

```bash
git config --global user.email "email@anda.com"
```

---

## 2. Visual Studio Code

### 1. Download GPG Key Microsoft

```bash
wget -qO- https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > packages.microsoft.gpg
```

### 2. Install Key ke Sistem

```bash
sudo install -o root -g root -m 644 packages.microsoft.gpg /etc/apt/trusted.gpg.d/
```

### 3. Tambahkan Repository VSCode

```bash
sudo sh -c 'echo "deb [arch=amd64,arm64,armhf signed-by=/etc/apt/trusted.gpg.d/packages.microsoft.gpg] https://packages.microsoft.com/repos/code stable main" > /etc/apt/sources.list.d/vscode.list'
```

### 4. Update & Install VSCode

```bash
sudo apt update && sudo apt install code -y
```

---

## 3. Android Studio

Metode manual tarball agar stabil dan terintegrasi menu.

### 1. Masuk ke Folder Opt

```bash
cd /opt
```

### 2. Buat Folder Android Studio

```bash
sudo mkdir android-studio && cd android-studio
```

### 3. Download Installer

*Download versi terbaru stable.*

```bash
sudo wget https://redirector.gvt1.com/edgedl/android/studio/ide-zips/2023.1.1.28/android-studio-2023.1.1.28-linux.tar.gz
```

### 4. Ekstrak File

*Proses ini mungkin memakan waktu.*

```bash
sudo tar -xvf android-studio-*.tar.gz --strip-components=1
```

### 5. Bersihkan File Installer

```bash
sudo rm android-studio-*.tar.gz
```

### 6. Buat File Menu Launcher

*Perintah ini membuka editor teks.*

```bash
sudo nano /usr/share/applications/android-studio.desktop
```

### 7. Isi Konfigurasi

Copy teks di bawah ini, lalu Paste ke dalam file Nano yang terbuka tadi.

```ini
[Desktop Entry]
Version=1.0
Type=Application
Name=Android Studio
Icon=/opt/android-studio/bin/studio.png
Exec="/opt/android-studio/bin/studio.sh" %f
Comment=The IDE for Android
Categories=Development;IDE;
Terminal=false
StartupWMClass=jetbrains-android-studio
```

### 8. Simpan File Nano

*Tekan `Ctrl + X`, lalu tekan `Y`, lalu `Enter`.*

### 9. Beri Izin Eksekusi

```bash
sudo chmod +x /usr/share/applications/android-studio.desktop
```

### 10. Update Database Menu

```bash
sudo update-desktop-database /usr/share/applications/
```

---

## 4. Python

### 1. Install Python 3 & Pip

```bash
sudo apt install python3 python3-pip python3-venv -y
```

---

## 5. Golang

### 1. Hapus Instalasi Lama (Jika ada)

```bash
sudo rm -rf /usr/local/go
```

### 2. Download Go (v1.21.5)

```bash
wget https://go.dev/dl/go1.21.5.linux-amd64.tar.gz
```

### 3. Ekstrak ke /usr/local

```bash
sudo tar -C /usr/local -xzf go1.21.5.linux-amd64.tar.gz
```

### 4. Tambahkan Path ke .bashrc

```bash
echo 'export PATH=$PATH:/usr/local/go/bin' >> ~/.bashrc
```

### 5. Reload Configuration

```bash
source ~/.bashrc
```

### 6. Cek Versi

```bash
go version
```

---

## 6. Rust

### 1. Download dan Jalankan Installer Rustup

```bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

> Setelah perintah di atas berjalan, ketik angka `1` lalu Enter untuk melanjutkan instalasi default.

### 2. Reload Environment

```bash
source ~/.cargo/env
```

---

## 7. Node.js

### 1. Setup Repository NodeSource (Versi 20 LTS)

```bash
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
```

### 2. Install Node.js & NPM

```bash
sudo apt install -y nodejs
```

---

## 8. PHP

### 1. Install PHP 8.x + Ekstensi

```bash
sudo apt install php php-fpm php-curl php-xml php-mysql php-mbstring php-zip php-bcmath php-intl -y
```

---

## 9. Composer

### 1. Download Composer Installer

```bash
php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
```

### 2. Install Composer Global

```bash
sudo php composer-setup.php --install-dir=/usr/local/bin --filename=composer
```

### 3. Hapus Installer

```bash
php -r "unlink('composer-setup.php');"
```

---

## 10. MySQL

### 1. Install MySQL Server

```bash
sudo apt install mysql-server -y
```

### 2. Jalankan Secure Installation

> Saat diminta VALIDATE PASSWORD COMPONENT, pilih **N** (No) agar tidak ribet.

```bash
sudo mysql_secure_installation
```

---

## 11. phpMyAdmin

### 1. Install Paket

```bash
sudo apt install phpmyadmin -y
```

> Pilih **Apache2**. Pilih **Yes** untuk dbconfig-common. Masukkan password.

### 2. Buat Symlink ke Apache

```bash
sudo ln -s /usr/share/phpmyadmin /var/www/html/phpmyadmin
```

### 3. Restart Apache

```bash
sudo systemctl restart apache2
```

---

## 12. XAMPP (LAMPP)

### 1. Download Installer XAMPP

```bash
wget https://sourceforge.net/projects/xampp/files/XAMPP%20Linux/8.2.12/xampp-linux-x64-8.2.12-0-installer.run
```

### 2. Beri Izin Eksekusi

```bash
chmod 755 xampp-linux-x64-8.2.12-0-installer.run
```

### 3. Jalankan Installer GUI

```bash
sudo ./xampp-linux-x64-8.2.12-0-installer.run
```

### 4. Buat Launcher Menu

```bash
sudo nano /usr/share/applications/xampp-control-panel.desktop
```

### 5. Isi Konfigurasi

```ini
[Desktop Entry]
Version=1.0
Type=Application
Name=XAMPP Control Panel
Exec=python3 /opt/lampp/manager-linux-x64.py
Icon=/opt/lampp/htdocs/favicon.ico
Terminal=false
Categories=Development;
```

---

## 13. Docker

### 1. Install Prerequisite

```bash
sudo apt-get install ca-certificates curl gnupg -y
```

### 2. Buat Folder Keyrings

```bash
sudo install -m 0755 -d /etc/apt/keyrings
```

### 3. Download Docker GPG Key

```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```

### 4. Atur Permission Key

```bash
sudo chmod a+r /etc/apt/keyrings/docker.gpg
```

### 5. Tambahkan Repository

```bash
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

### 6. Install Docker Engine

```bash
sudo apt-get update && sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin -y
```

### 7. (Opsional) Menggunakan Docker tanpa Sudo

> Agar tidak perlu ketik sudo setiap kali menjalankan docker.

```bash
sudo groupadd docker
```

```bash
sudo usermod -aG docker $USER
```

```bash
newgrp docker
```

---

## 14. R Language

### 1. Tambah Repository CRAN

```bash
sudo add-apt-repository "deb https://cloud.r-project.org/bin/linux/ubuntu $(lsb_release -cs)-cran40/"
```

### 2. Tambahkan Secure Key

```bash
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E298A3A825C0D65DFD57CBB651716619E084DAB9
```

### 3. Install R Base

```bash
sudo apt update && sudo apt install r-base r-base-dev -y
```

---

## 15. Flutter

### 1. Clone Flutter SDK

```bash
cd ~ && git clone https://github.com/flutter/flutter.git -b stable --depth 1
```

### 2. Tambahkan ke PATH

```bash
echo 'export PATH="$PATH:$HOME/flutter/bin"' >> ~/.bashrc
```

### 3. Reload Bash

```bash
source ~/.bashrc
```

### 4. Cek Status

```bash
flutter doctor
```

---

## 16. Jupyter

### 1. Upgrade Pip

```bash
pip install --upgrade pip
```

### 2. Install Jupyter

```bash
pip install jupyter
```

### 3. Install Jupyter Lab (Opsional)

```bash
pip install jupyterlab
```

---

## 17. Postman

### 1. Download Postman

```bash
wget https://dl.pstmn.io/download/latest/linux64 -O postman-linux-x64.tar.gz
```

### 2. Ekstrak ke /opt

```bash
sudo tar -xzf postman-linux-x64.tar.gz -C /opt
```

### 3. Hapus File Download

```bash
rm postman-linux-x64.tar.gz
```

### 4. Buat Launcher Menu

```bash
sudo nano /usr/share/applications/postman.desktop
```

### 5. Isi Konfigurasi

```ini
[Desktop Entry]
Encoding=UTF-8
Name=Postman
Exec=/opt/Postman/Postman
Icon=/opt/Postman/app/resources/app/assets/icon.png
Terminal=false
Type=Application
Categories=Development;
MimeType=text/plain
```

### 6. Update Database Menu

```bash
sudo update-desktop-database
```
