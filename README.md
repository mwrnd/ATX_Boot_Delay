**Work-In-Progress**: [Gerbers complete](https://github.com/mwrnd/ATX_Boot_Delay/releases/tag/v0.1-alpha) but not yet ordered.

# ATX Boot Delay

Power-On Boot Delay for ATX Motherboards with 9-Pin Front Panel Header.

Delaying BIOS boot is a simple trick that solves some PCIe issues. You can do this by pressing the POWER button, then pressing and holding the RESET button for a second before releasing it. Or, connect a capacitor across the reset pins of an ATX motherboard's [Front Panel Header](https://www.intel.com/content/www/us/en/support/articles/000007309/intel-nuc.html).

This board is a simple Front Panel replacement that allows choosing capacitor(s) to connect accross the RESET pins and delay boot.



## PCB Layout
![ATX Boot Delay Board PCB Layout](img/ATX_Boot_Delay_PCB_Layout.png)



## Schematic

![ATX Boot Delay Board Schematic](img/ATX_Boot_Delay_Schematic.png)



## Theory of Operation

![Delay Motherboard Boot Using RESET Capacitor](img/Delay_Boot_Using_Capacitor.jpg)

The capacitor across RESET works thanks to an [RC Delay](https://en.wikipedia.org/wiki/RC_time_constant) on the reset signal buffer. The [OpenCompute](https://en.wikipedia.org/wiki/Open_Compute_Project) project has a public schematic and the RESET Button is on Pg#151 in *Project_Olympus_Intel_XSP_Schematics_20171016.pdf* found in [`Project_Olympus_Intel_XSP_Collateral.zip`](http://files.opencompute.org/oc/public.php?service=files&t=e969672c57d6e17647adea54f2c3e5a7&download).

![RESET Button Schematic](img/Server_Motherboard_RESET_Button_Schematic.png)

A standard Schmitt-Trigger inverter such as the [SN74LVC1G14](https://www.ti.com/lit/gpn/SN74LVC1G14) has a positive-going threshold voltage of about 1.5V with a 3.3V supply. I have measured 1k-Ohm between the RESET+ pin and the 3.3V ATX Power supply rail. A 330uF capacitor therefore delays boot by about 200ms. [RC Calculator](http://ladyada.net/library/rccalc.html):

![RC Delay Calculator](img/RC_Delay_Calculator.png)

I found out about this technique [here](https://hackaday.com/2018/02/17/catching-the-pcie-bus/):

![Boot Delay Technique Source](img/Delay_Boot_with_Capacitor_Across_PC_RESET.png)



