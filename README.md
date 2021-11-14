# Asus Zenbook Duo UX481

This repo ilustrates the viability of installing Ubuntu 20.0.4TLS with full compatibility, the only issue is screnpad plus with brightnes at 50%, easy to fix with this, any alternative solution never worked for me:

> Hi there,
>
> I bought the 14 inch model (UX481) last week and while those two are fairly different (for instance my main screen is LCD, not OLED, and brightness control for the main screen worked out of the box) the problem with the brightness of the lower screen is quite similar: under Linux, it was stuck at around 50% brightness and I couldn't control it (or turn it off). So I did some digging through the DSTS code and also watched the behavior of the ASUS Windows software and finally found a way to control the bottom screen brightness in Linux. Using it is quite hack-ish at the moment (it will have to be built into the kernel to work nicely), but it's usable and I think there is a good chance that it also works at the UX581 – I don't see why ASUS should use a different method as the driver software used in Windows is identical for both models.
>
> So, here is how I managed to control bottom screen brightness on my device (use at your own risk):
> 
> install the acpi_call kernel module using the package from your distribution. In Debian, Ubuntu etc. the package is called acpi-call-dkms
> 
> load the module using sudo modprobe acpi_call
> 
> use the following commands to control the bottom screen (they all have to be executed as root - instead of using sudo, you can of course also use a root shell):
> Change Brightness of the screen:
> 
> echo '\_SB.ATKD.WMNB 0x0 0x53564544 b32000500xx000000' | sudo tee /proc/acpi/call
> 
> where xx is a value between 00 and FF (00 being darkest, FF brightest, 77 in between etc.)
> 
> So for maximum brightness, use:
> 
> echo '\_SB.ATKD.WMNB 0x0 0x53564544 b32000500FF000000' | sudo tee /proc/acpi/call
> 
> Turn off the screen:
> 
> echo '\_SB.ATKD.WMNB 0x0 0x53564544 b3100050000000000' | sudo tee /proc/acpi/call
> 
> To turn the screen back on again, just send a brightness command.
> 
> I added the acpi_call module to my /etc/modules file so it is loaded at system startup and added the following line to /etc/rc.local in order to turn the screen > to full brightness at system start:
> 
> echo '\_SB.ATKD.WMNB 0x0 0x53564544 b32000500FF000000' > /proc/acpi/call
> 
> I hope it also works for you!
> 
[Source](https://github.com/s-light/ASUS-ZenBook-Pro-Duo-UX581GV/issues/1)
