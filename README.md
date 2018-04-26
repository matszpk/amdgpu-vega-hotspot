## AMDGPU HotSpot (ASIC_MAX) temperature patch

This simple patch introduces the additional temperature into hardware monitor:

* temp2_input - (ASIC_MAX temperature) GPU hot spot temperature

Exactly, this is an aggregated value, the maximal temperature from the internal sensors.

Currently, this patch is for kernels 4.14 - 4.16.
This temperature input will be added for all graphics cards.

The temp1_input is graphics card's main (CTF) temperature.

### Patches

* vega10_extratemps-X.X.X.patch - original VEGA 10 patch (apply only for VEGA)
* amdgpu_extratemps-X.X.X.patch - AMDGPU patch for all graphics cards

### Applying patch

Enter to your linux kernel directory and enter command:

```
patch -p1 < amdgpu_extratemps-X.Y.Z.patch
```

and you can make your kernel.

### How to read sensor

Just by putting command (if you have configured lm3-sensors):

```
sensors
```

or by reading from file in sysfs:

```
cat /sys/class/drm/cardX/device/hwmon/hwmonY/temp2_input
```

where cardX is your VEGA graphic card and hwmon is your hwmon for this card.

New version of the AMDCOVC 0.3.9.2 can read extra temperatures and
you can use this tool to read a hot spot temperature.

### Linux directory

The linux-4.16.1 directory holds amdgpu driver with applied changes.
This is not whole Linux kernel sources.

### Previous version

The initial version of this patch provided two extra temperature sensors
(first was doubling standard temp1_input and second was the hot spot temperature sensor).
