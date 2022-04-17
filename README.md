podman-dump
===========

A python script and a systemd unit simplifying data backups from podman
containers.


Dependencies
------------

Podman-dump requires `podman` und `Python >= 3.6`.

Note that `conmon` version < 2.0.26 is affected by containers/conmon#236.
Unfortunately, this bug affects `conmon` shipped in
[Debian 11 (Bullseye)][conmon bullseye] as well as
[Ubuntu 22.04 (Jammy Jellyfish][conmon jammy]).

Use the `--conmon` flag of `podman-dump` to specify a more recent `conmon`
version to be used during dumps.

[conmon bullseye]: https://packages.debian.org/bullseye/conmon
[conmon jammy]: https://packages.ubuntu.com/jammy/conmon

Install
-------

Navigate to the releases page and pick the latest `podman-dump-dist.tar.gz`
tarball. Copy it to the target machine and unpack it there.

    $ scp dist/podman-dump-dist.tar.gz me@example.com:~
    $ ssh me@example.com sudo tar -C /usr/local -xzf ~/podman-dump-dist.tar.gz


Build
-----

*Preferred method*: Build a distribution tarball, copy it to the target machine
and unpack it there.

    $ make dist
    $ scp dist/podman-dump-dist.tar.gz me@example.com:~
    $ ssh me@example.com sudo tar -C /usr/local -xzf ~:podman-dump-dist.tar.gz

*Alternative method*: Check out this repository on the traget machine and
install it directly. The destination directory can be changed with the `prefix`
variable in order to change the installation prefix to something else than
`/usr/local`.

    $ make all
    $ sudo make prefix=/opt/local install

[Sphinx] is necessary in order to build the man pages and the users guide. This
step can be skipped by using the `install-bin` target.

[Sphinx]: https://www.sphinx-doc.org/


Annotations
-----------

Annotate containers with the `ch.znerol.podman-dump` label in order to
configure them for periodic backups. See the `podman-dump(1)` manpage for
detailed information.


Systemd timers
--------------

Enable `podman-dump@.timer` with an instance name matching one of the interval
shorthands supported by `systemd.time(7)`. E.g., in order to enable the weekly
schedule in the systemd `system` scope, run the following command:

```
systemctl enable --now podman-dump@weekly.timer
```

Refer to `podman-dump@.service(8)` manpage for detailed information.


Usage
-----

```
usage: podman-dump [-h] [-p] [-v] dumpdir schedule
usage: podman-dump [-h] [-p] [-v] [--podman PODMAN] [--conmon CONMON] dumpdir schedule

positional arguments:
  dumpdir          The destination directory for container dumps
  schedule         Name of the schedule to run

optional arguments:
  -h, --help       show this help message and exit
  -p, --prune      Prune old backups after dumping a container
  -v, --verbose    Turn on verbose logging
  --podman PODMAN  Path of the podman binary
  --conmon CONMON  Path of the conmon binary

```


License
-------

* [GPL-3 or later](https://www.gnu.org/licenses/gpl-3.0.en.html)

