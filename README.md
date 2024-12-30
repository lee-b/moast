# MOAST
# (or, Moon on a Stick Tools)

NOTE: no code here yet; the following is documentation of intended functionality, for now.

This is a SIMPLE command-line frontend to lots of astrophotography tools. It's for grabbing images of objects in space, CORRECTLY.  What you do after that (science, or artistic interpretation with false color, or whatever) is up to you, but there is no reason for a lot of manual monitoring or intervention in the data acquitision process: we just want to get the data accurately, to begin with.

## Installation

```
# apt-get install pipx
# pipx install moast
```

## Setup

```
moast add telescope "My-Scope" --aperture 200mm --focal-length 2000mm
moast add mount "My-Mount" --type Alt-Az --autoguided=True --slew-rate "4deg/sec"
moast add filter "Near-IR-Pass" --wavelengths "300nm-400nm" --description "Near infrared"
moast add filter "Luminance" --wavelengths "400nm-700nm" --description "Luminance filter for capturing overall brightness in visible spectrum."
moast add filter "Red" --wavelengths "620nm-750nm" --description "Red filter for capturing red wavelengths in the visible spectrum."
moast add filter "Green" --wavelengths "500nm-570nm" --description "Green filter for capturing green wavelengths in the visible spectrum."
moast add filter "Blue" --wavelengths "450nm-495nm" --description "Blue filter for capturing blue wavelengths in the visible spectrum."
moast add filter "Ultraviolet" --wavelengths "300nm-400nm" --description "Ultraviolet filter for capturing UV light."
moast add sensor "Mirrorless1" --sensor "CMOS" --resolution "4000x3000" --pixel-size "5.4um" --description "Astrophotography camera designed for deep-sky imaging."
moast add sensor "AstroCam1" --sensor "CMOS" --resolution "4000x3000" --pixel-size "1.56um" --description "Astrophotography camera designed for deep-sky imaging."

moast add filter-wheel "MyFilterWheel" --reconfigure-time "3s"
moast add filter-wheel-slot-content "MyFilterWheel:Slot1:IR-Cut"
moast add filter-wheel-slot-content "MyFilterWheel:Slot2:Luminence"
moast add filter-wheel-slot-content "MyFilterWheel:Slot3:Red"
moast add filter-wheel-slot-content "MyFilterWheel:Slot4:Green"
moast add filter-wheel-slot-content "MyFilterWheel:Slot5:Ultraviolet"

moast add config "MyScope-AstroCam1-LRGBUV" --scope "My-Scope" --mount "MyMount" --sensor "Mirrorless1" --filter-wheel "MyFilterWheel"
```

## Imaging

```
$ moast add plan "plan-1" --target "M 31" --summarise
Plan is as follows:
  Config: "MyScope-AstroCam1-LRGBUV"
  Scope: "MyScope"
  Mount: "MyMount"
  Autoguider: "True"
  Autoguider-Type: "internal"
  Reconfigure Time: 5s
  Slew Rate: 4 degrees per second
  Slew Rate scale: 1x
  Channels:
    - "Near-IR-Pass"
    - "Luminence"
    - "Red"
    - "Green"
    - "Blue"
    - "Ultraviolet"
  AFOV: 2 degrees
  Panels: 4
  Exposures per panel: 3
  Exposure Time: 3m
  Total Images: 12
  Total Imaging time: 12 minutes 0 seconds (720 seconds)
  Total time (post initial slew): 13 minutes 1 seconds (781 seconds)

$ moast run-plan "plan-1"
Connecting to equipment... complete.

Beginning slew... complete

Capturing panel 1:
   Near-IR-Pass: complete.
   Red: complete.
   Green: complete.
   Blue: complete.
   Ultraviolet: complete.

Capturing panel 2:
   Near-IR-Pass: complete.
   Red: complete.
   Green: complete.
   Blue: complete.
   Ultraviolet: complete.

Capturing panel 3:
   Near-IR-Pass: complete.
   Red: complete.
   Green: complete.
   Blue: complete.
   Ultraviolet: complete.

Capturing panel 4:
   Near-IR-Pass: complete.
   Red: complete.
   Green: complete.
   Blue: complete.
   Ultraviolet: complete.

Disconnecting from equipment... complete.

Processing images:
   Panel 1:
       Exposure 1: De-rotating... complete.
       Exposure 2: De-rotating... complete.
       Exposure 3: De-rotating... complete.
       Stacking exposures... complete.

   Panel 2:
       Exposure 1: De-rotating... complete.
       Exposure 2: De-rotating... complete.
       Exposure 3: De-rotating... complete.
       Stacking exposures... complete.

   Panel 3:
       Exposure 1: De-rotating... complete.
       Exposure 2: De-rotating... complete.
       Exposure 3: De-rotating... complete.
       Stacking exposures... complete.

   Panel 4:
       Exposure 1: De-rotating... complete.
       Exposure 1: De-rotating... complete.
       Exposure 3: De-rotating... complete.
       Stacking exposures.. complete.

Stitching panels... complete.

4 Panel, 6 channel capture of M 31 successful.

$ moast data list
-------------------------------------------------------------------------------------------------------------------------------------------------------
| Plan   | Target                   | Capture Start    | Capture End         | Num Images | Num Panels | Exposures Per Panel | Num Exposures | Size   |
+--------+--------------------------+------------------+---------------------+------------+------------+---------------------+---------------+--------+
| plan-1 | M 31 (Andromeda Galaxy)  | 2025/01/01 12:00 | 2025/01/01 12:15:25 |          1 |          4 |                   3 |            12 |  250GB |
-------------------------------------------------------------------------------------------------------------------------------------------------------

$ moast view plan-1
Launching default FITS viewer...
```

