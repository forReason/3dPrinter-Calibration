# 3dPrinter-Calibration
this repository serves the purpose of calibrating your 3d Printer. It is tested with an ender 3 v2

# New Printer Setup
1. Build together (youtube videos often have better tutorials)

## 2. CHECK ALL SCREWS
Oftentimes, not all screws are properly tightened, especially on cheap printers like the ender 3

## 3. Check Belt tensions
the belts should be tight, but not so tight that it causes a lot of stress on the motors.

## 4. Calibrate extruder motor (e-steps)
** You might need to preheat the nozzle before the printer allows you to extrude. Be aware, the nozzle gets very hot during that process, dont place it on flammable area. It is best to leave the hotend mounted and unmount the extruder instead or remove the bowden tubing. Some printers/custom firmware will allow you to set the minimum extrusion temperature. I set mine to 20°c.
4.1 Remove the connection between extruder and hotend. If you have a Bowden style extruder, remove the bowden tube at the hotend side. If you have a direct drive extruder, either dismount the extruder or the hotend.
4.2 Feed some Filament though the extruder. Cur it flush with the exit hole of the extruder.
4.3 To make sure values are not totally off, set a manual extrusion to 10mm (or use the `e-steps 10mm.gcode`). Check if the filament is carried into the direction of the hotend. It might be quite slow..
4.4 Cut the filament flush again on the exit hole of the extruder. Now measure the length of the Filament.  
Use the following formula, to calculate the correct e-steps: `e-Steps = 10mm / (actual mm * current e-steps)`. (or use the calculation excel sheet in How-Tos Documents and tools)
4.5 Set the newly calculated e-steps in the firmware and dont forget to save them.
4.6 With a caliper, measure 100mm (10cm) in front of the extruder, try to measure them as precisely as possible and mark the filament with a marker at that position as precisely as possible.
4.7 Print/"Execute" the `e-steps 100mm.gcode` file. The marker on the filament should now be close to the extruder intake.
4.8 Use the electronic adjustment to feed the filament further in or pull it back until the mark lines up with the extruder intake. Take note hof how many MM the filament got pulled in too much or too little (if you have to add 1.5 mm to set it flush, the extruded length was 98.5 for example. If you had to take back the filament by 1mm, it extruded 101mm.
4.9 Calculate the new e-steps with the following formula (or use the 100mm calculator in the excel): `e-Steps = 100mm / (actual mm * current e-steps)`
5. Set the e-steps in your firmware and save. Repeat the process until you are happy with the result. 

## 5. Check correct motor movement direction and end-stops
5.1 by manually moving the axis while the printer is turned off: Make sure that the endstops are actually beeing hit/triggered by the carriages
5.2 Move all axes in the corresponding middle position
5.3 Execute the move command on the screen. **Have your hand ready at the off switch**
- The axis should move to the direction of your endstops. **If an axis moves away from the End-Stop switch, turn off the printer, adjust the motor direction in settings**
- Do not let the carriages run into the endstops. Check them by triggering the end-stop switch manually with the finger. **If the Movement does not stop, something is wrong with your end-stop!**
## 6. Level bed
6.1 Set the bed leadscrews to minimum height
6.2 While the printer is switched off, move down the Z-Axis manually, until you hear the click of the end stop switch.
6.3 Roughly adjust the Bed-Height a little under the printing-nozzle
6.4 Check that all 4 corners are not too high
6.5 Turn off the printer, press the home button. Your printer should correctly find the home position, if you did everything correctly in section 4.
6.6 Execute/"Print" the bed_level.gcode file. It will automatically move between the 4 corners of the bed, until you hit stop. (tested on ender 3 v2)
6.6.1 Be careful, the Printbed gets preheated to 60°c. Dont burn your self.
6.6.2 In each corner, take a thin object (e.g. sheet of paper) and raise the corresponding corner until you can feel the nozzle scrathing on the paper if you move it back and forth. Doing this will un-level the other corners.
6.6.3 once you are satisfied with the particular corner, approve with the display button. The printhead will move to the next corner. Repeat for all corners until the bed is level (multiple rounds are required, as leveling one corner will un-level the other corners)
6.6.4 start printing the bed-level test, it will put a rim around the print first. during the rim, you can still do adjustments. If the printhead is too high in general, adjust down with the e-steps. The line should not be squished but shoud stick to the heatbed. You can do fine adjustments with the levelin-screws here. If you are not happy with the result or made plenty of adjustments, you might want to cancle the print, remove the parts that have been printed already and start the print again.

### common failures:
- The Filament does not stick: Bed is too low/nozzle too far from bed
- The Filament bulges up, gets a rough texture or ripples/frizzes/fuzz: The bed is slightly too high/nozzle too close too bed
- The Filament lines separate: Nozzle slightly too far from bed
- The Filament becomes really thin: bed too close

## 7. Calibrate Flow rate
Print the simple calibration cube with one line only. Alternatively print the file from the according filament type folder. Afterwards, measure the wall thickness. It should be exactly the size of your Nozzle.  
If it is not, calculate a new flow-rate with the following formula (or use the flow rate calculation in the excel for most standard 0.4mm nozzles):
`flow = (currentFlow * thickness should be) / thickness is`

## 8. Check dimensions
Print the x/y/Z calibration cube. It should be 20x20x20mm
