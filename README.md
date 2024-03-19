Airboat
=======
This project is an agile and speedy airboat designed with spare parts that I had laying around.  
Like most FPV pilots, I have a handfull of spare or broken parts laying around and I wanted to use on a watercraft design.
After countless testing and hull re-designing I finally landed on what I think is a good balanced hull design.
The hull is able to be taken up to full throttle and fully turned without capsizing or upsetting the hull too much.  
  
Here is the list of parts I used to create the airboat, but many other tinywhoop parts will work as well.

Parts list:
===========
- Flight Controller: Happymodel Diamond F4 ELRS
- Motors: 2x newbeedrone 0703 16420kv
- Props: Gemfan 1610 biblade
- Battery: Betafpv 300mah bt2.0
- bit of velcro for battery strap
- conformal coating

How to print:
=============
This project is broken into 3 printable parts.
- [Hull](airboat_design/airboat_neo_hull.stl): This is the hull of the boat without any electronics or additional features (print upside down with supports touching buildplate)
- [Carrier](airboat_design/carrier.stl): This is the model where all of the electronics are mounted, this can be moved to different hull designs (print flat side down with no supports)
- [Carrier plug](airboat_design/airboat_carrier_plug.stl): This is a plug that fits in behind the carrier (it helps push the carrier forward to balance the weight on the hull and fills the gap behind the carrier) (print large side down with no supports)

You will need to print one of each of these pieces to complete your airboat.

Programming FC:
===============
If you decided to use an old flight controller like I did, you'll need to configure it in betaflight to work as an airboat.
I have uploaded my [CLI dump](cli_dump/BF_airboat_diamondf4_dump.txt) if anyone is using a diamond f4, otherwise you'll need to do a few different configurations.

- Motor Resource allocation: You need to only enable the 2 motors that are being used.
  ```
  resource MOTOR 1 B07
  resource MOTOR 2 B10
  resource MOTOR 3 NONE
  resource MOTOR 4 NONE
  
  save
  ```

- Custom Motor Mixes: this will allow us to use a custom motor mix allowing us to turn using differential thrust
  ```
  mixer custom
  mmix reset
  mmix 0  1.000  0.000  0.000 -1.000
  mmix 1  1.000  0.000  0.000  1.000
  
  save
  ```

- Disable Runaway Prevention: On one of my boats, runaway prevention stopped me from hitting full power on the airboat, so I ended up disabling it
  ```
  set runaway_takeoff_prevention = OFF
  
  save
  ```

- Disable VTX: We need to disable the built in VTX if our FC has one so we dont cook the board. This can usually be accomplished by bridging a solder pad or disabling in software.  
  I have diabled the VTX in the `Configuration` -> `Other Features` tab in betaflight.
