## AMDGPU VEGA HotSpot temperature patch

This simple patch introduces the additional temperatures into hardware monitor:

* temp2_input - (CTF temperature) main GPU temperature
* temp3_input - (ASIC_MAX temperature) GPU hot spot temperature

Currently, this patch is for kernel 4.16 line (this patch can be applied to 4.15 version).
These temperatures sensors will be added for VEGA devices.

### Applying patch

Enter to you linux kernel directory and enter command:

```
patch -p1 < vega10_extratemps-X.Y.Z.patch
```

and you can make your kernel.

### How to read sensors

Just by putting command (if you have configured lm3-sensors):

```
sensors
```

or by reading from file in sysfs:

```
cat /sys/class/drm/cardX/device/hwmon/hwmonY/temp2_input
cat /sys/class/drm/cardX/device/hwmon/hwmonY/temp3_input
```

where cardX is your VEGA graphic card and hwmon is your hwmon for this card.

### Linux directory

The linux-4.16.1 directory holds amdgpu driver with applied changes.
This is not whole Linux kernel sources.
