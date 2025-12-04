podman-dump@.service
====================

Synopsis
--------

**podman-dump@.service**

**podman-dump@.timer**


Description
-----------

Periodically dumps container contents.

The instance name (systemd instance string specifier ``%i``) is used as the
schedule name.

Schedules can be enabled out of the box for all interval shorthands supported by
``systemd.time(7)``. E.g., in order to enable the weekly schedule in the systemd
``system`` scope, run the following command:

.. code-block:: shell

   systemctl enable --now podman-dump@weekly.timer

Environment
-----------

.. envvar:: PODMAN_DUMP_DIR

   Path of the directory where dumps are stored. Defaults to
   ``/var/backups/podman/%i`` when run in systemd ``system`` scope and
   ``~/.local/backups/podman/%i`` when run in ``user`` scope.

.. envvar:: PODMAN_DUMP_JOBDIR

   Path of the directory where job definitions are stored. Defaults to
   ``/etc/podman-dump/jobs`` when run in systemd ``system`` scope and
   ``~/.config/podman-dump/jobs`` when run in ``user`` scope.

.. envvar:: PODMAN_DUMP_FLAGS

   Flags used when invoking ``podman-dump``.


See Also
--------

:manpage:`podman-dump(1)`
