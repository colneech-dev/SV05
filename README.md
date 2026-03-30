# SV05
Release version 1.0.1 of my custom build of Marlin 2.1.1 for the Sovol SV05 with Creality v4.2.2 board.

This is based of the source code for 2.1.1 at https://github.com/MarlinFirmware

If you just want to install my compiled binary, copy the firmware bin file to an SD card (make sure there are no other bin files on it).  Make sure your SV05 is turned off, insert the SD card into the SV05, turn on the SV05.  It will take 10 - 20 seconds to update. The screen will be blank and then the Marlin info should come up and the printer should boot normally.

After flashing, check Info -> Printer Info on the LCD — it should show 2.1.1-SV05-v1.0.1 confirming the flash worked.

IT IS VERY IMPORTANT when changing firmware to reset the EEPROM. Go to Configuration -> Advanced Settings -> Initialize EEPROM after flashing.

Features and settings of my firmware.

1) 7x7 Bi-linear bed leveling. (I may switch to UBL in a newer version after some testing)
2) After G28, I have it set to always activate bed leveling. This way you don't need to do it in startup g-code.
3) I heat the hotend to 150 and the bed to 60 before doing any home, bed leveling, tramming, etc. So be aware when you do an initial home on power up, it will home x, home y, and then pause until it heats up. I find 150 gives me identical results to 200 and prevents filament from oozing out. Be aware when doing Z offset calibration if you have any filament stuck on the nozzle, you need to remove it with tweezers or whatever so you get a good Z offset.
4) Bed tramming wizard using CR Touch probe — no paper needed for tramming.
5) Host action commands are on (no idea why Sovol had this off). This is useful for OctoPrint, etc.
6) Cancel Object is activated (not really needed if you use OctoPrint, but allows you to live cancel objects in a multi-object print). This requires slicer setup to use. If you use OctoPrint you can add the exclude region plugin to get the same effect and more.
7) Power fail resume is removed from the firmware. If you need this, let me know and I can add it back.
8) Emergency parser enabled — allows OctoPrint to send emergency stop (M112) instantly.
9) S-Curve acceleration enabled for smoother motion.
10) Print counter enabled — tracks total prints, print time, and filament used (view with M78).
11) Custom Commands menu with two shortcuts:
   - Full Autotune: runs PID autotune on hotend (200C) and bed (60C) and saves to EEPROM.
   - Level Bed & Save: homes, runs full 7x7 bed level, and saves mesh to EEPROM.

I recommend doing a PID tune of the bed and hotend, and calibrating your extruder e-steps after installing my firmware. Use the Full Autotune option in the Custom Commands menu.

My typical operation to level printer.

1) I do the bed tramming wizard first (Configuration -> Tramming Wizard). Home all axes first, then enter the wizard. It will move to each corner and probe it — turn the bed knob to bring the reading as close to 0.00 as possible. After going through all four corners, exit and re-enter the wizard as re-homing updates the Z reference. Repeat until all corners are near 0.00.

2) Set the Z offset — go to Configuration -> Probe Offsets and set the Z offset using the paper test (a small tug on paper). This must be done before bed leveling.

3) Run Level Bed & Save from the Custom Commands menu. This will home, probe all 49 points, and save the mesh automatically.

4) You can always live adjust your z offset if needed and save a better value if you find during your print it isn't where you want it to be.

That is basically it. I welcome any feedback or suggestions.  I do plan on looking into UBL leveling and a few other things, but this has got me printing great prints.
