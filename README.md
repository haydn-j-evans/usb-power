Okay.  Attached is the source code for a program named hubpower.  You 
can use it to tell your hubs to turn their port power on and off.

To compile the program, all you have to do is:

	gcc -o hubpower hubpower.c

You'll probably need to run it with sudo.  Tell the program the hub's 
bus number and device number, and give it a list of ports and power 
settings.  For example,

	sudo ./hubpower 1:3 power 4 on 2 off

This will tell hub 3 on bus 1 to turn port 4's power on and port 2's 
power off.  Because of the way the Linux USB stack works, the program 
will also unbind the hub from the kernel driver when you do this, so 
the system will think that all devices attached to the hub have been 
unplugged.

You can tell the system to bind the hub back to the kernel driver.
The devices plugged into the hub won't work again until you do this:

	sudo ./hubpower 1:3 bind

However when you do this, the kernel driver will turn power for all the
ports back on.  There is no way to tell the Linux hub driver to leave a
port powered off.

Finally, you can see the current status of every port by doing:

	sudo ./hubpower 1:3 status