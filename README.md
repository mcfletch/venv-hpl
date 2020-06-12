VirtualEnv Host Package Link
===============================

version number: 1.0.0
author: Mike C. Fletcher

Overview
--------

Links Host's Python Library into Virtualenv

This allows you to link a hard-to-compile package into your
virtualenv. Common case is the python-gobject-introspection
library, which is not easily pip installable.

Installation / Usage
--------------------

To install use pip:

    $ pip install venvhpl

Or clone the repo:

    $ git clone https://github.com/mcfletch/venvhpl.git
    $ python setup.py install

Linking a package from the host python into your current virtualenv:

    $ source path/to/myenv/bin/activate
    (myenv) $ venv-hpl gi

Loading the `gi` module from a module such that if the initial
gi import fails we shell out to run `venv-hpl` then re-import:

    try:
        import gi
    except ImportError:
        try:
            import subprocess

            subprocess.check_call(['venv-hpl', 'gi'])
        except subprocess.CalledProcessError:
            raise ImportError("gi")
        else:
            import gi
    
Contributing
------------

This is a trivial project, but if you find something
that needs fixing, please open a pull request.

