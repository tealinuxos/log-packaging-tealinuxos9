Log packaging tealinuxos 9 
===============================
-------------------------------------------
## Panduan unpack iso pertama kali ##

```shell
$ sudo uck-remaster-unpack-iso namafile.iso
$ sudo uck-remaster-unpack-rootfs
$ sudo uck-remaster-chroot-rootfs
```

Jika sudah pernah melakukan unpack maka hanya perlu `sudo uck-remaster-chroot-rootfs`

------------------------------------

## Panduan pack iso pertama kali ##

- lakukan `apt -f install` terlebih dahulu saat masih di `chroot`

- kemudian ini `ls /lib/modules/`

- maka akan terlihat `4.8.0-36-generic` 

- jika sudah buat `initrd.lz` dengan cara `mkinitramfs 4.8.0-36-generic -o /tmp/initrd.lz`

- kemudian copy file `initrd.lz` dari `tmp/remaster-root/tmp/` ke `tmp/remaster-iso/casper/` kemudian replace

- jika sudah pack

```shell
# rm -rf /var/lib/apt/lists/*
# rm -rf /var/cache/apt/*
# exit
$ sudo uck-remaster-pack-rootfs
$ sudo uck-remaster-pack-iso -d "tealinuxos" tealinux-test-brpbit.iso
```

- jika 32bit -> `i386` atau 64bit -> `amd64`

- jika sudah maka file `tealinux-test-brpbit.iso` ada di `tmp/remaster-new-files`

-------------------------------------------
 
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
-> xfburn
-> firefox
-> firefox-locale-en
-> xfce4-taskmanager
```

#### Hati-hati dalam menghapus aplikasi ####

------------------------------------------------------------
## Memulai install aplikasi default ##

- install aplikasi default yang sudah ditetapkan dan dirundingkan oleh 

- cara install aplikasi ` apt install namaaplikasi`

- jika ada notif `[Y/n]` maka pilih `Y`

- daftar aplikasi yang secara default terinstall 

- pertama update dan upgrade dulu `apt update`

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
-> unzip
-> unrar
-> libreoffice
-> xserver-xorg-video-intel
-> npm
```

#### Hati-hati dalam menambahkan aplikasi ####

--------------------------------------------------
## Memulai install aplikasi dari nambah ppa ##

- pertama cari dulu ppa yang akan ditambahkan

- cara menambahkan ppa `add-apt-repository ppa:darimana/nama-aplikasi`

- sesudah itu update repo `apt update`

- lalu install nama aplikasi yang tadi sudah ditambahkan `apt install namaaplikasi`

- ada beberapa yang harus ditambahkan melalui ppa

firefox                   | `ppa:ubuntu-mozilla-daily/firefox-aurora`

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

- kemudian edit file-file tadi `tmp/remaster-root/usr/share/plymouth/themes/default.plymouth` di terminal kamu

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

- atau menggunakan cara ini

```shell
update-alternatives --install /usr/share/plymouth/themes/default.plymouth default.plymouth /usr/share/plymouth/themes/nama-tema/nama-tema.plymouth 200
update-alternatives --config default.plymouth #pilih *1
update-initramfs -u
```

#### Hati-hati dalam mengganti plymouth default ####

- pada saat `update-initramfs -u` akan ada error 

```shell
update-initramfs: Generating /boot/initrd.img-4.8.0-040800-generic
W: Possible missing firmware /lib/firmware/i915/kbl_dmc_ver1_01.bin for module i915
W: Possible missing firmware /lib/firmware/i915/kbl_guc_ver9_14.bin for module i915
W: Possible missing firmware /lib/firmware/i915/bxt_guc_ver8_7.bin for module i915
```

- download file-file tadi di https://01.org/linuxgraphics/downloads/firmware 

- extract didalam folder `tmp/remaster-root/` 

- kemudian install `./install.sh` satu persatu dari dalam folder

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

## Memulai mengganti wallpaper default ##

- pertama pilih wallpaper yang akan dijadikan sebagai default

- kemudian copy wallpaper tadi ke `tmp/remaster-root/usr/share/xfce4/backdrops/`

- kemudian edit file `tmp/remaster-root/etc/xdg/xdg-xubuntu/xfce4/xfconf/xfce-perchannel-xml/xfce4-desktop.xml`

- isi file 

```shell
<?xml version="1.0" encoding="UTF-8"?>

<channel name="xfce4-desktop" version="1.0">
  <property name="desktop-icons" type="empty">
    <property name="style" type="empty"/>
    <property name="file-icons" type="empty">
      <property name="show-home" type="bool" value="false"/>
      <property name="show-filesystem" type="bool" value="false"/>
      <property name="show-removable" type="bool" value="false"/>
      <property name="show-trash" type="bool" value="false"/>
    </property>
    <property name="icon-size" type="empty"/>
    <property name="tooltip-size" type="empty"/>
  </property>
  <property name="backdrop" type="empty">
    <property name="screen0" type="empty">
      <property name="monitor0" type="empty">
        <property name="image-path" type="empty"/>
        <property name="image-style" type="empty"/>
        <property name="image-show" type="empty"/>
        <property name="workspace0" type="empty">
          <property name="color-style" type="int" value="0"/>
          <property name="image-style" type="int" value="5"/>
          <property name="last-image" type="string" value="/usr/share/xfce4/backdrops/raptor_lick_the_past.png"/>
        </property>
        <property name="workspace1" type="empty">
          <property name="color-style" type="int" value="0"/>
          <property name="image-style" type="int" value="5"/>
          <property name="last-image" type="string" value="/usr/share/xfce4/backdrops/raptor_lick_the_past.png"/>
        </property>
      </property>
      <property name="monitor1" type="empty">
        <property name="image-path" type="empty"/>
        <property name="image-style" type="empty"/>
        <property name="image-show" type="empty"/>
      </property>
    </property>
  </property>
  <property name="last" type="empty">
    <property name="window-width" type="int" value="640"/>
    <property name="window-height" type="int" value="539"/>
  </property>
</channel>
```

- ganti `raptor_lick_the_past.png` dengan wallpaper yang dipilih

- kemudian save

- buatlah satu file dengan nama `tealinux.xml` di `tmp/remaster-root/etc/xdg/xdg-xubuntu/xfce4/xfconf/xfce-perchannel-xml/` 

- kemudian isi file tadi adalah

```shell
<?xml version="1.0" encoding="UTF-8"?>

<channel name="tealinux" version="1.0">
  <property name="switcher" type="empty">
    <property name="DevTheme" type="string" value="Working-Theme-Dark"/>
    <property name="DevWindow" type="string" value="Working-Theme-Dark"/>
    <property name="DevIcon" type="string" value="Paper2"/>
    <property name="NormalTheme" type="string" value="Working-Theme-Greet"/>
    <property name="NormalWindow" type="string" value="Working-Theme-Greet"/>
    <property name="NormalIcon" type="string" value="Paper"/>
  </property>
</channel>
```

- kemudian save

#### Hati-hati dalam mengganti settingan ini ####

---------------------------

## Memulai menambah shortcut default ##

- pertama siapkan nama aplikasi yang akan ditambah sebagai default

- pikirkan tombol kombinasi apa yang akan dijadikan shirtcut key

- kemudian edit file di `tmp/remaster-root/etc/xdg/xdg-xubuntu/xfce4/xfconf/xfce-perchannel-xml/xfce4-keyboard-shortcuts.xml`

- hasilnya seperti ini 

```shell
<property name="&lt;Primary&gt;&lt;Alt&gt;l" type="string" value="xflock4"/>
      <property name="&lt;Super&gt;1" type="string" value="parole"/>
      <property name="&lt;Super&gt;2" type="string" value="pidgin"/>
      <property name="&lt;Super&gt;p" type="string" value="xfce4-display-settings --minimal"/>
      <property name="&lt;Super&gt;3" type="string" value="libreoffice --writer"/>
      <property name="&lt;Primary&gt;&lt;Alt&gt;t" type="string" value="exo-open --launch TerminalEmulator"/>
      <property name="&lt;Super&gt;r" type="string" value="xfce4-appfinder"/>
      <property name="&lt;Super&gt;t" type="string" value="exo-open --launch TerminalEmulator"/>
      <property name="&lt;Super&gt;w" type="string" value="exo-open --launch WebBrowser"/>
      <property name="&lt;Super&gt;4" type="string" value="libreoffice --calc"/>
      <property name="XF86Display" type="string" value="xfce4-display-settings --minimal"/>
      <property name="&lt;Alt&gt;F1" type="string" value="xfce4-popup-applicationsmenu"/>
      <property name="XF86WWW" type="string" value="exo-open --launch WebBrowser"/>
      <property name="XF86Mail" type="string" value="exo-open --launch MailReader"/>
      <property name="&lt;Primary&gt;&lt;Alt&gt;Escape" type="string" value="xkill"/>
      <property name="XF86Messenger" type="string" value="pidgin"/>
      <property name="XF86Calculator" type="string" value="gnome-calculator"/>
      <property name="XF86Music" type="string" value="parole"/>
      <property name="XF86HomePage" type="string" value="exo-open --launch WebBrowser"/>
      <property name="override" type="bool" value="true"/>
      <property name="Super_L" type="string" value="xfce4-popup-whiskermenu"/>
      <property name="F12" type="string" value="xfce4-terminal --drop-down"/>
      <property name="&lt;Shift&gt;Print" type="string" value="xfce4-screenshooter -r"/>
      <property name="&lt;Super&gt;" type="string" value="xfce4-popup-whiskermenu"/>
```

- dengan cara `<property name="namatombol" type="string" value="command/nama-aplikasi"/>`

- kemudian save

#### Hati-hati dalam mengganti settingan ini ####

---------------------------

## Memulai mengganti username dan hostname (live session) ##

- pertama buka `tmp/remaster-root/etc/casper.conf`

- edit file yang isinya ini

```shell
# This file should go in /etc/casper.conf
# Supported variables are:
# USERNAME, USERFULLNAME, HOST, BUILD_SYSTEM, FLAVOUR

export USERNAME="tealinuxos"
export USERFULLNAME="Live session user"
export HOST="tealinuxos"
export BUILD_SYSTEM="Ubuntu"

# USERNAME and HOSTNAME as specified above won't be honoured and will be set to
# flavour string acquired at boot time, unless you set FLAVOUR to any
# non-empty string.

# export FLAVOUR="Ubuntu"
```

- jika sudah save

#### Hati-hati dalam mengganti settingan ini ####

---------------------------

## Memulai agar os menjadi tealinux ##

- ganti yang tulisan xubuntu menjadi TeaLinuxOS 9.0

- ada di `tmp/remaster-iso/.disk/info`

- `tmp/remaster-iso/isolinux/txt.cfg`

- `tmp/remaster-iso/boot/grub/grub.cfg`

#### Hati-hati dalam mengganti settingan ini ####

---------------------------

## Memulai mengganti whisker ##

- siapkan file

- kemudian taruh di `tmp/remaster-root/usr/share/pixmaps/` dengan ekstensi `.png`

- kemudian edit file `tmp/remaster-root/etc/xdg/xdg-xubuntu/xfce4/whiskermenu/default.rc`

- edit file agar icon whisker menggunakan icon kita

- jika sudah save 

#### Hati-hati dalam mengganti settingan ini ####

---------------------------


## Memulai menambah panel ##

- buka `tmp/remaster-root/etc/xdg/xdg-xubuntu/xfce4/panel/default.xml`

- dan tambah ini setelah `plugin-8`

```shell
    <property name="plugin-9" type="string" value="pager"/>
    <property name="plugin-10" type="string" value="actions">
      <property name="ask-confirmation" type="bool" value="true"/>
      <property name="appearance" type="uint" value="0"/>
      <property name="items" type="array">
        <value type="string" value="-lock-screen"/>
        <value type="string" value="-switch-user"/>
        <value type="string" value="-separator"/>
        <value type="string" value="-suspend"/>
        <value type="string" value="-hibernate"/>
        <value type="string" value="-separator"/>
        <value type="string" value="-shutdown"/>
        <value type="string" value="-restart"/>
        <value type="string" value="-separator"/>
        <value type="string" value="+logout"/>
        <value type="string" value="-logout-dialog"/>
      </property>
    </property>
```

#### Hati - hati dalam mengganti setting ####

------------------------------------------------

## Memulai mengganti background saat install ##

- siapkan backgroundnya dulu

- lalu edit `tmp/remaster-root/usr/bin/ubiquity-dm`

- edit bagian ini 

```shell
background_image = None
            for background in (
                    '/usr/share/xfce4/backdrops/bg-wp-web-ver.png',
                    '/usr/share/backgrounds/'
                    'ubuntustudio/ubuntustudio-default.png',
                    '/usr/share/lubuntu/wallpapers/'
                    'lubuntu-default-wallpaper.png'):
                exists = os.access(background, os.R_OK)
                if exists:
                    background_image = background
                    break

            accessibility = False
```

- pastikan sesuai dengan nama background

## Memulai mengganti theme lightdm greeter ##

- siapkan tema, icon, font

- buka `tmp/remaster-root/etc/lightdm/lightdm-gtk-greeter.conf`

- kemudian isi dengan

```shell 
[greeter]
background = /usr/share/xfce4/backdrops/bg-wp-web-ver.png
theme-name = Working-Theme-Greet
icon-theme-name = Paper
font-name = URW Gothic L Demi 11
position = 35%,end 50%,center
theme = Working-Theme-Greet
```

## Memulai mengganti logo tealinuxos saat ubiquity ##

- sudah ada logonya

- copy and replace `tmp/remaster-root/usr/share/ubiquity/pixmaps/ubuntu_installed.png`

- kemudian selesai

## Mulai bingung ##

- edit file `tmp/remaster-root/usr/share/applications/exo-file-manager.desktop`

- pastikan sama

```shell
Exec=nautilus
Icon=system-file-manager
StartupNotify=true
```

## Memeulai mengganti background grub ##

- siapkan gambar

- dan kemudian edit file `tmp/remaster-root/etc/grub.d/05_debian_theme`

- kemudian edit dibagian

```shell
if set_background_image "/usr/share/xfce4/backdrops/bg-wp-web-ver.png"; then
			exit 0
		fi
		;;
```

- edit yang paling bawah


## Memulai setting mime ##

- buka di `tmp/remaster-root/usr/share/applications/mimeinfo.cache`

- cari `inode/directory=` ganti menjadi `nautilus.desktop`

- kemudian save

## Memulai menambah bingung ##

- buka `tmp/remaster-root/usr/share/python-apt/templates/`

- kemudian copy file `Ubuntu.info` menjadi `TeaLinuxOS.info`

- kemudian copy file `Ubuntu.mirrors` menjadi `TeaLinuxOS.mirrors`

- edit beberapa line di `TeaLinuxOS.info`

```shell 
RepositoryType: deb
BaseURI: http://studio.tealinuxos.org/ubuntu/
MatchURI: studio.tealinuxos.org/ubuntu/
BaseURI-amd64: http://studio.tealinuxos.org/module/debs/
MatchURI-amd64: studio.tealinuxos.org/module/debs/
BaseURI-i386: http://studio.tealinuxos.org/module/debs/
MatchURI-i386: studio.tealinuxos.org/module/debs/
MirrorsFile-amd64: TeaLinuxOS.mirrors
MirrorsFile-i386: TeaLinuxOS.mirrors
Description: TeaLinuxOS for developing environtment
```

- kemudian edit file `TeaLinuxOS.mirrors`

- tambahkan

```shell
#LOC:ID
http://studio.tealinuxos.org/ubuntu/
```

## Memulai install modularitea ##

- pertama install dulu npm

- caranya install bisa lihat di https://nodejs.org/en/download/package-manager/#debian-and-ubuntu-based-linux-distributions

- atau langsung saja

```
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
apt-get install -y nodejs
```

- kemudian masuk di folder `tmp/remaster-root/usr/share/`

```
git clone https://github.com/tealinuxos/modularitea.git
chmod 777 -R modularitea/
cd modularitea/gui-electron/
npm i
cd ..
```

- jika sudah bikin file `runmodularitea` dan isinya

```
#!/bin/sh

cd /usr/share/modularitea/gui-electron/
npm run dev
```

- jika sudah bikin shortcut `tmp/remaster-root/usr/share/applications/modularitea.desktop`

- dengan isinya

```
[Desktop Entry]
Name=Modularitea
GenericName=Modularitea
Comment=Modularitea merupakan aplikasi yang dapat memasang lingkungan kerja untuk para pengembang hanya dengan beberapa langkah sederhana. Modularitea menyederhanakan proses cari, unduh, pasang dan ubahsuai ke dalam bentuk modul.
Exec=/usr/share/modularitea/runmodularitea
Icon=/usr/share/icons/modularitea.png
Terminal=false
Type=Application
Categories=GNOME;GTK;Core;Development;Utility;XFCE;Settings;X-XFCE-SettingsDialog;
```

- jika sudah save
