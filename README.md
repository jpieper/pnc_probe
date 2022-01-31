# Pocket NC Probe Support #

This repository contains:

* Hardware designs to integrate a https://vers.by touch probe into the Pocket NC, https://pocketnc.com
* g-code routines for performing probe operations on the Pocket NC

# Usage #

When installed, [G38.x gcode commands](https://linuxcnc.org/docs/2.6/html/gcode/gcode.html#sec:G38-probe) work as expected.  If the jpieper/pnc_probe subroutines are installed, two new gcode programs are available: `pnc-probe-center-id` and `pnc-probe-center-od`.

These scripts probe features that are close to machine X=0,Y=0 and set G54 to the exact center.

To run either, manually position the probe along either the X axis or Y axis just inside (for ID) or just outside (for OD) at the depth you wish to probe.  Leave sufficient margin (~2mm) so that when the probe checks other directions it will have room to plunge without colliding with the work.

Then start the program.

# Installation #

## Hardware ##

Watch the following video:

TODO

1. Attach the adapter housing to the A axis stepper using a cable tie.  The cable tie should be pulled tight, as this helps keep the enclosure sealed from chips.

2. Disconnect the RJ45 cable from the A axis carriage and connect it to the bottom RJ45 port on the adapter.  The 1ft long ethernet cable should then be connected from the A axis carriage to the top port of the adapter.

3. To insert the probe, the A axis MUST be moved out of the home position.  Note, the machine CANNOT BE HOMED while the probe is inserted, or it will crash.

4. Using a dial indicator, adjust the M2 screws accessed through holes in the front of the probe to reduce runout at the tip of the probe.

5. Remove the screw cap from the adapter enclosure, attach the probe cable to the USB port.  Note, this is not actual USB, but that is the cable the vers.by ships with.

6. Attach the magnetic coupled end of the cable to the probe.

7. When removing the probe, be sure to reinstall the USB cap, otherwise chips may fall into the connector.

## Software ##

1. Copy the contents of the `ncfiles/` and `subroutines/` directories to `/home/pocketnc` on the pocketnc.  You can use WinSCP from Windows, or rsync from Mac/Linux.  A suitable command for linux might look like:

```
rsync -Pv ncfiles subroutines pocketnc@192.168.6.2:
```

2. Depending upon your machine version, you may need to add a .ini overlay.

### Kinetic (current) ###

 * Config Tab
 * Server
 * INI OVERLAY
 * EDIT OVERLAY (bottom right)
 * If RS274NGC is not already in the list of groups, use the '+' button to add it.
 * Ensure the following key is set as follows:

```
SUBROUTINE_PATH=/opt/pocketnc/Settings/subroutines:/home/pocketnc/subroutines
```

 * If you had to change anything, click "REBOOT MACHINE".

### Legacy ###

TODO

# LICENSE #

All files contained in this repository are available under an Apache 2.0 License: https://www.apache.org/licenses/LICENSE-2.0
