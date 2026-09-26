First C64 program
=================

Now that we've set up our development environment in the last section, we
naturally want to test it. And what could be more obvious and traditional
for our first program than a **Hello C64 World** program.

Here, I'll briefly describe how we build the source code and run it on the
emulator.  I won't go into the details of the source code or the technology
behind the C64 here.

I'll cover that later.

Project organization
--------------------

First, we'll create a new directory.

.. code-block:: bash

    mkdir hello_c64
    cd hello_c64

In diesem Verzeichnis erstellen wir 2 Dateien. Zum einen das ``Makefile``, das
die Befehle für das ``make`` Kommando enthält und eine ``main.asm``, den
eigentlichen Source Code.

In this directory, we create two files: first, the ``Makefile``, which contains
the instructions for the ``make`` command, and second, a ``main.asm`` file,
which is the actual source code.

.. code-block:: bash

    touch Makefile
    touch main.asm

Next, we open the ``Makefile`` in the editor of our choice and insert the following.

.. code-block:: make

   ASM=ca65
   LD=cl65

   ASMFLAGS=--cpu $(CPU) -t $(SYSTEM) -l $(@:.o=.lst) -o
   LDFLAGS=--cpu $(CPU) -t $(SYSTEM) -m $(MAP) -o

   TARGET=HELLO.PRG
   MAP=hello.map

   OBJ=main.o
                                                                                                                                                                             
   CPU=65C02
   SYSTEM=c64

   %.o: %.asm
   	$(ASM) $(ASMFLAGS) $@ $<

   $(TARGET): $(OBJ)
   	$(LD) $(LDFLAGS) $(TARGET) $(OBJ)

   clean:
   	rm -rf $(OBJ) $(TARGET) *.lst $(MAP)

.. todo::
   Makefile überarbeiten. Mit debugger
   Makefile darauf hinweisen, dass TABs verwendet werden müssen.
