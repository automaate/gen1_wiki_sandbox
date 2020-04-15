# Summary

This tutorial describes the basic steps to create a MPLAB® Harmony  Graphics Suite application without using a Harmony Board Support Package (BSP) or Graphics Template. 

# Description

This tutorial describes the basic steps to create a MPLAB® Harmony  Graphics Suite application without using a Board Support Package (BSP) or Graphics Template.  The tutorial uses the [SAM E70 Xplained Ultra Evaluation Kit](https://www.microchip.com/DevelopmentTools/ProductDetails/PartNO/DM320113). It starts with a new MPLAB® Harmony project and finishes with a graphics application equivalent to aria_quickstart.

The instructions in this tutorial assume that you have already installed following software:

* [MPLAB® X Integrated Development Environment](https://www.microchip.com/mplab/mplab-x-ide) v5.15 or later
* [MPLAB® XC32/32++ C Compiler](https://www.microchip.com/mplab/compilers) v2.20 or later
* [MPLAB® Harmony 3 Configurator](https://github.com/Microchip-MPLAB-Harmony/mhc/wiki)

The instructions also assume that you have acquired following hardware:

* [SAM E70 Xplained Ultra Evaluation Kit](https://www.microchip.com/DevelopmentTools/ProductDetails/PartNO/DM320113) 
* Display Module (choose one)
    *   [High-Performance 4.3" WQVGA Display Module (AC320005-4)](https://www.microchip.com/Developmenttools/ProductDetails/AC320005-4)
    *   [Display Module from MEB II](https://www.microchip.com/Developmenttools/ProductDetails/DM320005-2). 
* Standard USB A to micro-B cable

# Deep-Dive on SAM E70

## Install MHC
To install MHC, follow the [Harmony V3 MHC installation guide](https://github.com/Microchip-MPLAB-Harmony/mhc/wiki). Upon completion, proceed to **Configure Hardware**.

## Configure Hardware

SAM E70 Xplained Ultra board configuration is simply a board to PC connection using a standard USB A to micro-B cable. The connection provides power and debug communication. The connection is illustrated in the image below: 

![](images/deep_dive_e70_connect.png)
 
### Configure the 4.3” WQVGA Display 
* Disconnect the ribbon cable that connects the display to the interposer board.  The board is for the MEB 2 only, and not used on the SAM E70 Xplained Ultra kit

![Microchip Technology](images/quickstart_e70_display_back.png)

* Release the ribbon cable from the interposer board
* Release the black clamp on the E70’s J2 connector and turn the display over
* Insert the ribbon cable into J2 and close the clamp

![Microchip Technology](images/quickstart_e70_ribbon_cable.png)

![Important](images/Important%20Star.png) The board and display are powered by a Micro B – USB A cable from PC to the “Debug USB” port on the E70 board.


### Creating New Project Tutorial Steps

**Launch the MPLAB X IDE**
From the File pull-down menu:
* Select **New Project**. This will display the New Project dialog window
* Proceed to **Creating New Project Tutorial Steps**

**Choose Project**

In Categories window:
* Click **Microchip Embedded**
In Projects window
* Click **32-bit MPLAB Harmony Project**
* Click **Next**

![Microchip Technology](images/cnga_new_project_dialog.PNG)

![Important](images/Important%20Star.png) If **32-bit MPLAB Harmony Project** is not visible repeat software installation steps **Install MHC** above.

**Framework Selection** 

* Set **Framework Path:** to your Harmony v3 root installation directory. This path is not set by default. You must enter the path used at installation
* Select **Convert to Relative Path for Configuration**
* Click **Next**

![Important](images/Important%20Star.png) The Launch Framework Downloader button is used to download or configure a local framework. Because you have already installed H3, this button click is not required.

![Microchip Technology](images/deep-dive_manageframework.png)

**Project Settings**  

* Set **Location:** field to `deep-dive`. This will create a directory for your deep-dive application
* Set **Folder:** field to `sam_e70`. This will be the name of the MPLAB X project folder configured for SAM E70
* Set **Name:** field to `app-deep-dive`. This will be the name of your application displayed in MPLAB X
* Click **Next**

![Microchip Technology](images/deep-dive_namelocation.png)

**Configuration Settings** 

* Set **Name:** field to `sam_e70`. This will create a sam_e70 folder for configuration settings
* Select for **Device Family:** drop down, `ATSAM`
* Select for **Device Filter:** `same70`. This optional step helps narrow the possible device target selections to only this family
* Select for **Target Device:** drop down, `ATSAME70Q21B`
* Click **Finish**

![Note](images/Important%20Star.png) The selection of Target Device `ATSAME70Q21B` is required. The device name will enable the listing of the supported BSP specific for this board later in this tutorial. Using a different device may not give any selections for the BSP.

![Microchip Technology](images/deep-dive_configsettings.png)

When **Finish** is clicked, the following message may be displayed while the configuration database setup dialog is loaded.

![Microchip Technology](images/cnga_launching_configurator.png)

**Configuration Database Setup** 

* Select the following packages to load into the project:  `gfx`, `core`, and `bsp`
* Deselect all other packages
* Click **Launch**

![Microchip Technology](images/deep-dive_confdbsetup.png)

When Launch is complete, the Project Graph will display the following default components:

![Microchip Technology](images/deep-dive_e70_default_pg.png)

**Make Harmony Core Connections** 

Because this is a Harmony based application, you will need to use the Harmony Core Service Component. 

Under Available Components:
* **Expand** Harmony
* **Click** Core
When prompted to activate FreeRTOS
* **Click** No

You will also need the Time System Service.  

A Harmony component will list its Current Consumers and Available Consumers when a right click occurs on the its circle icons. 
* Right click the Core Service icon on Harmony Core Service component
* Select Available Consumers
* Select TIME
* Click the TMR icon on TIME System Service component
* Select TC0

![Microchip Technology](images/deep-dive_selectime.png)

**Make Graphics Connections** 

Because this is a GFX enabled application, you will need to select a graphics library. For this tutorial, we will use Aria. Under Available Components, **expand** Graphics>Middleware>Aria and **double click** Aria.

* Right click the GFX HAL icon on Aria component
* Select Satisfiers
* Select GFX Core

![Microchip Technology](images/deep-dive_gfx_hal_satis.png)

* Right click the Display Driver diamond icon on the GFX Core component
* Select Satisfiers 
* Select LCC
* Right click the SMC_CS diamond diamond icon on the LCC component
* Select Satisfiers 
* Select SMC_CS0

On completion, your Project Graph window should look similar to the following image:

![Microchip Technology](images/deep-dive_aria_project.png)

**Make Touch Connections** 

This is a touch enabled application. You will need to use the MaXTouch Controller. Under Available Components, **expand** Input/Touch and **double click** MaXTouch Controller. MaXTouch component will need an I2C driver, and the I2C driver will need the TWIHSO peripheral. Setup the Satisfiers for each.

* Right click the Input System Service icon on MaxTouch Controller component
* Select Satisfiers
* Select Input System Service
* Right click the DRV_I2C icon on maXTouch Controller component
* Select I2C
* Right click I2C icon on I2C component 
* Select TWIHSO
* Right click touch panel on maXTouch Controller component
* Select PDA TM4301B

If the display needs to be configured, then you will need to launch Display Manager.  For this tutorial, Display Managing is not required. See Getting started with Display Manager for more information.

![Microchip Technology](images/deep-dive_launch_displaymanager.png)

* Right click the Graphics Display icon on PDA TM4301B component
* Select GFX Core

You will need to tell Aria that touch is to be enabled:
* Select Aria
* Click Configuration Options
* Expand Code Generator Options 
* Select "Enable Input Event Interface?"

![Microchip Technology](images/deep-dive_aria_enabletouch.png)

The final Project Graphics should is illustrated below:

![Microchip Technology](images/deep-dive_e70_gfx_core_pg.png)

**Pin Settings** 

Using the SAM E70 schematic obtained from the users guide, the following PINs are required for successful hardware communication. Note: the drv_maxtouch and drv_gfx_lcc drivers require specific names for its pins. If you do not have the correct pin names a compiler output will display an error along with the expected name.

![Microchip Technology](images/deep-dive_e70_schematic.png)

The final pin settings are as follows:

![Microchip Technology](images/deep-dive_e70_twi_pins.png)

![Microchip Technology](images/deep-dive_e70_ice_pins.png)

![Microchip Technology](images/deep-dive_e70_touch_pins.png)

![Microchip Technology](images/deep-dive_e70_display_pins.png)

![Microchip Technology](images/deep-dive_e70_rgb_pins.png)

**Create a UI design using the new project wizard** 

When MHGC’s Welcome Dialog is displayed:
* Click the **Create a new project using the new project wizard** button

![Microchip Technology](images/quickstart_gc_newproject.png)

![Important](images/Important%20Star.png) If the Welcome Dialog does not appear, it is because it had been disabled previously.  The Welcome Dialog can be re-enabled by using MHGC’s File > Settings > General menu:

![Microchip Technology](images/QSG%2060%20Seconds%20Reenable%20Welcome%20Dialog.png)

* In the MPLAB Harmony Graphics Composer (MHGC) screen use the left-most icon to create a new graphics design.

![Microchip Technology](images/QSG%2060%20Seconds%20Create%20New%20Design.png)

In the New Project Wizard, for the **Color Mode** step:
* Select `RGB_565` 
* Click **NEXT**

![Microchip Technology](images/cnga_color_mode.png)

For the **Memory Size** step, It is not recommended to change this setting for this tutorial:
* Click **NEXT** to accept the default Flash Memory Size 

For the **Project Type** step:
* Choose the second option **create a new project using a basic template** 
* Click **NEXT**

![Microchip Technology](images/QSG%2060%20Seconds%20New%20Project%20Wizard%20New%20Project%20Type.png)

**Generate Compile** 

Generate the application’s code for the first time:
* Select the **Generate Code** button of MHC’s window

![Microchip Technology](images/QSG%2060%20Seconds%20Generate%20Code.png)

Save the project’s configuration. 
* Enter for **File name:** `sam_e70`
* Select `USER_ALL` as the Merge Strategy

![Microchip Technology](images/QSG%2060%20Seconds%20Generate%20Project%20USER_ALL.png)

* Click Generate: 

![Microchip Technology](images/QSG%2060%20Seconds%20Click%20Generate.png)

Now the project’s initial software has been configured.

**NOTE**: Here is a brief explanation of the different merge strategies that are available:
* **ALL**: The user will be prompted with a merge window for all generated files. This includes files that have no user modifications but are changed because of changes in MHC configuration or component updates. (This choice is always the safest.)
* **USER_ALL**: The user will always be prompted with a merge window for all generated files that contain user modifications.
* **USER_RECENT**: The user will be prompted with a merge window for all generated files that contain recent user modifications.
* **OVERWRITE**: All generated file content will be replaced by the contents of this generate operation. All user changes will be overwritten.

A compilation error could occur if a pin name is undefined. 
![Microchip Technology](images/deep-dive_undefined_pin.png) 


**Program and Run**

**Project Properties dialog.**  Right mouse click on the project’s name and bring up the Project Properties dialog

![Microchip Technology](images/QSG%2060%20Seconds%20Modify%20Project%20Properties.png)

* Under **Hardware Tool**, select `EDBG`
* Under **Compiler Toolchain**, select XC32 compiler `V2.20`
* Click OK

![Microchip Technology](images/QSG%2060%20Seconds%20Project%20Properties%20Mod2.png)

**Run Main Project**

* Select **Run Main Project**. This button will build, program, and run the application

![Microchip Technology](images/QSG%2060%20Seconds%20Run%20Main%20Project.png)

**Observe Display**

The demonstration will display the following UI:

![Microchip Technology](images/deep-dive_running.png) 