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
