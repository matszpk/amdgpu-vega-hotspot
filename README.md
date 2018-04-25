## AMDGPU Fiji/Tonga/Polaris/VEGA HotSpot temperature patch

This simple patch introduces the additional temperature into hardware monitor:

* temp2_input - (ASIC_MAX temperature) GPU hot spot temperature

Exactly, this is an aggregated value, the maximal temperature from the internal sensors.

Currently, this patch is for kernel 4.16 line (this patch can be applied to 4.15 version).
These temperature sensor will be added for the VEGA and GCN 1.2/1.3
(Fiji, Tonga, Polaris) devices.

The temp1_input is graphics card's main (CTF) temperature (since Linux 4.15 version).

### Applying patch

Enter to your linux kernel directory and enter command:

```
patch -p1 < vega10_extratemps-X.Y.Z.patch
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
