# ![Microchip Technology](images/mhgs.png) Driver Development Process

A collection of driver development tutorials are provided with MPLAB Harmony Graphics
Suite to help users develop graphics drivers using the MPLAB Harmony Graphics Suite
development process. This support includes: display and touch driver development
support using MPLAB Harmony Configurator (MHC) display and touch configurable components.

## Display Driver Components

* LE GLCD Controller Component
* LE ILI9488 Controller Component
* LE LCC Controller Component
* LE SSD1936 Controller Component
* LE External Controller Component

The LE drivers for GLCD and LCC are integrated, pre-coded and only require configuration using their respective components.  The LE External Controller is a generic component capable of creating a SSD1963 or ILI9488 display driver or a driver from a similar class of display controller. The user of the LE External Controller component use configuration options to create the necessary initialization, blitting, and backlight routines.

## Touch Driver Components

* maXTouch Controller Component
* Generic Touch Component
* Peripheral Touch Component

The drivers for maXTouch and peripheral touch are integrated, pre-coded and only require configuration using their respective components. The Generic Touch Component is capable of creating a display driver or a driver from a similar class of touch controller. The user of the Generic Touch component use configuration options to create the necessary initialization and event routines.

A basic understanding of these components are helpful when creating drivers for
other display and touch drivers.

# Basic Driver Development Support

* [Display Driver Support](Display-Driver-Support)
* [Touch Driver Support](Touch-Driver-Support)

***

If you are new to MPLAB Harmony, you should probably start with these tutorials:

* [MPLAB® Harmony v3 software framework](https://microchipdeveloper.com/harmony3:start)
* [MPLAB® Harmony v3 Configurator Overview](https://microchipdeveloper.com/harmony3:mhc-overview)
* [Create a New MPLAB® Harmony v3 Project](https://microchipdeveloper.com/harmony3:new-proj)

***

**Is this page helpful**? Send [feedback](issues).

### Next Steps

* Learn about our graphics [quickstart guides](Application-QuickStart)
