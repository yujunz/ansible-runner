.. _standalone:

Using Runner as a standalone command line tool
==============================================

The **Ansible Runner** command line tool can be used as a standard command line interface to **Ansible** itself but is primarily intended
to fit into automation and pipeline workflows. Because of this it has a bit of a different workflow than **Ansible** itself in that you can select
between a few different modes to launch the command.

While you can launch **Runner** and provide it all of the inputs as arguments to the command line (as you do with **Ansible** itself),
there is another interface where inputs are gathered into a single location referred to in the command line parameters as ``private_data_dir``
(see :ref:`inputdir`)

To view the parameters accepted by ``ansible-runner``::

  $ ansible-runner --help

An example invocation of the standalone ``ansible-runner`` utilty::

  $ ansible-runner -p playbook.yml run /tmp/private

Where playbook.yml is the playbook from the ``/tmp/private/projects`` directory, and ``run`` is the command mode you want to invoke **Runner** with

The different **commands** that runner accepts are:

* ``run`` starts ``ansible-runner`` in the foreground and waits until the underlying **Ansible** process completes before returning
* ``start`` starts ``ansible-runner`` as a background daemon process and generates a pid file
* ``stop`` terminates an ``ansible-runner`` process that was launched in the background with ``start``
* ``is-alive`` checks the status of an ``ansible-runner`` process that was started in the background with ``start``

While **Runner** is running it creates an ``artifacts`` directory (see :ref:`artifactdir`) regardless of what mode it was started
in. The resulting output and status from **Ansible** will be located here. You can control the exact location underneath the ``artifacts`` directory
with the ``-i IDENT`` argument to ``ansible-runner``, otherwise a random UUID will be generated.

Executing **Runner** in the foreground
--------------------------------------

When launching **Runner** with the ``run`` command, as above, the program will stay in the foreground and you'll see output just as you expect from a normal
**Ansible** process. **Runner** will still populate the ``artifacts`` directory, as mentioned in the last section, to preserve the output and allow processing
of the artifacts after exit.

Executing **Runner** in the background
--------------------------------------

When launching **Runner** with the ``start`` command. The program will generate a pid file and move to the background. You can check its status with the
``is-alive`` command, or terminate it with the ``stop`` command. You can the stdout, status, and return code in the ``artifacts`` directory.

Running Playbooks
-----------------

**TODO**

Running Roles Directly
----------------------

**TODO**
