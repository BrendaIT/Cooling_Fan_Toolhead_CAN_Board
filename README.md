# Cooling_Fan_Toolhead_CAN_Board
This MOD arises from the need for active cooling on the Toolhead Board CAN for VORON2.4 350 Afterburner with cable chain. When printing ABS or other materials, with the doors closed the Toolhead Board CAN reaches temperatures around 70/80 degrees. In my case the Board went into ERROR_MCU thus stopping the print in progress.
Right here comes the need to implement a fan for Active Cooling on the CAN Board.

I took into account various factors such as:

- Reduced weight in order not to overload the X axis.

- That it was compact in the distance between the motor and the rear part of the Gantry, so as not to touch the Chain.

-That it was efficient to keep the board temperature stable.

- That it was easy to assemble and compatible with the cards on the market:

FLY SHT42, Huvud v0.61, BTT EBB42 CAN v1.0.
STL files are printed in ABS, with 30% fill, 0.20 layer height and internal support.


MATERIAL:

The fan is a Radial 30x30x10mm LINK: https://www.amazon.it/gp/product/B08MKLDGQR/ref=ppx_yo_dt_b_asin_title_o01_s00?ie=UTF8&psc=1
The screws: 2x M3 countersunk head (fixing the support to the motor) 4x M3x20mm (fixing the board to the support) 3x M3x5mm (for fixing the chain)


PRINTING:
-Print the two STL files, bearing in mind that the Fan_Cooling file must be printed with support, as in the photo in the Image folder.


ASSEMBLY:
Step 1: Using the soldering iron, insert the 3 M3 inserts for fixing the chain.

Step 2: Remove the 2 rear / upper screws of the Nema17 motor of the Afterborner, fix the chain holder base with the two screws.


Step 3: Screw in the three screws for securing the chain.


Step 4: Connect all connectors to the card.


Step 5: First insert the fan wires into the hole in the upper left of the Holder, then gently insert the Fan so that the propellers are facing up.


6 Step: Align the board with the four screw holes in the motor mount.


Step 7: Bundle and align the cables so that they do not pinch when tightening the screws, set the fan holder down by aligning the four holes on the top of the board.


Step 8: Screw the four board screws to the motor mount.


9 Step: Connect the fan to a Pin of the Motherboard (you can do it in two ways: 1 connect in parallel to the cooling fan of the hotend on the SHT42, Huvud or EBB Toolboard, in this case we will not need any macro, because the fan will turn on as soon as the hotend fan turns on. 2 insert an extra wire in the cable chain and lead to the printer motherboard, connect to an available PIN, this will be our Negative pole, the positive pole must be taken directly from the connector Power of the Toolboard in this case, we need the macro to set the fan)

Step 10: The Gcode Macro must be inserted in your printer.cfg, remember to change the PIN with your settings, if you have Activated the MCU SHT42 Temperature... 
Comment the session:


 #[temperature_sensor FLY-SHT42]
 
 #sensor_type: temperature_mcu
 
 #sensor_mcu: sht42

and add the new macro which already includes the MCU temperature reading.


 # Printer.cfg

[temperature_fan sht42_cool]

pin: PD14 # Bed Heater terminals, XYE board

max_power: 1.0

max_speed: 1.0

min_speed: 0.05

shutdown_speed: 0.0 # 0.9

kick_start_time: 0.1

cycle_time: 0.01 # 0.01

off_below: 0.25 # 0.15

sensor_type: temperature_mcu

sensor_mcu: sht42

#sensor_pin: PF4 # TH0 socket, Z board

min_temp: 0

max_temp: 80

target_temp: 50.0

control: pid

hardware_pwm: false

pid_kp: 40.0

pid_ki: 5.0

pid_kd: 0.01

#gcode_id: A

The game is done! If the temperature of the Toolboard goes above 50.0 degrees the fan turns on thus keeping the card not above 50.0 and consequently avoiding errors.

Good Printing!
