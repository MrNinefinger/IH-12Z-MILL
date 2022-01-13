IH-12Z-MILL configuration

LinuxCNC configuration for an Industrial Hoobies / Machine Tools Warehouse / RF45 12Z Mill converted to use step/dir servos (and a stepper for 4th axis) 
and a MESA 7i76E interface card. This is my "working configuration", and it may not be optimal but its good enough for me (for now).

General Machine Configuration Notes:

The configuration includes a 4th axis, being operated by a stepper motor.

The spindle parameters are for the VFD which is a GE Fuji.  The commanded RPM I think corresponds to H3 - this needs to be verified.
The 4th axis is a 6" rotary table, with a 90:1 input ratio so 1 rev of the stepper motor is 4 degrees of movement.  with 32 micro stepping and a standard 200step/rev motor, the step scale (steps / degree) is 32*200/4=1600 
The mill is configured with home switches at 'max' Z (high point on column) and 'min' X (table furthest to the left viewed from front) and 'max' Y (table closest to column). Spindle speed is not displayed

Installation Notes:
Note - the below is not needd for the mill but is usefull to keep the same general PC configuration between mill and lathe.

    To install any new .comp file linuxcnc-uspace-dev is needed, may have to add the repositories manually (look up and add to synaptic package manager), as well as "build essential"

    sudo apt-get update
    sudo apt-get install build-essential
    sudo apt-get install linuxcnc-uspace-dev
    The Synaptic package manager has to be closed before using the terminal to install stuff (i.e. toolchanger.comp) open a terminal in the folder where the .comp file is and enter:

    I had issues with sudo, can instead run in root and omit sudo prefix on commands: su root exit root when done!

Usefull tools to improve linux functionality: visudo will let you add you're username to the sudo list,instructions here: https://devconnected.com/how-to-add-a-user-to-sudoers-on-debian-10-buster/

apt-get install visudo
Lastly - clone this respository to the configs folder in Linuxcnc

~/linuxcnc/configs$ git clone https://github.com/MrNinefinger/IH-12Z-MILL

Running it:

Things to work on:

 Add spindle speed display (put encoder on spindle?).
 Tool changes (M6) is currently remapped and set to auto measure tool length on every tool change - but tool setter is not fixed in place, and can be accidentally disabled by not having the touch probe active!
 figure out seperating touch probe signal and tool setter.
 Figure out gearing in linuxcnc to be able to select the Low high gear settings and the 3 gears and have the commanded speed be correct.
 add real buttons and an encoder for jogging, MDI entry, etc.
 investigate QTdragon screens (needs Linuxcnc 2.9 which will probably break everything!)
 add a seperate set of files for Linuxcnc installation tips and hints (i.e. change wicd to network manager, setup 2nd ethernet connection for MESA and wireless for internet, etc.)
 figure out how to change the default loaded .ngc file to something not dangerous if somehow you accidentally hit cycle start (more importatnt on the mill)
