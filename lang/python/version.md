Python Versions
===============

Python's reference implementation is the [CPython] interpreter.
There are two major versions:
* 2.7 (2010): [legacy], supported until 2020 (latest 2.7.13 2016-12)
* 3.6.3 (2017-10): current (3.7 releasing 2018-06)

On almost all systems `/usr/bin/python3` is present if Python 3 is
installed. It's almost never installed as part of the base system.

On most systems `/usr/bin/python` will be Python 2 unless the sysadmin
has explicitly selected otherwise. Red Hat flavour systems include
Python 2 as part of the base system; on other systems many packages
(over a thousand non-Python ones on Debian) require it and many more
recommend it.

#### OS/Distro Version Reference

| OS/Distro     | `python`  |`python3`  | Distro Release Date
|---------------|-----------|-----------|----------------------
| Ubuntu 18.04  | 2.7.14+   | 3.6.4+    | 2018-04
| Debian 9      | 2.7.13    | 3.5.3     | 2017-06
| Ubuntu 16.04  | 2.7.12    | 3.5.2     | 2016-04
| Debian 8      | 2.7.9     | 3.4.2     | 2015-05
| CentOS 7      | 2.7.5 [1] | [2]       | 2014-06
| Ubuntu 14.04  | 2.7.6     | 3.4.3     | 2014-04
| Debian 7      | 2.7.3     | 3.2.3     | 2013-05
| Ubuntu 12.04  | 2.7.3     | 3.2.3     | 2012-04 x
| CentOS 6      | 2.6.6 [1] | [2]       | 2011-06 x
| Debian 6      | ?         | ?         | 2011-02 x
| Ubuntu 10.04  | 2.6.5     | 3.1.2     | 2010-04 x
| CentOS 5      | 2.4.3     | -         | 2007-04 x

##### Notes

1. Python 2 is included in the base OS install.

2. CentOS and RedHat <= 7 do not include Python 3 in their standard OS
   packages. You can install from the third-party EPEL packages with:

       yum install -y epel-release
       yum install -y python34         # 3.4.5; `python3`
       yum install -y python36         # 3.6.3; `python36`; CentOS 7 only


Building Alternative Versions
-----------------------------

### [Pythonz]

Download and install in `~/.pythonz` with:

    curl -kL https://raw.github.com/saghul/pythonz/master/pythonz-install | bash

To enable the `pythonz` command:

    [[ -s $HOME/.pythonz/etc/bashrc ]] && source $HOME/.pythonz/etc/bashrc

Set up virtual environments with:

    virtualenv -p $(pythonz locate 2.7.3) python2.7.3           # Python < 3.3
    /usr/local/pythonz/pythons/CPython-3.4.1/bin/pyvenv pyvenv  # Python >= 3.3

### From Source

Get the source from [GitHub] or the Python.org [downloads] area and
build it:

    sudo apt-get install build-essential dpkg-dev \
        zlib1g-dev libbz2-dev liblzma-dev \
        libssl-dev libgdbm-dev libncurses5-dev libreadline-dev
    #   Use libssl1.0-dev instead for Python <=3.4
    #   XXX should include libsqlite as well...
    mkdir ~/.local/python34
    ./configure --prefix=/home/cjs/.local/python34
    make -j 4
    #   Check for notices about libs it couldn't build
    make -j 8 install       # Python 2.x may need `altinstall`?



[pythonz]: https://github.com/saghul/pythonz
