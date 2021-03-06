.. _dev:

Development Scripts
===================

.. _dev_install:

The `dev_install` Command
-------------------------

A ``dev_install`` command exists to assist in the installation of tools for
local development. It will clone the tool if it is missing, and add to a
``dev.pth`` file to link it into your environment::

    $ dev_install --list
    < big list of tools and their repos >

    $ dev_install sgfs
    < snip >
    Successfully installed sgfs
    Cleaning up...

If something has changed about the package that breaks its link (e.g. top-level
package names have changed), then ``dev_install --rebuild NAME`` should fix it.


.. _dev_command:

The `dev` Command Wrapper
-------------------------

A ``dev`` command exists that will run any other command from within an automatically constructed development environment. Effectively, any Python imports will use your local packages, and any executables will be sourced from your local paths. Any packages or executables not found locally will fall back on the production tools.

It does this by searching for development tools in :envvar:`KS_DEV_SITES`, and appends those that exist to :envvar:`KS_SITES`. It also looks across the standard ``PATH`` for directories that fall within the production environment, and prepends the development versions of those paths.

Lets look at some examples. I can bring up a Python shell in the development environment::

    $ dev python
    Python 2.6.6 (r266:84292, Nov  1 2010, 12:40:26) 
    [GCC 4.2.1 (Apple Inc. build 5646)] on darwin
    Type "help", "copyright", "credits" or "license" for more information.
    >>> import ks
    >>> ks
    <module 'ks' from '/home/mboers/dev/key_base/python/ks.py'>

Notice how the ``ks`` package was located in my home directory. I can also launch the development version of the toolbox::

    $ dev which toolbox
    /home/mboers/dev/key_base/2d/bin/toolbox
    $ dev toolbox

To drop into a development shell::

    $ dev bash
    $ which toolbox
    /home/mboers/dev/key_base/2d/bin/toolbox

You can also use other developer's environments!

::

    $ dev -u mreid which toolbox
    /home/mreid/dev/key_base/2d/bin/toolbox

See ``dev --help`` for all of the options.

