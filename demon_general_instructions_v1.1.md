
###################################################
#######>>>>>>>>>>  3DPrintDemon  <<<<<<<<<<<#######
#######   https://github.com/3DPrintDemon   #######

# IF YOU USE & LIKE THESE MACROS PLEASE CONSIDER SUPPORTING MY EFFORTS AT 
# https://ko-fi.com/3dprintdemon 



########################## VERY IMPORTANT ###############################
#########################################################################
FOR THIS TO WORK!!!
YOU MUST DO THIS!!!
ADD THE 3 LINES BELOW TO PRUSASLICER'S OR ORCA SLICER'S START GCODE SECTION

M104 S0
M140 S0
print_start EXTRUDER=[first_layer_temperature[initial_extruder]] BED=[first_layer_bed_temperature] HEIGHT=[first_layer_height] LAYER=[layer_height] FILAMENT=[filament_type] EXTRUSION=[extrusion_width] 

#########################################################################
### IF YOU USE CURA ### 
# ADD THE 3 LINES BELOW TO CURA SLICER'S START GCODE SECTION, BUT YOU WILL ALSO NEED TO MAKE CHANGES TO THE MACROS THEMSELVES - SORRY :-{

M109 S0
M190 S0
print_start EXTRUDER={material_print_temperature_layer_0} BED={material_bed_temperature_layer_0} HEIGHT={layer_height_0} LAYER={layer_height} FILAMENT={material_type} EXTRUSION={line_width}

#########################################################################
CURA USERS - You will need to modify all instances of 'PET' & 'FLEX' in the macros to 'PETG' & 'TPU 95A'. Also do not use Cura's 'PLA+' setting, Just use 'PLA'.
Yes, I know its a hassle...
But tbh, why are you still using Cura?! lol ;-p
#########################################################################

ALL SLICERS....

Your slicer's Start G-Code box most only contain those 3 lines above, plus the Mainsail layer count command - see the Mailsail website's slicer section for your slicer.

https://docs.mainsail.xyz/overview/slicer

#########################################################################
Also be sure to add the line below in your slicer's End G-Code box

PRINT_END

#########################################################################

This macro relies on you setting the correct filament type in your slicer! BE SURE YOU DO THIS! OR IT WILL NOT WORK!!

#########################################################################
IMPORTANT!!!!!
#########################################################################

You must [include] all Demon .cfg files in your printer.cfg file for this pack to work! The versions must also meet the currently expected versions, and yes the macros will check!

Create a new folder in Mainsial & call it demon_macros
Then in your printer.cfg paste in [inculde ./demon_macros/*.cfg]

That will automatically incudle all files in that folder with .cfg
NOTE: this will also include ANY old files already there if you dont delete them on an future update.
It just lets you include all files automatically.

#########################################################################

Dont Miss this....
Make sure you download install these files they are REQUIRED for these macros to work correctly.
https://github.com/3DPrintDemon/Non_Blocking_Wait_Sovol/releases/tag/Heat_Soak_Timers_V1.0

#########################################################################

READ THIS PAGE
https://github.com/3DPrintDemon/Demon_KLIPPER_Essentials/releases 

For more cool stuff visit...
https://github.com/3DPrintDemon

AUTO POWER ON/OFF BUTTON & REMOTE POWER CONTROL
https://github.com/3DPrintDemon/BTT-Relay-v1.2-Moonraker_INSTANT_Power-On-Button

AUTOMATIC ONLINE PRINTER FILES BACKUP
https://github.com/3DPrintDemon/Auto_Backup_Your_Klipper_Printer

#########################################################################

The _RET_CALI_START macro is used when calibrating your retraction settings with files generated at:

http://www.retractioncalibration.com/

All you need do is paste _RET_CALI_START into the website's "Custom Gcode" box next to the green "Generate Gcode" button This is without a doubt the absolute BEST retraction test out there!

#########################################################################


##################################################################################################################################################
## NOTE: THIS FEATURE DOES NOT WORK ON THE SOVOL'S OWN BRAND SV06/+/SV07/+ KLIPPERSCREEN as it is not possible to edit the home screen on their device.
## Works on other Klipper systems!
##################################################################################################################################################


NEW CUSTOM MENU!
Copy & paste these lines to your Klipperscreen.conf file, it will give you a new filament handling menu for the included macros...
NOTE: You'll need to restart Klipperscreen service for the changes to take effect. Use power menu top right of Mainsail


[menu __main custom]
name: Prepare
icon: klipper

[menu __main custom ready_up_pla]
name: Ready Up PLA
icon: filament
method: printer.gcode.script
params: {"script":"ready_up_pla"}

[menu __main custom ready_up_asa]
name: Ready Up ASA
icon: filament
method: printer.gcode.script
params: {"script":"ready_up_asa"}

[menu __main custom ready_up_petg]
name: Ready Up petg
icon: filament
method: printer.gcode.script
params: {"script":"ready_up_PETG"}

[menu __main custom ready_to_load_unload]
name: Ready to Load Unload
icon: filament
method: printer.gcode.script
params: {"script":"ready_to_load_unload"}


##################################################################################################################################################


If you use a filament runout sensor copy this to your printer.cfg file...



########################################
# FILAMENT RUNOUT
########################################

[filament_switch_sensor filament_sensor]
switch_pin: ### #<<<<<< INSERT OWN PIN SV07/+ USE "PD11" OR SV06/+ USE "PA4"
pause_on_runout: True
insert_gcode:
    { action_respond_info("Insert Detected") }
runout_gcode:
    { action_respond_info("Runout Detected") }



##################################################################################################################################################

Be sure to [include mainsail.cfg] in your printer.cfg & then copy & paste the _ClIENT_VARIABLE macro below into your macros.cfg file to enable required system variables...

MAKE SURE YOU EDIT THEM CORRECTLY FOR YOUR OWN PRINTER!!!!!

##################################################################################################################################################



# Client variable macro for your printer.cfg
[gcode_macro _CLIENT_VARIABLE]
variable_use_custom_pos   : False ; use custom park coordinates for x,y [True/False]
variable_custom_park_x    : 5.0   ; custom x position; value must be within your defined min and max of X
variable_custom_park_y    : 210.0   ; custom y position; value must be within your defined min and max of Y
variable_custom_park_dz   : 2.0   ; custom dz value; the value in mm to lift the nozzle when move to park position
variable_retract          : 1.0   ; the value to retract while PAUSE
variable_cancel_retract   : 5.0   ; the value to retract while CANCEL_PRINT
variable_speed_retract    : 35.0  ; retract speed in mm/s
variable_unretract        : 1.0   ; the value to unretract while RESUME
variable_speed_unretract  : 35.0  ; unretract speed in mm/s
variable_speed_hop        : 15.0  ; z move speed in mm/s
variable_speed_move       : 100.0 ; move speed in mm/s
variable_park_at_cancel   : False ; allow to move the toolhead to park while execute CANCEL_PRINT [True/False]
variable_park_at_cancel_x : None  ; different park position during CANCEL_PRINT [None/Position as Float]; park_at_cancel must be True
variable_park_at_cancel_y : None  ; different park position during CANCEL_PRINT [None/Position as Float]; park_at_cancel must be True
# !!! Caution [firmware_retraction] must be defined in the printer.cfg if you set use_fw_retract: True !!!
variable_use_fw_retract   : False ; use fw_retraction instead of the manual version [True/False]
variable_idle_timeout     : 0     ; time in sec until idle_timeout kicks in. Value 0 means that no value will be set or restored
variable_runout_sensor    : ""    ; If a sensor is defined, it will be used to cancel the execution of RESUME in case no filament is detected.
#                                   Specify the config name of the runout sensor e.g "filament_switch_sensor runout". Hint use the same as in your printer.cfg
# !!! Custom macros, please use with care and review the section of the corresponding macro.
# These macros are for simple operations like setting a status LED. Please make sure your macro does not interfere with the basic macro functions.
# Only  single line commands are supported, please create a macro if you need more than one command.
variable_user_pause_macro : ""    ; Everything insight the "" will be executed after the klipper base pause (PAUSE_BASE) function
variable_user_resume_macro: ""    ; Everything insight the "" will be executed before the klipper base resume (RESUME_BASE) function
variable_user_cancel_macro: ""    ; Everything insight the "" will be executed before the klipper base cancel (CANCEL_PRINT_BASE) function
gcode:



#########################################################################
For more cool stuff visit...
https://github.com/3DPrintDemon

#########################################################################
BEFORE FIRST USE
#########################################################################

CHECK YOUR VALUES ARE CORRECT BEFORE USE, THIS IS VITAL & TOTALLY ON YOU!
DO NOT BLINDLY USE ANY OF THESE DEFAULT VALUES!!
USE THESE MACROS AT YOUR OWN RISK! 
DONT CRY TO ME IF YOU DIDN'T CHECK/CHANGE VALUES & YOU BREAK THINGS!

>>>>>>>>>>>>>>>>>>>>>>>>>!!WARNING!!<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<
THIS START CODE USES RELATIVE EXTRUSION!! SET IT IN YOUR SLICER!


################ IMPORTANT!!! BUILD NEW BED MESHES WITH THE BED AT THE TEMPS YOU PRINT AT FOR EACH TYPE OF FILAMENT LIST BELOW! ###################
##################################### ALLOW TO HEAT SOAK 10-15 MINUTES THEN HOME BEFORE BUILDING MESH!! ###########################################
########################################### BUILD & STORE 5 MESHES TOTAL INCLUDING YOUR DEFAULT ##################################################
################################################ DO NOT OVERWRITE YOUR "DEFAULT" MESH!!! ##########################################################

default (to use with PLA)
ASA
ABS
PETG
TPU


###################################################
#######>>>>>>>>>>  3DPrintDemon  <<<<<<<<<<<#######
#######   https://github.com/3DPrintDemon   #######

# IF YOU USE & LIKE THESE MACROS PLEASE CONSIDER SUPPORTING MY EFFORTS AT 
# https://ko-fi.com/3dprintdemon 




##################################################################################################################################################

SV07/+ & SV06/+ Owners with the new Sovol Klipper screens YOU NEED TO DO THIS.....!

##################################################################################################################################################

Go into your printer.cfg 

Now comment out the Sovol macros in the printer.cfg
• [gcode_macro CANCEL_PRINT]
• [gcode_macro START_PRINT]
• [gcode_macro PAUSE]
• [gcode_macro RESUME]
• [gcode_macro PRINT_END]
• [gcode_macro PRINT_START]

Be sure to get them all! Dont worry you wont need them.


NOTE: If you have a PLUS size printer you can change the variable_custom_park_y to read 290 instead of 210

NOTE: You will probably see some weird errors due to the customised Sovol Klipper code that's being used on these systems about "no attributes for 'bed'" & "must home axis first".

This is normal & to be expected for this non-standard Klipper build being used & has been reported to Sovol. These errors should not cause problems as my own SV07+ machine does both yet my other 4 machines on regular unedited main branch Klipper are perfectly fine WITH NO ERRORS!

Happy printing!!





