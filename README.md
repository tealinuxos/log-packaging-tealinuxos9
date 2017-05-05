Log packaging tealinuxos 9 
===============================
-------------------------------------------
## Panduan unpack iso pertama kali ##

```shell
$ sudo uck-remaster-unpack-iso namafile.iso
$ sudo uck-remaster-unpack-rootfs
$ sudo uck-remaster-unpack-initrd
$ sudo uck-remaster-chroot-rootfs
```

Jika sudah pernah melakukan unpack maka hanya perlu `sudo uck-remaster-chroot-rootfs`

------------------------------------
## Memulai menghapus ##

- pertama lihat daftar aplikasi yang terdaftar dengan nama aplikasi namaaplikasi

- dengan perintah `dpkg -l | grep namaaplikasi` 

- misalkan begini `dpkg -l | grep libreoffice` maka hasilnya yang ada dibawah

```shell

ii  libreoffice-base-core                 1:5.1.2-0ubuntu1                                    amd64        office productivity suite -- shared library
ii  libreoffice-calc                      1:5.1.2-0ubuntu1                                    amd64        office productivity suite -- spreadsheet
ii  libreoffice-common                    1:5.1.2-0ubuntu1                                    all          office productivity suite -- arch-independent files
ii  libreoffice-core                      1:5.1.2-0ubuntu1                                    amd64        office productivity suite -- arch-dependent files
ii  libreoffice-gtk                       1:5.1.2-0ubuntu1                                    amd64        office productivity suite -- GTK+ integration
ii  libreoffice-math                      1:5.1.2-0ubuntu1                                    amd64        office productivity suite -- equation editor
ii  libreoffice-style-elementary          1:5.1.2-0ubuntu1                                    all          office productivity suite -- Elementary symbol style
ii  libreoffice-style-galaxy              1:5.1.2-0ubuntu1                                    all          office productivity suite -- Galaxy (Default) symbol style
ii  libreoffice-writer                    1:5.1.2-0ubuntu1                                    amd64        office productivity suite -- word processor
```

- kemudian catat semua aplikasi yang ada satu persatu dengan hanya mengambil nama aplikasi

- misalnya begini

```shell
-> libreoffice-base-core
-> libreoffice-calc
-> libreoffice-common
.....[teruskan sendiri]
```

- saat sudah maka mulai dengan menghapus aplikasi-aplikasi tadi dengan perintah

```shell
# apt remove --purge namaaplikasi
# apt autoremove
# apt autoclean
```

- jika ada notif `[Y/n]` pada saat remove maka pilih `Y`

- selesaikan semua daftar aplikasi ini

```shell
-> orage
-> gigolo
-> pidgin
-> pidgin-data
-> pidgin-libnotify
-> pidgin-otr
-> thunderbird
-> parole
-> ristretto
-> transmission-common
-> transmission-gtk
-> xfce4-dict
-> evince-common
-> gnome-mines
-> gnome-sudoku
-> mousepad
-> xfce4-notes
-> xfce4-notes-plugin
-> xfce4-screenshooter
-> xfburn
-> firefox
-> firefox-locale-en
-> gnome-calculator
-> gnome-software
-> gnome-software-common
-> gnome-system-tools
-> xfce4-taskmanager
```

#### Hati-hati dalam menghapus aplikasi ####

------------------------------------------------------------
## Memulai install aplikasi default tealinuxos 9 ##

- install aplikasi default yang sudah ditetapkan dan dirundingkan oleh 

- cara install aplikasi ` apt install namaaplikasi`

- jika ada notif `[Y/n]` maka pilih `Y`

- daftar aplikasi yang secara default terinstall 

- pertama update dan upgrade dulu `apt update; apt upgrade`

```shell
-> gnome-calculator
-> gnome-software
-> gnome-system-monitor
-> vlc
-> audacious
-> evince 
-> nautilus
-> nautilus-admin
-> xubuntu-restricted-extras
-> gdebi
-> gpicview
-> python-pip
-> git
-> gedit
-> xserver-xorg-video-intel
```

#### Hati-hati dalam menambahkan aplikasi ####

--------------------------------------------------
## Memulai install aplikasi dari nambah ppa ##

- pertama cari dulu ppa yang akan ditambahkan

- cara menambahkan ppa `add-apt-repository ppa:darimana/nama-aplikasi`

- sesudah itu update repo `apt update`

- lalu install nama aplikasi yang tadi sudah ditambahkan `apt install namaaplikasi`

- ada beberapa yang harus ditambahkan melalui ppa

firefox dev edition       | `ppa:ubuntu-mozilla-daily/firefox-aurora`

tea-installer-gtk         | `ppa:tea-projects/softwares`

tea-maker-gtk             | `ppa:tea-projects/softwares`

theme-switcher-tray       | `ppa:tea-projects/softwares`

#### Hati-hati dalam menambahkan aplikasi dari ppa ####

--------------------------------------------------
## Memulai mengganti plymouth ##

- pastikan sudah punya satu gelondong file nya, bisa bikin sendiri ataupun cari di internet

- dalam satu gelodong tadi terdapat `namaplymouth.plymouth` dan `namaplymouth.script`

- jika sudah copy paste file gelondong tadi ke `tmp/remaster-root/usr/share/plymouth/themes/` 

- kemudian disana ada link yang namanya `default.plymouth` dan `text.plymouth`

- kemudian kedua file tadi menggunakan perintah `tmp/remaster-root/usr/share/plymouth/themes/default.plymouth` di terminal kamu

- maka hasilnya seperti ini

```shell
[Plymouth Theme]
Name=tealinuxos
Description=tealinuxos plymouth 
ModuleName=script

[script]
ImageDir=/usr/share/plymouth/themes/tealinuxos
ScriptFile=/usr/share/plymouth/themes/tealinuxos/tealinuxos.script
```

- aslinya default bawaan, maka diganti dengan tealinuxos

- jika sudah save

- kemudian edit satunya `tmp/remaster-root/usr/share/plymouth/themes/text.plymouth`

```shell
[Plymouth Theme]
Name=Xubuntu Text
Description=Text mode theme based on xubuntu-logo theme
ModuleName=ubuntu-text

[ubuntu-text]
title=TeaLinuxOS 8.0
black=0x000000
white=0xffffff
brown=0x000000
blue=0xffffff
```

- ganti settin default dengan setting tealinuxos

- jika sudah save

- kemudian ketik perintah ini menggunakan terminal `update-initramfs -u`


#### Hati-hati dalam mengganti plymouth default ####

---------------------------
## Memulai mengganti tema default ##

- siapkan tema yang akan dijadikan default

- copy segelondong tema yang sudah ada ke `tmp/remaster-root/usr/share/themes/`

- kemudian edit file yang ada di `tmp/remaster-root/etc/xdg/xdg-xubuntu/xfce4/xfconf/xfce-perchannel-xml/xsettings.xml` menggunakan text editor

- kemudian edit file `xsettings.xml` yang berisi default diganti dengan nama tema yang akan dijadikan default

```shell
<?xml version="1.0" encoding="UTF-8"?>

<channel name="xsettings" version="1.0">
  <property name="Net" type="empty">
    <property name="ThemeName" type="string" value="Tea-Mint-Light"/>
    <property name="IconThemeName" type="string" value="Tea-Mint-Light"/>
  </property>
  <property name="Xft" type="empty">
    <property name="DPI" type="int" value="96"/>
    <property name="Antialias" type="int" value="1"/>
    <property name="Hinting" type="int" value="1"/>
    <property name="HintStyle" type="string" value="hintslight"/>
    <property name="RGBA" type="string" value="rgb"/>
    <property name="Lcdfilter" type="string" value="lcddefault"/>
  </property>
  <property name="Gtk" type="empty">
    <property name="CursorThemeName" type="string" value="Human"/>
    <property name="CursorThemeSize" type="int" value="24"/>
    <property name="DecorationLayout" type="string" value="menu:minimize,maximize,close"/>
    <property name="FontName" type="string" value="Ubuntu 9"/>
    <property name="IconSizes" type="string" value="gtk-button=16,16"/>
  </property>
</channel>
```

- lihat "Tea-Mint-Light" 

- kita juga bisa memberikan tema kursor default, font default dan ukuran ikon

- jika sudah save

#### Hati-hati dalam mengganti settingan ini ####

---------------------------
