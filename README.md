BBB eQEP Library
================

bbb-eqep is a library for accessing the eQEP modules built into the Beaglebone Black's microprocessor. Although this library has only been tested on the BBB, it will likely work on other TI processors that include the eQEP modules.

Building and Installation
=========================
Please see the INSTALL file for detailed instructions. Here's the basics:

````shell
autoreconf
./configure
make
make install
````

If you have Doxygen installed, the docs folder will be filled with documentation.

Programming Tutorial
====================

First, pinmux the eQEP pins and enable the associated PWM module.
````shell
# echo fast_eQEP0 > /sys/devices/bone_capemgr.*/slots
````

Using the library is as simple as passing the eQEP number or base address to the constructor, and calling getPosition().

````cpp
eQEP eqep0(0);
eQEP eqep2(eQEP2);
uint32_t eqep_pos = eqep.getPosition();
````

The eQEP class also has a default cast to `uint32_t` so the last line can be shortened to:

````cpp
uint32_t eqep_pos = eqep;
````

Please see the test.cpp file for more example usages.

Accessor methods are provided for virtually every eQEP feature. All of these are best viewed through the Doxygen generated documentation.
Instantiating an eQEP sets standard defaults across the eQEP block and makes this library incompatible with other eQEP reading solutions.

Prerequisites
=============
Since this library relies heavily on `mmap()` and direct memory access, likely the resultant programs will require root priviledges to run. Please let me know if you figure out a way to operate this library in userspace.

Test Program Output
===================
````shell
$ sudo examples/test 0
SYSCONFIG 0xC
CLKCONFIG 0x111
QEPCTL0   0x8
QDECCTL0  0x0
QEINT0    0x0
QUPRD0    0x0
QPOSMAX0  0xFFFFFFFF
QEPSTS0   0x80
last position: 920723
micros per read: 0.218907
quadrature read kHz: 4568.149902
revid: 0x44D31103 (should read 44D31103)
eqep: 920723
````