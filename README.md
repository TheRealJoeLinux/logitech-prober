logitech-prober
===============

The Problem
-----------
You just purchased a Logitech mouse (or mouse/keyboard combo) for your Ubuntu computer, and it came with that handy little _unifying receiver_.

You plug the receiver in to an open USB port, and nothing happens.

The Other Problem
-----------------
Turns out, it's not a matter of Ubuntu being incompatible, it's just that it appears to fail after the initial probe (reference open bugs [046d:c52b USB3 port Logitech mouse using unifying receiver not always detected](https://bugs.launchpad.net/ubuntu/+source/linux/+bug/1039143) and [046d:c52b Cannot use logitech mouse M324 (Unifying Receiver)](https://bugs.launchpad.net/ubuntu/+source/linux/+bug/1028806)) , and never bothers re-probing for nearby wireless devices again.

**This is easily solved by simply reloading the appropriate modules again to force the system to probe.**

_Side Note: Once the above-referenced bugs are closed, hopefully there will no longer be a need for this utility or others like it._

You can run this command to do so:

    $ sudo modprobe -r hid_logitech_dj && sudo modprobe hid_logitech_dj

Of course, that's a pain. This repo is the solution.

The Solution
------------
The most automated way to do this that I've found is to create a script to do this module magic for you upon booting your computer. The script needs to know when to stop messing with your modules, so I also created a program that does nothing more than output your mouse's current X coordinates.

_Once you've followed the installation instructions below, you should be able to simply keep moving your wireless mouse after you get to the login screen until your mouse starts moving, and the script should end itself automatically._

Installation
------------
Clone this repo (or [download as a zip](https://github.com/TheRealJoeLinux/logitech-prober/zipball/master)), and then *cd* into the resulting directory.

    $ git clone git://github.com/TheRealJoeLinux/logitech-prober.git
    $ cd logitech-prober/

Install the packages "build-essential" and "libx11-dev", if you don't have them already.

    $ sudo apt-get install build-essential libx11-dev

Compile the file that spits out your mouse's X coordinates

    $ make

Install the script and newly compiled file

    $ sudo make install

**Next time you start up your computer, just start wiggling the mouse left and right as soon as the mouse cursor shows up on screen. Once it starts moving, you should be set!**

Alternatively, you can just run `/usr/local/bin/logitech-prober.sh` once you've gone through the installation steps above, and just keep wiggling the mouse left and right until it moves on screen.

Removal
-------
Simply run the following command (within the project directory of course):

    $ sudo make uninstall
