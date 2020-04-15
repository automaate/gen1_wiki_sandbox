# ![Microchip Technology](images/mhgs.png) Quickstart Curiosity 2.0 PIC32MZEF Development Board

This guide describes the basic steps to create a graphics-enabled application using the
[Curiosity PIC32MZEF Development Board](https://www.microchip.com/DevelopmentTools/ProductDetails/PartNO/DM320104) connected to a  [WQVGA](https://www.microchip.com/Developmenttools/ProductDetails/AC320005-4). You will build a simple application that displays an image and touch button. It starts with the creation of a new MPLAB® project and finishes with a graphics application equivalent to aria_quickstart.

The demonstration will render the following image on the display:

![Microchip Technology](images/deep-dive_running.png)

<details><summary>Who should use this guide</summary>
<p>

This guide is intended for developers who are building applications a custom PIC32MZEF board similar to or the same as the [Curiosity PIC32MZEF Development Board](https://www.microchip.com/DevelopmentTools/ProductDetails/PartNO/DM320104) and the [ WQVGA Display Module (AC320005-4)](https://www.microchip.com/Developmenttools/ProductDetails/AC320005-4). 

</p>
</details>


<details><summary>What this guide contains</summary>
<p>
You will build a simple application that displays an image and touch button. It starts with the creation of a new MPLAB® project and finishes with a graphics application equivalent to aria_quickstart. Here are the primary steps to create a graphics application for your PIC32MZEF hardware:

1. Create a new project and configure clock for PIC32MZEF.
    *  Create MPLAB Harmony v3 Project using MPLAB X IDE
    *  Verify Clock Settings
2. Configure Harmony components for graphics middleware and drivers
3. Configure pins for external graphics communication
4. Generate Code
5. Add application code to project
6. Build, program and observe outputs
</p>
</details>

<details><summary>Materials you will need</summary>
<p>

## Documentation

|Documentation|Description|
|----|----|
|[PIC32MZ EF Curiosity Development Board User’s Guide](http://ww1.microchip.com/downloads/en/DeviceDoc/70005282B.pdf) | User guide and schematics|

## Hardware 

|Hardware|Description|
|----|----|
| [Curiosity PIC32MZEF Development Board](https://www.microchip.com/DevelopmentTools/ProductDetails/PartNO/DM320104)|Development Board |
| [ WQVGA Display Module (AC320005-4)](https://www.microchip.com/Developmenttools/ProductDetails/AC320005-4). | High-Performance 4.3" WQVGA Display Module |
| [WQVGA Display Module from MEB II](https://www.microchip.com/Developmenttools/ProductDetails/DM320005-2) |  Alternative High-Performance 4.3" WQVGA Display Module if an MEB-II board is available |
| Standard USB A to micro-B cable| PC debugging connector. |

> **_NOTE:_** The Curiosity PIC32MZEF Development Board includes an on-board Embedded Debugger (EDBG), which requires no additional hardware to get started. For programming/debugging, the EDBG connects to the host PC through the USB micro-B connector on the Curiosity PIC32MZEF Development Board.

<details><summary>Hardware Setup</summary>
<p>

Curiosity PIC32MZEF Development Board is connected to the display using the display ribbon cable. Programming is a board to PC link using a standard USB A to micro-B cable. The connection, illustrated below, provides power and debug communication.

![](images/deep_dive_e70_connect.png)
 
If your WQVGA display cable is connected to a interposer board, following these steps:

* Disconnect the ribbon cable that connects the display to the interposer board.  The board is for the MEB 2 only, and not used with the Curiosity PIC32MZEF Development Board.

![Microchip Technology](images/quickstart_e70_display_back.png)

* Release the ribbon cable from the interposer board. 
* Release the black clamp on the PIC32MZEF’s J2 connector and turn the display over. 
* Insert the ribbon cable into J2 and close the clamp.

![Microchip Technology](images/quickstart_e70_ribbon_cable.png)

![Important](images/Important%20Star.png) The board and display are powered by a Micro B – USB A cable from PC to the “USB Debug” port on the Curiosity PIC32MZEF Development Board.
</p>
</details>

## Software

|Software|Description|Install|
|----|----|----|
| [MPLAB® X Integrated Development Environment](https://www.microchip.com/mplab/mplab-x-ide)| v5.15 or later| [Install MPLAB IDE](https://microchipdeveloper.com/install:mplabx) |
| [MPLAB® XC32/32++ C Compiler](https://www.microchip.com/mplab/compilers) | v2.20 or later | [Install Compiler](https://microchipdeveloper.com/install:xc32)|
| [MPLAB® Harmony 3](https://github.com/Microchip-MPLAB-Harmony/mhc/wiki)| v3.5 or later | [Install Harmony v3](https://microchipdeveloper.com/harmony3:mhc-overview#install)|


> **_NOTE:_** This project has been verified to work with the following versions of software tools:
MPLAB X IDE v5.20, MPLAB XC32 Compiler v2.20, MPLAB Harmony v3.5.0

> **_NOTE:_** Because we regularly update our tools, occasionally you may discover an issue while using the newer versions. If you suspect that to be the case, we recommend that you use the same versions that the project was tested with.

</p>
</details>

# QuickStart steps

## Create a new MPLAB Harmony v3 project

1. Select **File > New Project** from the main IDE menu.

2. In the **Categories** pane of the **New Project** dialog, select **Microchip Embedded**. In the **Projects** pane, select **32-bit MPLAB Harmony 3 Project**, then click **Next**.

![Microchip Technology](images/project_creation_setup.png)

> **_NOTE:_** If **32-Bit MPLAB Harmony 3 Project** selection is not displayed, [Download MPLAB Harmony Framework](https://microchipdeveloper.com/harmony3:mhc-overview#download).

3. In the **Framework Path** edit box, browse to the folder you downloaded the framework to. If you haven't done this, or want to download it to a different folder, click the **Launch Framework Downloader** button, then click **Next**.

> **_NOTE:_**  For more information on the framework downloader, see the, [Download MPLAB Harmony Framework](https://microchipdeveloper.com/harmony3:mhc-overview#download) section of the "MPLAB® Harmony Configurator Overview" page.

![Microchip Technology](images/project_path_setup.png)

4. In the **Project Settings** window, apply the following settings:

    * **Location**: Indicates the path to the root folder of the new project. All project files will be placed inside this folder. The project location can be any valid path, for example: C:\microchip\harmony\v3.
    * **Folder**: Indicates the name of the MPLABX .X folder. Enter “**pic32_mzef**” to create a **pic32_mzef.X** folder.
    * **Name**: Enter the project’s logical name as “**my_board**”. This is the name that will be shown from within the MPLAB X IDE.

> **_NOTE:_**  This must be a valid directory name for your operating system. The Path box is read-only. It will update as you make changes to the other entries.

    * Click Next to proceed to Configuration Settings.

![Microchip Technology](images/pic32_mzef_newprj3.png)

5. Follow the steps below to set the project’s Configuration Settings.

    * **Name**: Enter the configuration name as “pic32_mzef”.
    * **Target Device**: Select “**PIC32MZ2048EFM144**” as the target device.
    * Click **Finish** to launch the MHC.

> **_NOTE:_** You can select the Device Family or enter a partial device name to filter the list in Target Device in order to make it easier to locate the desired device.

![Microchip Technology](images/pic32_mzef_newprj4.png)

> **_NOTE:_** The **New Project Wizard** opens a Configuration Database Setup window to allow you to review the packages that will be used by the current project.

6. While the MHC tool launches, it will ask for the packages to be loaded. In the **Load** checkboxes list, select the **gfx**, **core**, and **bsp** packages and unselect all other packages.

![Microchip Technology](images/same70_launch_step.png)

Click **Launch** to launch the MHC Configurator tool with the selected packages.

* **Launching MPLAB Harmony Configurator**. The following message will be displayed while the project is loaded into MPLAB X.

![Microchip Technology](images/cnga_launching_configurator.PNG)

7. The MHC plugin’s main window for the project will be displayed. This is the initial project graph.

![Microchip Technology](images/pic32_mzef_initial_project_graph.png)

8. Before proceeding, set up the compiler toolchain. Click on the **Projects** tab on the top left pane. Right click on the project name **my_board** and go to **Properties**.

![Microchip Technology](images/project_view.png)

Make sure that XC32 (v2.20) is selected as the Compiler Toolchain for XC32. Click on **Apply** and then click on **OK**.

![Microchip Technology](images/pic32_mzef_xc32_setup.png)

## Verify Clock Settings

1. Launch **Clock Diagram** by going to **MHC** tab in MPLABX IDE and then select **Tools > Clock Configuration**.

![Microchip Technology](images/clock_configuration_open.png)

A new tab, **Clock Diagram**, is opened in the project’s main window.

2. Click on the **Clock Diagram** tab, scroll to the right and verify that SYSCLK is set to 200 MHz.

![Microchip Technology](images/clock_configuration_setup.png)

## Configure Software

1. Because this is a Harmony based application, you will need to use the **Harmony Core Service** Component. 

Under the bottom left tab, **Available Components**, expand **Harmony**.
Double click or drag and drop **Core** to add the **Harmony Core Service** to the project graph. When prompted to activate **FreeRTOS**, click **No**.

![Microchip Technology](images/pic32_mzef_mebii_coreselect.png)

![Microchip Technology](images/pic32_mzef_mebii_nortos.png)

2. You will also need the **Time System Service**.  

> **_NOTE:_** Harmony components lists Current Consumers and Available Consumers when a right click occurs on the circle icons. 

* On the **Harmony Core Service** component, right click the Core Service icon on Harmony Core Service component, select **Available Consumers**, then select **TIME**.

![Microchip Technology](images/pic32_mzef_mebii_timeselect.png)

* On the **Time System Service** component, right click the **TMR** icon, select **CORE_TIMER(core_timer)**.

![Microchip Technology](images/pic32_mzef_mebii_coretimer.png)


Because this is a GFX enabled application, you will need to select a graphics library. For this tutorial, we will use **Aria**. 

3. Under the bottom left tab, **Available Components**, expand **Graphics>Middleware**. Double click or drag and drop Aria to add the Aria graphics library to the project graph.

4. On the Aria component, right click the **GFX HAL**, select **Satisfiers**, and select **GFX Core**.

![Microchip Technology](images/same70_aria_gfxcore.png)

5. On the **GFX Core** component, right click the **Display Driver** icon, select **Satisfiers**, and select **LCC**.

![Microchip Technology](images/pic32_mzef_mebii_lccselect.png)

6. On the **LCC** component, right click **EBI_CS** diamond icon, select **Satisfiers**, and select **EBI (ebi)**.

![Microchip Technology](images/pic32_mzef_mebii_ebiselect.png)

7. On the **GFX Core** component, right click **Graphics Display** diamond icon, select **Satisfiers**, and select **PDA TM4301B (gfx_disp_pdatm4301b_480x272)**.

![Microchip Technology](images/pic32_mzef_mebii_4301select.png)

8. On the **PDA TM4301B** component, right click **Touch Panel** diamond icon, select **Consumers**, and select **MaXTouch Controller (gfx_maxtouch_controller)**.

![Microchip Technology](images/pic32_mzef_mebii_mxtselect.png)

9. On the MaXTouch Controller component, right click **DRV_I2C** diamond icon, select **Satisfiers**, and select **I2C (drv_i2c)**.

![Microchip Technology](images/pic32_mzef_mebii_i2cselect.png)

10. On the **MaXTouch Controller** component, right click **Input System Service** circle icon, select **Available Satisfiers**, and select **Input System Service (sys_input)**.

![Microchip Technology](images/pic32_mzef_mebii_sysinselect.png)

11. On the **I2C Driver** component, right click Input **I2C** diamond icon, select **Satisfiers**, and select **I2C1 (i2c1)**.

![Microchip Technology](images/pic32_mzef_mebii_i2c1select.png)

On completion, your **Project Graph** window should look similar to the following image:

![Microchip Technology](images/same70_final_project_view.png)

If the display needs to be configured, then you will need to launch **Display Manager**.  For this tutorial, Display Managing is not required. See Getting started with Display Manager for more information.

![Microchip Technology](images/deep-dive_launch_displaymanager.png)

## Configure Hardware

In this step, you will need to connect the PIC32MZ EF to the external touch controller and display modules.

Using the Curiosity PIC32MZ EF 2.0 Development Board schematic obtained from the [user guide](http://ww1.microchip.com/downloads/en/DeviceDoc/Curiosity_PIC32MZEF2.0_Development_Board_Users_Guide_DS70005400A.pdf).

> **_NOTE:_** If you are using a schematic for your custom board, map the required graphics pins to your board.

> **_NOTE:_** the drv_maxtouch and drv_gfx_lcc drivers require specific names for its pins. If you do not have the correct pin names a compiler output will display an error along with the expected name.

The pin mapping table below is made available for convenience.

#### Required Pin Settings
| Ball/Pin Number | Pin ID| Name| Function|Direction|Latch|
| --- | --- | --- | --- | --- | --- | 
| B9| RB1 | BSP_MAXTOUCH_CHG | GPIO | In| |
| M11| RA14 | SCL1 | SCL1 ||
| N11| RA15 | SDA1 | SDA1 ||
| M3 | RE3| TM4301B_BACKLIGHT| GPIO| OUT| High|


1. Open the Pin Configuration tabs by clicking **MHC > Tools > Pin Configuration**.

![Microchip Technology](images/open_pin_configuration.png)

2. Select the MHC Pin Settings tab and sort the entries by Port names as shown below.

![Microchip Technology](images/ports_pins_setup.png)

3. Use the table above to establish your Pin Settings.

## Generate Code

1. When done, before generating code, click **Save MHC State** as shown below.

![Microchip Technology](images/save_mhc_state.png)

2. Save the configuration in its default location when prompted.

3. Generate the code as shown below.

![Microchip Technology](images/generate_code_step1.png)

4. Click on the Generate button in the Generate Project window, keeping the default settings as shown below. If prompted for saving the configuration, click Save.

![Microchip Technology](images/generate_code_step2.png)

5. As the code is generated, MHC displays the progress as shown below.

![Microchip Technology](images/generate_code_step3.png)

6. Examine the generated code.

MHC will include all the MPLAB Harmony library files and generate the code based on the MHC selections. The generated code would add files and folders to your Harmony project

7. Navigate to the Projects tab to view the project tree structure.

8. Build the code by clicking on the **Clean and Build** icon ![Microchip Technology](images/build.png) and verify that the project builds successfully.

## Add application UI code to project

The UI design is already developed. Use Graphics Composer to insert the design into your project.

Launch the **Graphics Composer** from the MHC/Tools Menu:

![Microchip Technology](images/QSG%2060%20Seconds%20Launch%20MHGC.png)

* When MHGC’s Welcome Dialog is displayed. Click the **Create a new project using the new project wizard** button.

![Microchip Technology](images/quickstart_gc_newproject.png)

![Important](images/Important%20Star.png) If the Welcome Dialog does not appear, it is because it had been disabled previously.  The Welcome Dialog can be re-enabled by using MHGC’s File > Settings > General menu:

![Microchip Technology](images/QSG%2060%20Seconds%20Reenable%20Welcome%20Dialog.png)

* In the MPLAB Harmony Graphics Composer (MHGC) screen use the left-most icon to create a new graphics design.

![Microchip Technology](images/QSG%2060%20Seconds%20Create%20New%20Design.png)

In the New Project Wizard, for the **Color Mode** step, 
* Select `RGB_565` 
* Click **NEXT**.

![Microchip Technology](images/cnga_color_mode.png)

**Memory Size**

For the **Memory Size** step, accept the default Flash Memory Size and click **NEXT**. It is not recommended to change this setting for this tutorial.

![Microchip Technology](images/cnga_memory_size.png)

**Project Type**

For the **Project Type** step, chose the second option **create a new project using a basic template** and click **NEXT**.

![Microchip Technology](images/QSG%2060%20Seconds%20New%20Project%20Wizard%20New%20Project%20Type.png)

The MHGC window will display the following image:

![Microchip Technology](images/QSG%2060%20Seconds%20MHGC%20Screen%20Design.png)

You are now ready to build the code!

## Build, program and observe outputs

1. Verify that the display is connected to GFX Connector on the Curiosity PIC32MZ EF 2.0 Development Board.

2. The Curiosity PIC32MZ EF 2.0 Development Board allows using the Embedded Debugger (EDBG ) for debugging. Connect the Type-A male to micro-B USB cable to micro-B DEBUG USB port to power and debug the Curiosity PIC32MZ EF 2.0 Development Board.

3. Go to **File > Project Properties** and make sure that the EDBG is selected as the debugger under the **Hardware Tools** and XC32 (v2.20) is selected as the **Compiler Toolchain** for XC32.

4. Clean and build your application by clicking on the **Clean and Build** button as shown below.

![Microchip Technology](images/clean_and_build_icon.png)

5. Program your application to the device, by clicking on the **Make and Program** button as shown below.

![Microchip Technology](images/make_and_program.png)

The application should build and program successfully. A compilation error could occur if a pin name is undefined. For example: 
![Microchip Technology](images/deep-dive_undefined_pin.png) 

The demonstration will display the following UI:

![Microchip Technology](images/QSG%2060%20Seconds%20Final%20Display.png)

# Observations

You observed that the application displayed the home screen. You were able to change screens and control widgets.

# Review

You have successfully created an application using MPLAB Harmony v3 on Curiosity PIC32MZ EF 2.0. Your application used all the fundamental elements that go in building a graphics application. Your application successfully rendered a UI to the High-Performance 4.3" WQVGA Display Module. The application also took user from the display module.

In this application, you used MPLAB® Harmony Configurator (MHC) to configure Curiosity PIC32MZ EF 2.0. You used MHC to add and connect components. You used Pin Configurator to set up the pins for display and maXTouch controller.

# Summary

This guide provided you training of configuring and using all the fundamental components needed to build a graphics application on a Curiosity PIC32MZ EF 2.0 Development Board with MPLAB Harmony v3 Framework. As a next step, you may customize this application and reconfigure some of the components used in this tutorial. You could also add new components (PLIBs, etc.) to enhance this application to realize your end application.

Next Steps
* Learn how to add events to the project: [Adding Event to a Graphics Application ](https://github.com/Microchip-MPLAB-Harmony/gfx/wiki/Adding-Event-to-a-Graphics-Application)


***

**Is this page helpful**? Send [feedback](https://github.com/Microchip-MPLAB-Harmony/gfx/issues).