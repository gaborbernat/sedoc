Systemd Units
=============

A simple example of setting up a network service to be run by systemd
can be found at [fabianlee]. Socket activation examples can be found
at [systemd for Developers I][0p-socket] and [systemd for Developers
II][0p-socket2].


Systemd [Unit] Types
--------------------

| Unit Type     | Description
|---------------|----------------------------------------------------------
| [*.target]    | Groups units and creates sync points for startup
| [*.slice]     | Hierarchical sub-group of processes
| [*.service]   | A process controlled and supervised by systemd
| [*.scope]     | Management of externally created procs (no config file; created via API)
| [*.socket]    | Listening socket that activates a service on request
| [*.timer]     | Timer-based activation
| [*.path]      | Path-based activation using [inotify(7)].
| [*.mount]     | Filesystem mount point controlled and supervised by systemd
| [*.automount] | Filesystem automount point
| [*.swap]      |
| [*.device]    |

See also `systemctl -t help` output and the list of [special units].
For those units that are configured with files, there is a list of all
[directives].


Transient Units
---------------

[`systemd-run`] creates one of three types of transient unit:
* `.service` unit (default): started and managed asynchronously by
  the service manager in a clean and detached environment. (Output
  goes to standard loggin system.)
* `.scope` unit (`--scope`): started synchronously (in foreground) in
  current environment (systemd-run is parent process)
* `.timer` unit (`--on-*`): timer that starts a `.service` unit when
  it elapses.

Transient services that have existed but are kept with `--remain-after-exit`
will not be listed in the `systemctl status` process tree but can be
found by name or other means, e.g.

    systemctl status '*.service'
    systemctl --user -t service list-units


Systemd User Units
------------------

Systemd can also be used by regular users to run services and even
manage an entire desktop session, though at the moment there seem to
be a lot of issues with this.

System and user units live in separate namespaces; `systemctl status
postfix.service` and `systemctl status --user postfix.service` refer
to different units.

Further information:
* [Arch Linux Systemd/User][arch-systemd-user] wiki page
* William Giokas' [Converting to systemd --user][kaisforza]
* zoqaeski's [systemd-user-units] repo
* [gtmanfred page] on managing your Xorg session (archive copy)


Unit Files
----------

Similar to [XDG Desktop Entry] files (in turn similar to Windows INI
files) but settings can be specified more than once, with various
interpretations (usually, a list of each value for that setting, reset
by setting a value to empty; this is not compatible with the XDG
parser).

#### Load Paths

`$SYSTEMD_UNIT_PATH` overrides everything below, or prefixes
everything below if the last entry is empty (`...:`).

`--system` mode:

    /etc/systemd/system
    /run/systemd/system
    /lib/systemd/system

`--user` mode:

    ${XDG_CONFIG_HOME:-$HOME/.config}/systemd/user
    /etc/systemd/user
    $XDG_RUNTIME_DIR/systemd/user
    /run/systemd/user
    ${XDG_DATA_HOME:-$HOME/.local/share}/systemd/user
    /usr/lib/systemd/user

#### Unit File Directives

See [unit-file](unit-file.md) for details.



[*.automount]: https://www.freedesktop.org/software/systemd/man/systemd.automount.html
[*.device]: https://www.freedesktop.org/software/systemd/man/systemd.device.html
[*.mount]: https://www.freedesktop.org/software/systemd/man/systemd.mount.html
[*.path]: https://www.freedesktop.org/software/systemd/man/systemd.path.html
[*.scope]: https://www.freedesktop.org/software/systemd/man/systemd.scope.html
[*.service]: https://www.freedesktop.org/software/systemd/man/systemd.service.html
[*.slice]: https://www.freedesktop.org/software/systemd/man/systemd.slice.html
[*.socket]: https://www.freedesktop.org/software/systemd/man/systemd.socket.html
[*.swap]: https://www.freedesktop.org/software/systemd/man/systemd.swap.html
[*.target]: https://www.freedesktop.org/software/systemd/man/systemd.target.html
[*.timer]: https://www.freedesktop.org/software/systemd/man/systemd.timer.html
[0p-socket2]: http://0pointer.de/blog/projects/socket-activation2.html
[0p-socket]: http://0pointer.de/blog/projects/socket-activation.html
[Unit]: https://www.freedesktop.org/software/systemd/man/systemd.unit.html
[XDG Desktop Entry]: https://specifications.freedesktop.org/desktop-entry-spec/latest/
[`systemd-nspawn`]: https://www.freedesktop.org/software/systemd/man/systemd-nspawn.html
[`systemd-run`]: https://www.freedesktop.org/software/systemd/man/systemd-run.html
[arch-systemd-user]: https://wiki.archlinux.org/index.php/Systemd/User
[containers]: http://0pointer.net/blog/systemd-for-administrators-part-xxi.html
[directives]: https://www.freedesktop.org/software/systemd/man/systemd.directives.html#
[fabianlee]: https://fabianlee.org/2017/05/21/golang-running-a-go-binary-as-a-systemd-service-on-ubuntu-16-04/
[gtmanfred page]: https://web.archive.org/web/20130205193653/http://blog.gtmanfred.com/?p=26
[inotify(7)]: http://man7.org/linux/man-pages/man7/inotify.7.html
[kaisforza]: https://bitbucket.org/KaiSforza/systemd-user-units
[machine-id]: https://www.freedesktop.org/software/systemd/man/machine-id.html
[special units]: https://www.freedesktop.org/software/systemd/man/systemd.special.html
[zoqaeski]: https://github.com/zoqaeski/systemd-user-units
