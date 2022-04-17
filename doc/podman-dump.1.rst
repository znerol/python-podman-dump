podman-dump
===========

Synopsis
--------

**podman-dump** [*-p*] [*-v*] [*--podman PODMAN*] [*--conmon CONMON*] [*dumpdir*] [*schedule*]


Description
-----------

Looks for running podman containers annotated with the ``ch.znerol.podman-dump``
label. Executs all specified jobs matching the given *schedule* und dumps the
results into *dumpdir*. Prunes old dumps if *-p* / *--prune* flag is present.

The ``ch.znerol.podman-dump`` label must contain a JSON document of the
following form:

.. code-block:: json

      {
        "jobs": [
          {
            "command": ["echo", "output of weekly job"],
            "schedules": ["weekly"]
          },
          {
            "command": ["echo", "output of daily job"]
            "schedules": ["daily", "manual"]
          },
        ]
      }

Each job specification may include the following keys and values:

command
   Required list of strings specifying a command. The first value represents the
   executable to run, while the following values are passed as arguments.

   Note that environment variables are not expanded automatically in the command
   line. If this is desired, then a shell needs to be invoked.

schedules
   Required list of strings of schedule names this job is part of.

compress
   Optional boolean value (``true`` or ``false``). Whether or not the dump
   should be compressed with ``gzip``. Defaults to ``false``.

extension
   Optional file extension for the dumpfile (e.g. ``.sql``). Defaults to the
   empty string (no extension).

part
   Optional part-suffix for the dumfile. Used to separate multiple types of
   dumps (e.g. ``schema`` and ``data`` foro databes dumps). Omitted by default.

keep
   Optional positive integer specifying how many old files are kept when the
   dumpdir is pruned. Defaults to ``0`` (no pruning, all files are kept).

env
   Optional mapping of string keys to string values. Additional environment
   variables to make available for the command.

env_file
   Optional string path to an environment file.

interactive
   Optional boolean value (``true`` or ``false``). When set to true, keep stdin
   open even if not attached. Defaults to ``false``.

tty
  Optional boolean value (``true`` or ``false``). Allocate a pseudo-TTY.
  Defaults to ``false``.

user
   Optional string value specifying user and group to run command under. User
   and group must be separated by colon. User and group can be specified either
   by name or by numeric id.

workdir
   Optional string value specifying the working directory the command will run
   in.

See Also
--------

:manpage:`podman-dump@.service(8)`
