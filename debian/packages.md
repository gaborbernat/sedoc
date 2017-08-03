Debian Package Information
==========================

### Quick Info

To make available the standard extra stuff, add `contrib` and
`non-free` to the lines in `/etc/apt/sources.list`. (Remember to
`apt-get update` after.) The most commonly wanted packages are:

* `firmware-iwlwifi`: Thinkpad and other Intel WiFi chips
* `firmware-linux-nonfree`: general stuff


Repository Configuration Format
-------------------------------

The package repositories (remote and local) are listed in

    /etc/apt/sources.list
    /etc/apt/sources.list.d/*.{list,sources}

where `*` is `[A-Za-z0-9._-]`. `.list` is the one-line format;
`.sources` is the deb822 (multiline) format. Both are decribed in the
`sources.list(5)` manpage.

### One-line Format

Sources are listed from most to less preferred.

    deb|deb-src [opt=val opt=val] uri suite component...

1. `deb` or `deb-src`. Normally there will be a pair of otherwise
   identical lines starting with each.
2. `uri` can be the base of the distro or an exact path. Not clear on
   details. Examples:
3. `suite`: Examples include `stretch`, `stretch/updates`, 
4. `component`: The standard seems to be `main`, plus optional `contrib`
    and `non-free`.

#### Debian 9 Standard `sources.list`

From an install started with non-free components:

    #deb    cdrom:[Debian GNU/Linux 9.0.0 _Stretch_ - Official amd64 NETINST 20170617-13:06]/ stretch contrib main non-free

    deb	    http://ftp.jp.debian.org/debian/            stretch             main non-free contrib
    deb-src http://ftp.jp.debian.org/debian/            stretch             main non-free contrib

    deb     http://security.debian.org/debian-security  stretch/updates     main contrib non-free
    deb-src http://security.debian.org/debian-security  stretch/updates     main contrib non-free

    # stretch-updates, previously known as 'volatile'
    deb     http://ftp.jp.debian.org/debian/            stretch-updates     main contrib non-free
    deb-src http://ftp.jp.debian.org/debian/            stretch-updates     main contrib non-free

    # stretch-backports, previously on backports.debian.org
    deb     http://ftp.jp.debian.org/debian/            stretch-backports   main contrib non-free
    deb-src http://ftp.jp.debian.org/debian/            stretch-backports   main contrib non-free