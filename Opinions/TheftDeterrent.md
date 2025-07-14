# I need to run malware on my laptop so it can keep booting.

This "malware" is made by Intel and forced by the local government, with the warning "if you don't run this program your computer will block itself" (which was actually true) and don't allow students to wipe the disk in order for this program to keep running. Of course, you can easily install a different OS (which is what I did) and install the program there and it will work perfectly fine (assuming there are no problems with dependencies).

I currently installed Arch Linux, which isn't compatible with this program because it is only for Debian and Debian-based distros like Huayra, which is the distro that not only came pre-installed in this computer but also included the program I'm calling "malware". I tried forcing the install of this program, and while it does run the systemd daemon, it doesn't launch the GUI app, it straight up doesn't work. So I don’t know if the program, the thing that keeps my netbook unlocked, is actually enabled and properly configured.

## Debian

I was able to install this program without any problem in any distro based on Debian 10 and 11, including Huayra 5 (based on Debian 10.13) and Huayra 6 (Debian 11). But Debian 12 removed the python>=2.7 package, I decided to remove that dependency from the manifest and the program would run flawlessly. Then I tried making a fake python=2.7 package, installing it and then installing TDA; that also worked.

The program came bundled in 4 different packages, I manually downloaded them from the original repositories and reuploaded them to my own server.

> https://jotalea.com.ar/files/theftdeterrentguardian_6.0.0.11.huayra10_amd64.deb
> https://jotalea.com.ar/files/theftdeterrentdaemon_6.0.0.11.huayra10_amd64.deb
> https://jotalea.com.ar/files/theftdeterrentclient_6.0.0.11.huayra10_amd64.deb
> https://jotalea.com.ar/files/theftdeterrentclient-lib_6.0.0.11.huayra10_amd64.deb

And, just in case, I made a GitHub repository to save the files there too

> https://github.com/Jotalea/TheftDeterrent

## File structure

I extracted the content of all 4 .deb files and put them in the place they belong

```bash
$ tree
/
├── etc
│   └── NetworkManager
│       └── conf.d
│           └── theft-disable-random-mac.conf
├── lib
│   └── systemd
│       └── system
│           ├── theftdeterrent-agent.service
│           ├── theftdeterrent-guardian.service
│           └── theftdeterrent-tpmdaemon.service
├── opt
│   └── TheftDeterrentclient
│       ├── client
│       │   ├── bitmaps
│       │   │   ├── About_BG.png
│       │   │   ├── icon_warning_l.png
│       │   │   ├── icon_warning_m.png
│       │   │   ├── icon_warn_m.png
│       │   │   ├── LogoAbout.png
│       │   │   ├── LogoProtected_l.png
│       │   │   ├── LogoTitle.png
│       │   │   ├── main_wnd.png
│       │   │   ├── status
│       │   │   │   ├── LogoAbouttoExpire_l.png
│       │   │   │   ├── LogoAbouttoExpire_m.png
│       │   │   │   ├── LogoAbouttoExpire_s.png
│       │   │   │   ├── LogoDisconnectedActive_l.png
│       │   │   │   ├── LogoDisconnectedActive_m.png
│       │   │   │   ├── LogoDisconnectedActive_s.png
│       │   │   │   ├── LogoDisconnectedInactive_l.png
│       │   │   │   ├── LogoDisconnectedInactive_m.png
│       │   │   │   ├── LogoDisconnectedInactive_s.png
│       │   │   │   ├── LogoDownload_l.png
│       │   │   │   ├── LogoDownload_m.png
│       │   │   │   ├── LogoDownload_s.png
│       │   │   │   ├── LogoInctive_l.png
│       │   │   │   ├── LogoInctive_m.png
│       │   │   │   ├── LogoInctive_s.png
│       │   │   │   ├── LogoInstall_l.png
│       │   │   │   ├── LogoInstall_m.png
│       │   │   │   ├── LogoInstall_s.png
│       │   │   │   ├── LogoPermanent_l.png
│       │   │   │   ├── LogoPermanent_m.png
│       │   │   │   ├── LogoPermanent_s.png
│       │   │   │   ├── LogoProtected_l.png
│       │   │   │   ├── LogoProtected_m.png
│       │   │   │   ├── LogoProtected_s.png
│       │   │   │   ├── LogoUnknown_l.png
│       │   │   │   ├── LogoUnknown_m.png
│       │   │   │   └── LogoUnknown_s.png
│       │   │   ├── test
│       │   │   │   ├── icon_error_l.png
│       │   │   │   ├── icon_error_m.png
│       │   │   │   ├── icon_success_l.png
│       │   │   │   ├── icon_success_m.png
│       │   │   │   ├── loading_animation_l.gif
│       │   │   │   └── loading_animation_m.gif
│       │   │   └── trayicon
│       │   │       ├── TrayIconAboutToExpire.ico
│       │   │       ├── TrayIconDisconnectActive.ico
│       │   │       ├── TrayIconDisconnectInactive.ico
│       │   │       ├── TrayIconDownloading.ico
│       │   │       ├── TrayIconInactive.ico
│       │   │       ├── TrayIconPermanent.ico
│       │   │       ├── TrayIconProtected.ico
│       │   │       ├── TrayIconUnknown.ico
│       │   │       └── TrayIconUpgrading.ico
│       │   ├── extensions
│       │   │   └── TheftDeterrent_client_Extension
│       │   │       ├── extension.js
│       │   │       ├── icon
│       │   │       │   ├── LogoAbouttoExpire_m.png
│       │   │       │   ├── LogoAbouttoExpire_s.png
│       │   │       │   ├── LogoDisconnectedActive_m.png
│       │   │       │   ├── LogoDisconnectedActive_s.png
│       │   │       │   ├── LogoDisconnectedInactive_m.png
│       │   │       │   ├── LogoDisconnectedInactive_s.png
│       │   │       │   ├── LogoDownload_m.png
│       │   │       │   ├── LogoDownload_s.png
│       │   │       │   ├── LogoInctive_m.png
│       │   │       │   ├── LogoInctive_s.png
│       │   │       │   ├── LogoInstall_m.png
│       │   │       │   ├── LogoInstall_s.png
│       │   │       │   ├── LogoPermanent_m.png
│       │   │       │   ├── LogoPermanent_s.png
│       │   │       │   ├── LogoProtected_m.png
│       │   │       │   ├── LogoProtected_s.png
│       │   │       │   ├── LogoUnknown_m.png
│       │   │       │   └── LogoUnknown_s.png
│       │   │       ├── metadata.json
│       │   │       └── stylesheet.css
│       │   ├── help
│       │   │   ├── help.css
│       │   │   ├── help.js
│       │   │   ├── img
│       │   │   │   ├── English
│       │   │   │   │   ├── image002.jpg
│       │   │   │   │   ├── image004.jpg
│       │   │   │   │   ├── image006.jpg
│       │   │   │   │   ├── image007.jpg
│       │   │   │   │   └── image008.jpg
│       │   │   │   ├── image001.jpg
│       │   │   │   ├── image003.jpg
│       │   │   │   ├── image005.jpg
│       │   │   │   ├── image009.jpg
│       │   │   │   ├── image010.jpg
│       │   │   │   ├── image011.jpg
│       │   │   │   ├── image012.jpg
│       │   │   │   ├── image013.jpg
│       │   │   │   ├── image014.jpg
│       │   │   │   ├── minus.gif
│       │   │   │   ├── plus.gif
│       │   │   │   ├── Portuguese
│       │   │   │   │   ├── image002.jpg
│       │   │   │   │   ├── image004.jpg
│       │   │   │   │   ├── image006.jpg
│       │   │   │   │   ├── image007.jpg
│       │   │   │   │   └── image008.jpg
│       │   │   │   ├── Spanish
│       │   │   │   │   ├── image002.jpg
│       │   │   │   │   ├── image004.jpg
│       │   │   │   │   ├── image006.jpg
│       │   │   │   │   ├── image007.jpg
│       │   │   │   │   └── image008.jpg
│       │   │   │   ├── Turkish
│       │   │   │   │   ├── image002.jpg
│       │   │   │   │   ├── image004.jpg
│       │   │   │   │   ├── image006.jpg
│       │   │   │   │   ├── image007.jpg
│       │   │   │   │   └── image008.jpg
│       │   │   │   └── Vietnam
│       │   │   │       ├── image002.jpg
│       │   │   │       ├── image004.jpg
│       │   │   │       ├── image006.jpg
│       │   │   │       ├── image007.jpg
│       │   │   │       └── image008.jpg
│       │   │   ├── main_en-US.html
│       │   │   ├── main_es-MX.html
│       │   │   ├── main_pt-BR.html
│       │   │   ├── main_tr-TR.html
│       │   │   ├── main_vi-VN.html
│       │   │   └── VERSION
│       │   ├── icon
│       │   │   ├── LogoAbouttoExpire_m.png
│       │   │   ├── LogoAbouttoExpire_s.png
│       │   │   ├── LogoDisconnectedActive_m.png
│       │   │   ├── LogoDisconnectedActive_s.png
│       │   │   ├── LogoDisconnectedInactive_m.png
│       │   │   ├── LogoDisconnectedInactive_s.png
│       │   │   ├── LogoDownload_m.png
│       │   │   ├── LogoDownload_s.png
│       │   │   ├── LogoInctive_m.png
│       │   │   ├── LogoInctive_s.png
│       │   │   ├── LogoInstall_m.png
│       │   │   ├── LogoInstall_s.png
│       │   │   ├── LogoPermanent_m.png
│       │   │   ├── LogoPermanent_s.png
│       │   │   ├── LogoProtected_m.png
│       │   │   ├── LogoProtected_s.png
│       │   │   ├── LogoUnknown_m.png
│       │   │   └── LogoUnknown_s.png
│       │   ├── lib.tar.gz
│       │   ├── locale
│       │   │   ├── en
│       │   │   │   └── LC_MESSAGES
│       │   │   │       └── tdclient.mo
│       │   │   ├── es
│       │   │   │   └── LC_MESSAGES
│       │   │   │       └── tdclient.mo
│       │   │   ├── pt
│       │   │   │   └── LC_MESSAGES
│       │   │   │       └── tdclient.mo
│       │   │   ├── tr
│       │   │   │   └── LC_MESSAGES
│       │   │   │       └── tdclient.mo
│       │   │   └── vi
│       │   │       └── LC_MESSAGES
│       │   │           └── tdclient.mo
│       │   ├── Theft_Deterrent_agent
│       │   ├── TheftDeterrentclient
│       │   │   ├── atk.so
│       │   │   ├── bz2.so
│       │   │   ├── cairo._cairo.so
│       │   │   ├── _codecs_cn.so
│       │   │   ├── _codecs_hk.so
│       │   │   ├── _codecs_iso2022.so
│       │   │   ├── _codecs_jp.so
│       │   │   ├── _codecs_kr.so
│       │   │   ├── _codecs_tw.so
│       │   │   ├── _ctypes.so
│       │   │   ├── _dbus_bindings.so
│       │   │   ├── _dbus_glib_bindings.so
│       │   │   ├── gdk-pixbuf-2.0
│       │   │   │   └── loaders.cache
│       │   │   ├── gio._gio.so
│       │   │   ├── gio.unix.so
│       │   │   ├── glib._glib.so
│       │   │   ├── gobject._gobject.so
│       │   │   ├── gtk-2.0
│       │   │   │   └── immodules.cache
│       │   │   ├── gtk._gtk.so
│       │   │   ├── _hashlib.so
│       │   │   ├── im-fcitx.so
│       │   │   ├── im-ibus.so
│       │   │   ├── libatk-1.0.so.0
│       │   │   ├── libbz2.so.1.0
│       │   │   ├── libcairo.so.2
│       │   │   ├── libcrypto.so.1.0.0
│       │   │   ├── libdatrie.so.1
│       │   │   ├── libdbus-1.so.3
│       │   │   ├── libdbus-glib-1.so.2
│       │   │   ├── libexpat.so.1
│       │   │   ├── libfcitx-gclient.so.0
│       │   │   ├── libfcitx-utils.so.0
│       │   │   ├── libffi.so.6
│       │   │   ├── libfontconfig.so.1
│       │   │   ├── libfreetype.so.6
│       │   │   ├── libgcc_s.so.1
│       │   │   ├── libgcrypt.so.20
│       │   │   ├── libgdk_pixbuf-2.0.so.0
│       │   │   ├── libgdk-x11-2.0.so.0
│       │   │   ├── libgio-2.0.so.0
│       │   │   ├── libglib-2.0.so.0
│       │   │   ├── libgmodule-2.0.so.0
│       │   │   ├── libgobject-2.0.so.0
│       │   │   ├── libgpg-error.so.0
│       │   │   ├── libgraphite2.so.3
│       │   │   ├── libgthread-2.0.so.0
│       │   │   ├── libgtk-x11-2.0.so.0
│       │   │   ├── libharfbuzz.so.0
│       │   │   ├── libibus-1.0.so.5
│       │   │   ├── libICE.so.6
│       │   │   ├── libjbig.so.0
│       │   │   ├── libjpeg.so.8
│       │   │   ├── liblzma.so.5
│       │   │   ├── libnotify.so.4
│       │   │   ├── libpango-1.0.so.0
│       │   │   ├── libpangocairo-1.0.so.0
│       │   │   ├── libpangoft2-1.0.so.0
│       │   │   ├── libpcre.so.3
│       │   │   ├── libpixbufloader-bmp.so
│       │   │   ├── libpixbufloader-gif.so
│       │   │   ├── libpixbufloader-png.so
│       │   │   ├── libpixman-1.so.0
│       │   │   ├── libpng12.so.0
│       │   │   ├── libpyglib-2.0-python2.7.so.0
│       │   │   ├── libpython2.7.so.1.0
│       │   │   ├── libreadline.so.6
│       │   │   ├── libselinux.so.1
│       │   │   ├── libSM.so.6
│       │   │   ├── libssl.so.1.0.0
│       │   │   ├── libstdc++.so.6
│       │   │   ├── libsystemd.so.0
│       │   │   ├── libthai.so.0
│       │   │   ├── libtiff.so.5
│       │   │   ├── libtinfo.so.5
│       │   │   ├── libuuid.so.1
│       │   │   ├── libwx_baseu-3.0.so.0
│       │   │   ├── libwx_baseu_net-3.0.so.0
│       │   │   ├── libwx_gtk2u_adv-3.0.so.0
│       │   │   ├── libwx_gtk2u_core-3.0.so.0
│       │   │   ├── libwx_gtk2u_html-3.0.so.0
│       │   │   ├── libX11.so.6
│       │   │   ├── libXau.so.6
│       │   │   ├── libxcb-render.so.0
│       │   │   ├── libxcb-shm.so.0
│       │   │   ├── libxcb.so.1
│       │   │   ├── libXcomposite.so.1
│       │   │   ├── libXcursor.so.1
│       │   │   ├── libXdamage.so.1
│       │   │   ├── libXdmcp.so.6
│       │   │   ├── libXext.so.6
│       │   │   ├── libXfixes.so.3
│       │   │   ├── libXinerama.so.1
│       │   │   ├── libXi.so.6
│       │   │   ├── libxkbcommon.so.0
│       │   │   ├── libXrandr.so.2
│       │   │   ├── libXrender.so.1
│       │   │   ├── libXxf86vm.so.1
│       │   │   ├── libz.so.1
│       │   │   ├── _multibytecodec.so
│       │   │   ├── out00-PYZ.pyz
│       │   │   ├── pangocairo.so
│       │   │   ├── pango.so
│       │   │   ├── psutil._psutil_linux.so
│       │   │   ├── psutil._psutil_posix.so
│       │   │   ├── pyexpat.so
│       │   │   ├── pyiboot01_bootstrap
│       │   │   ├── pyimod01_os_path
│       │   │   ├── pyimod02_archive
│       │   │   ├── pyimod03_importers
│       │   │   ├── pynotify._pynotify.so
│       │   │   ├── readline.so
│       │   │   ├── resource.so
│       │   │   ├── _ssl.so
│       │   │   ├── struct
│       │   │   ├── termios.so
│       │   │   ├── thrift.protocol.fastbinary.so
│       │   │   ├── wx._animate.so
│       │   │   ├── wx._controls_.so
│       │   │   ├── wx._core_.so
│       │   │   ├── wx._gdi_.so
│       │   │   ├── wx._misc_.so
│       │   │   └── wx._windows_.so
│       │   ├── Theft_Deterrent_client.autorun
│       │   ├── theftdeterrentclient.desktop
│       │   ├── Theft_Deterrent_client.png
│       │   ├── Theft_Deterrent_client.run
│       │   └── Theft_Deterrent_client_statusicon.app
│       └── guardian
│           └── Theft_Deterrent_guardian
└── usr
    ├── local
    │   ├── theftdeterrentclient
    │   │   ├── client
    │   │   │   ├── service_start
    │   │   │   ├── service_status
    │   │   │   ├── service_stop
    │   │   │   └── theftdeterrentagent
    │   │   └── guardian
    │   │       ├── funcdefine
    │   │       ├── funcguardian
    │   │       ├── funcreturn
    │   │       ├── funcutil
    │   │       ├── LANG_0
    │   │       ├── LANG_1
    │   │       ├── LANG_2
    │   │       ├── LANG_3
    │   │       ├── LANG_4
    │   │       ├── LANG_5
    │   │       ├── LANG_6
    │   │       ├── service_start
    │   │       ├── service_status
    │   │       ├── service_stop
    │   │       └── theftdeterrentguardian
    │   └── theftdeterrentdaemon
    │       ├── funcdaemon
    │       ├── funcdefine
    │       ├── funcreturn
    │       ├── funcutil
    │       ├── service_start
    │       ├── service_status
    │       ├── service_stop
    │       └── tpmdaemon
    ├── sbin
    │   └── tpmdaemon
    └── share
        ├── applications
        │   └── theftdeterrentclient.desktop
        ├── doc
        │   ├── theftdeterrentclient
        │   │   ├── changelog.gz
        │   │   └── copyright
        │   ├── theftdeterrentclient-lib
        │   │   ├── changelog.gz
        │   │   └── copyright
        │   ├── theftdeterrentdaemon
        │   │   ├── changelog.gz
        │   │   └── copyright
        │   └── theftdeterrentguardian
        │       ├── changelog.gz
        │       └── copyright
        └── theftdeterrentclient
            ├── theftdeterrentclient.funcagent
            ├── theftdeterrentclient.funcagentui
            ├── theftdeterrentclient.funcdaemon
            ├── theftdeterrentclient.funcdefine
            ├── theftdeterrentclient.funcreturn
            ├── theftdeterrentclient.funcutil
            ├── theftdeterrentclient.LANG_0
            ├── theftdeterrentclient.LANG_1
            ├── theftdeterrentclient.LANG_2
            ├── theftdeterrentclient.LANG_3
            ├── theftdeterrentclient.LANG_4
            ├── theftdeterrentclient.LANG_5
            ├── theftdeterrentclient.LANG_6
            ├── theftdeterrentdaemon.funcdaemon
            ├── theftdeterrentdaemon.funcdefine
            ├── theftdeterrentdaemon.funcreturn
            ├── theftdeterrentdaemon.funcutil
            ├── theftdeterrentguardian.funcdefine
            ├── theftdeterrentguardian.funcguardian
            ├── theftdeterrentguardian.funcreturn
            ├── theftdeterrentguardian.funcutil
            ├── theftdeterrentguardian.LANG_0
            ├── theftdeterrentguardian.LANG_1
            ├── theftdeterrentguardian.LANG_2
            ├── theftdeterrentguardian.LANG_3
            ├── theftdeterrentguardian.LANG_4
            ├── theftdeterrentguardian.LANG_5
            └── theftdeterrentguardian.LANG_6

55 directories, 340 files
```

Hmm, there is the .desktop file that DEs use for launching the app, let me check them

```bash
$ cat /usr/share/applications/theftdeterrentclient.desktop
[Desktop Entry]
Name=Theft Deterrent client
Exec=/opt/TheftDeterrentclient/client/Theft_Deterrent_client.run
Icon=/opt/TheftDeterrentclient/client/Theft_Deterrent_client.png
Terminal=false
Type=Application
Categories=System;
X-GNOME-Autostart-enabled=true
X-KDE-autostart-phase=1
```

So, it runs `/opt/TheftDeterrentclient/client/Theft_Deterrent_client.run`, is that a binary?

```
$ cat /opt/TheftDeterrentclient/client/Theft_Deterrent_client.run
#! /bin/sh

apppath=/opt/TheftDeterrentclient/client
appfile=TheftDeterrentclient

#chmod +x ${apppath}/${appfile} > /dev/null 2>&1

LC_ALL=C LANG=C ${apppath}/${appfile} > /dev/null 2>&1%   
```

No, it is a script, it enables execution of and runs /opt/TheftDeterrentclient/client/TheftDeterrentclient, that must be a script, right?

```bash
$ cat /opt/TheftDeterrentclient/client/TheftDeterrentclient
cat: /opt/TheftDeterrentclient/client/TheftDeterrentclient: It's a directory
```

Huh?? Why would it chmod a directory? Oh wait, it is not changing the mode because that line is commented in the script, so it is directly trying to run it. But wait, it is a directory, let me see what is inside it

```bash
$ ls /opt/TheftDeterrentclient/client/TheftDeterrentclient
atk.so                  libgmodule-2.0.so.0           libxcb-render.so.0
bz2.so                  libgobject-2.0.so.0           libxcb-shm.so.0
cairo._cairo.so         libgpg-error.so.0             libxcb.so.1
_codecs_cn.so           libgraphite2.so.3             libXcomposite.so.1
_codecs_hk.so           libgthread-2.0.so.0           libXcursor.so.1
_codecs_iso2022.so      libgtk-x11-2.0.so.0           libXdamage.so.1
_codecs_jp.so           libharfbuzz.so.0              libXdmcp.so.6
_codecs_kr.so           libibus-1.0.so.5              libXext.so.6
_codecs_tw.so           libICE.so.6                   libXfixes.so.3
_ctypes.so              libjbig.so.0                  libXinerama.so.1
_dbus_bindings.so       libjpeg.so.8                  libXi.so.6
_dbus_glib_bindings.so  liblzma.so.5                  libxkbcommon.so.0
gdk-pixbuf-2.0          libnotify.so.4                libXrandr.so.2
gio._gio.so             libpango-1.0.so.0             libXrender.so.1
gio.unix.so             libpangocairo-1.0.so.0        libXxf86vm.so.1
glib._glib.so           libpangoft2-1.0.so.0          libz.so.1
gobject._gobject.so     libpcre.so.3                  _multibytecodec.so
gtk-2.0                 libpixbufloader-bmp.so        out00-PYZ.pyz
gtk._gtk.so             libpixbufloader-gif.so        pangocairo.so
_hashlib.so             libpixbufloader-png.so        pango.so
im-fcitx.so             libpixman-1.so.0              psutil._psutil_linux.so
im-ibus.so              libpng12.so.0                 psutil._psutil_posix.so
libatk-1.0.so.0         libpyglib-2.0-python2.7.so.0  pyexpat.so
libbz2.so.1.0           libpython2.7.so.1.0           pyiboot01_bootstrap
libcairo.so.2           libreadline.so.6              pyimod01_os_path
libcrypto.so.1.0.0      libselinux.so.1               pyimod02_archive
libdatrie.so.1          libSM.so.6                    pyimod03_importers
libdbus-1.so.3          libssl.so.1.0.0               pynotify._pynotify.so
libdbus-glib-1.so.2     libstdc++.so.6                readline.so
libexpat.so.1           libsystemd.so.0               resource.so
libfcitx-gclient.so.0   libthai.so.0                  _ssl.so
libfcitx-utils.so.0     libtiff.so.5                  struct
libffi.so.6             libtinfo.so.5                 termios.so
libfontconfig.so.1      libuuid.so.1                  thrift.protocol.fastbinary.so
libfreetype.so.6        libwx_baseu-3.0.so.0          wx._animate.so
libgcc_s.so.1           libwx_baseu_net-3.0.so.0      wx._controls_.so
libgcrypt.so.20         libwx_gtk2u_adv-3.0.so.0      wx._core_.so
libgdk_pixbuf-2.0.so.0  libwx_gtk2u_core-3.0.so.0     wx._gdi_.so
libgdk-x11-2.0.so.0     libwx_gtk2u_html-3.0.so.0     wx._misc_.so
libgio-2.0.so.0         libX11.so.6                   wx._windows_.so
libglib-2.0.so.0        libXau.so.6
```

But these are all libraries, aren't they?

There is another .desktop file, let me see

```bash
$ cat /opt/TheftDeterrentclient/client/theftdeterrentclient.desktop
[Desktop Entry]
Name=Theft Deterrent client
Exec=/opt/TheftDeterrentclient/client/Theft_Deterrent_client.autorun
Icon=/opt/TheftDeterrentclient/client/Theft_Deterrent_client.png
Terminal=false
Type=Application
Categories=System;
X-GNOME-Autostart-enabled=true
X-KDE-autostart-phase=1
```

This one is different, it runs /opt/TheftDeterrentclient/client/Theft_Deterrent_client.autorun instead of /opt/TheftDeterrentclient/client/Theft_Deterrent_client.run; let me see what does it contain

```bash
$ cat /opt/TheftDeterrentclient/client/Theft_Deterrent_client.autorun
#!/bin/bash

startup_dir=.config/autostart
desktop_file=theftdeterrentclient.desktop
apppath=/opt/TheftDeterrentclient/client
appfile=TheftDeterrentclient
extension_dir=TheftDeterrent_client_Extension

print_verbose_log=$1
ishidden=$2
cur_process=$$

if [ "x${print_verbose_log}" = "x-v" ] ; then
    ui_log_file=/tmp/TDClientUI_${cur_process}.log
else
    #ui_log_file=/tmp/TDClientUI_${cur_process}.log
    ui_log_file=/dev/null
fi

hideflag="--hide"
if [ "x${ishidden}" = "xshow" ] ; then
    hideflag=""
elif [ "x${ishidden}" = "xhide" ] ; then
    hideflag="--hide"
fi

fn_execute()
{
    #chmod +x ${apppath}/${appfile} > /dev/null 2>&1

    tmp_str=`dirname  "$0"`
    if [ "${tmp_str:0:1}" = "." ]; then
        run_top_dir=`pwd`${tmp_str:1}
    else
        if [ "${tmp_str:0:1}" = "/" ]; then
            run_top_dir=${tmp_str}
        else
            run_top_dir=`pwd`/${tmp_str}
        fi
    fi

    echo immodules.cache=${run_top_dir}/gtk-2.0/immodules.cache >> ${ui_log_file} 2>&1
#xun+,why,please see "3rd-lib.build/src_orig/ReadMe_3rd-lib.txt,2018.02.18
    export GTK_IM_MODULE_FILE=${run_top_dir}/gtk-2.0/immodules.cache
#xun+,why,please see "3rd-lib.build/src_orig/ReadMe_3rd-lib.txt,2018.02.18,end
    echo "run"  >> ${ui_log_file} 2>&1
    date  >> ${ui_log_file} 2>&1
    LC_ALL=C LANG=C ${apppath}/${appfile} ${hideflag} >> ${ui_log_file} 2>&1
    date  >> ${ui_log_file} 2>&1
    echo end  >> ${ui_log_file} 2>&1
}

fn_register()
{
    home_folder=$(eval echo ~${SUDO_USER})
    if [ ! -f "${home_folder}/${startup_dir}/${desktop_file}" ]; then
        echo "${home_folder}/${startup_dir}/${desktop_file} not fount,creat it" >> ${ui_log_file} 2>&1
        mkdir -p ${home_folder}/${startup_dir} >> ${ui_log_file} 2>&1
        ln -s ${apppath}/${desktop_file} ${home_folder}/${startup_dir}/${desktop_file} > /dev/null 2>&1
    else
        echo "${home_folder}/${startup_dir}/${desktop_file} is OK" >> ${ui_log_file} 2>&1
    fi

    gnome-shell --version >> ${ui_log_file} 2>&1
    gnome_shell_err=$?
    echo gnome_shell_err=${gnome_shell_err} >> ${ui_log_file} 2>&1
    if [ ${gnome_shell_err} -eq 0 ]; then
        # Register extension
        _existext_str=`LANG=C gsettings get org.gnome.shell enabled-extensions`
        echo _existext_str=-${_existext_str}-  >> ${ui_log_file} 2>&1
        _existext=`echo ${_existext_str} | grep -w "${extension_dir}"`
        _null__existext=`echo ${_existext_str}  | grep -w "\[\]"`
        echo _null__existext=${_null__existext}  >> ${ui_log_file} 2>&1
        if [ "x${_existext_str}" = "x" ] ; then
        	_existext="['${extension_dir}']"
	   else
           	if [ "x${_null__existext}" = "x" ] ; then    
                if [ "x${_existext}" = "x" ] ; then    
                    tmp_r=${_existext_str%%"]"}
                    echo "_existext_str=-${_existext_str}-"  >> ${ui_log_file} 2>&1
                    echo "tmp_r=-${tmp_r}-"  >> ${ui_log_file} 2>&1
	          	   _existext="${tmp_r}, '${extension_dir}']"
                fi
	       else
                _existext="['${extension_dir}']"
          	fi
        fi
        echo "_existext=-${_existext}-"  >> ${ui_log_file} 2>&1
        LANG=C nohup gsettings set org.gnome.shell enabled-extensions "${_existext}" > /dev/null 2>&1 &
    else #if [ ${gnome_shell_err} -eq 0 ]
        echo "gnome-shell not found"  >> ${ui_log_file} 2>&1
    fi #if [ ${gnome_shell_err} -eq 0 ]

    # Ubuntu support
    #LANG=C nohup gsettings set com.canonical.Unity.Panel systray-whitelist "['all']" > /dev/null 2>&1 &
}

fn_register
fn_execute
```

Now this is more interesting, let's see what happens if I run it
```bash
$ /opt/TheftDeterrentclient/client/Theft_Deterrent_client.autorun

/opt/TheftDeterrentclient/client/TheftDeterrentclient $ 
```

Nope, it closes instantly and doesn't show any errors.

```bash
$ /opt/TheftDeterrentclient/client/Theft_Deterrent_agent
=============Hello, Agent================

/opt/TheftDeterrentclient/client $ 
```

```bash
$ ldd /opt/TheftDeterrentclient/client/Theft_Deterrent_agent
	linux-vdso.so.1 (0x00007fafc2a83000)
	libpthread.so.0 => /usr/lib/libpthread.so.0 (0x00007fafc2a48000)
	libdl.so.2 => /usr/lib/libdl.so.2 (0x00007fafc2a43000)
	librt.so.1 => /usr/lib/librt.so.1 (0x00007fafc2a3e000)
	libm.so.6 => /usr/lib/libm.so.6 (0x00007fafc2946000)
	libgcc_s.so.1 => /usr/lib/libgcc_s.so.1 (0x00007fafc2919000)
	libc.so.6 => /usr/lib/libc.so.6 (0x00007fafc2729000)
	/lib64/ld-linux-x86-64.so.2 => /usr/lib64/ld-linux-x86-64.so.2 (0x00007fafc2a85000)
$ ldd /opt/TheftDeterrentclient/client/Theft_Deterrent_client.autorun
	no es un ejecutable dinámico
$ ldd /opt/TheftDeterrentclient/client/theftdeterrentclient.desktop
ldd: atención: no tiene permiso de ejecución para `/opt/TheftDeterrentclient/client/theftdeterrentclient.desktop'
	no es un ejecutable dinámico
$ ldd /opt/TheftDeterrentclient/client/Theft_Deterrent_client.run
	no es un ejecutable dinámico
$ ldd /opt/TheftDeterrentclient/client/Theft_Deterrent_client_statusicon.app
	linux-vdso.so.1 (0x00007f46d4a4b000)
	libdl.so.2 => /usr/lib/libdl.so.2 (0x00007f46d4a10000)
	libz.so.1 => /usr/lib/libz.so.1 (0x00007f46d49f7000)
	libc.so.6 => /usr/lib/libc.so.6 (0x00007f46d4807000)
	/lib64/ld-linux-x86-64.so.2 => /usr/lib64/ld-linux-x86-64.so.2 (0x00007f46d4a4d000)
```
