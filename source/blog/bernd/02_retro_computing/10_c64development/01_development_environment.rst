C64 Development Environment
===========================

On this page, I describe how my development environment is set up and installed.
I sometimes build tools from source packages and install them here.

I usually have a project directory under ``/opt`` where I install these kinds
of things. But that might not work for everyone. So these directories are
customizable.  Just because I do it this way doesn’t mean it has to work
for you, too. 

System
------

I use Linux as my development system for personal projects.
I haven't used Windows for personal use in years.
I don't want to start an argument or trigger a discussion here.
Everyone should use whatever they want.

I usually use a relatively recent version of Ubuntu LTS.

Since I use Linux, this guide will focus exclusively on Linux.

make
----

A build tool is a program that checks whether there have been changes to the source
files that aren't yet reflected in the executable.
If there have been changes, there is a set of rules for how the source
file must be built in order to obtain an up-to-date binary.

I usually use CMake as the build tool for my projects.
But that would be like using a sledgehammer to crack a nut. So here I'm using
plain and simple ``make``.
On Ubuntu, there’s a package that installs ``make`` and ``gcc``.
Since we need both, that's a good choice.

.. code-block:: bash

   sudo apt install build-essential

Compiler/Assembler
------------------

The `cc65 <https://cc65.github.io/>`_ is a cross-compiler package for
6502-based systems.  It supports a wide variety of systems, including
the VIC-20 and the C64. I think the cc65 is a very good choice.

To install the compiler, you can either use pre-built packages

.. code-block:: bash

   sudo apt install cc65

or you can clone the GitHub repository and build it yourself.
All you need is ``make`` and a C compiler.

.. code-block:: bash

   git clone https://github.com/cc65/cc65.git
   cd cc65
   PREFIX=/opt/c64/cc65 make
   sudo make install

These commands clone the GitHub repository, build the compiler suite, and
install it in /opt/cc65. To use it, you must add the directory ``/opt/c64/cc65/bin``
to the ``PATH`` environment variable.

.. code-block:: bash

   export PATH=$PATH:/opt/c64/cc65/bin

So now we have a working compiler, assembler, and linker.

git
---

Git is a version control system and the de facto standard for version control.
I've been using Git for many years and love it.
It’s a very powerful tool, but a few simple commands are enough to
get started. I recommend that whenever you start a software project, the
first thing you do is run ``git init`` and, once your work is done, push your code
to a Git server. But this isn’t meant to be an introduction to Git.
Please use Google for that.

.. code-block:: bash

   sudo apt install git

Editor
------

The editor is a very personal choice. I prefer VI or one of its clones:
VIM, NeoVIM, ...
I also consider myself a VI power user. I've been using it for many years.
There's a funny story about why I use VI. I like to tell it over a beer, but
there's no room for it here right now.

Another reason I like VI is that it's installed on every - and I mean EVERY -
Unix-based system. I'm an embedded Linux developer, and whenever I log in to
a Linux system - no matter how small - I know there's a VI on it. And if you
can handle it reasonably well, it makes life a little easier for an embedded
developer.

I've also been eyeing the `Helix Editor <https://helix-editor.com/>`_ for quite
some time. However, I haven't quite managed to make the switch yet.

The downside of VI and Helix is that they have a slightly steeper learning curve.
If you’re not used to using keyboard shortcuts and working without a mouse -
or, more generally, working in a text terminal - then the learning curve is
steeper. But it’s worth it. In my opinion...

For most people, though, a modern IDE is a must and definitely makes sense.
`Visual Studio Code <https://code.visualstudio.com/>`_ is a great option here.

Emualtor
--------

There are tons of emulators for retro systems, especially for the Commodore C64.
One of the best-known is certainly the Versatile Commodore Emulator, or
`VICE <https://vice-emu.sourceforge.io>`_ for short.
You can install the emulator via

.. code-block:: bash

   sudo apt install vice

or build it yourself. I prefer to build it myself, since the Ubuntu
repository doesn't contain the latest version.

First, you need to download the `source code <https://sourceforge.net/projects/vice-emu/files/releases/vice-3.10.tar.gz/download>`_.
Then, extract the archive.

.. code-block:: bash

   tar -xzvf vice-3.10.tar.gz

Next, you'll need to install all the dependencies required for the build process.
Don't worry—you can uninstall them again after the build is complete.

.. code-block:: bash

   sudo apt install autoconf automake build-essential byacc flex xa65 gawk \
   libgtk-3-dev texinfo texlive-fonts-recommended texlive-latex-extra dos2unix \
   libpulse-dev libasound2-dev libglew-dev libcurl4-openssl-dev libevdev-dev \
   libgif-dev libpcap-dev

Now you need to navigate to the source code directory and start the build.

.. code-block:: bash

   cd vice-3.10
   ./configure --enable-gtk3ui --prefix=/opt/c64/vice
   make
   sudo make install

The VICE emulator should now be installed in ``/opt/c64/vice``.
To use it, you must add the directory ``/opt/c64/vice/bin`` to the ``PATH``
environment variable.

.. code-block:: bash

   export PATH=$PATH:/opt/c64/vice/bin

Now all the dependencies required for the build can be uninstalled.
This step is optional. The development packages for the libraries "only" take
up some space, but otherwise don't cause any problems.

.. code-block:: bash

   sudo apt purge autoconf automake build-essential byacc flex xa65 gawk \
   libgtk-3-dev texinfo texlive-fonts-recommended texlive-latex-extra dos2unix \
   libpulse-dev libasound2-dev libglew-dev libcurl4-openssl-dev libevdev-dev \
   libgif-dev libpcap-dev

Debugger
--------

.. todo::

   Add debugger
