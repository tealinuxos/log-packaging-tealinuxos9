Log packaging tealinuxos 9 i386
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

- kemudian catat semua aplikasi yang ada satu persatu

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


