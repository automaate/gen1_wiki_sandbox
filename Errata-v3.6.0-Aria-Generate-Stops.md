# ![Microchip Technology](images/mhgs.png) Aria application does not generate. Stops at 99%

## Issue

There is a known issue when using MHC v3.4.0 to generate code for Aria applications. Users may experience that the percentage indicator on the progress bar reaches 99% but not continue.

***

## Resolution

This post is provided to offer two options to resolve this issue.

**Option 1**:  Use MHC v3.4.0 and replace graphics jar files.

Replace the attached .jar files in following locations, relaunch MHC and regenerate?


1. Download [plugins.jar](https://www.microchip.com/forums/download.axd?file=0;1141825).
2. Replace gfx\middleware\aria\library\plugins\libaria.jar.
3. Replace gfx\middleware\aria\library\plugins\lib\gac.jar.
4. Replace gfx\middleware\aria\hal\plugins\displaymanager.jar.
5. Exit and relaunch MHC.
6. Regenerate code.


**Option 2**. Use MHC v3.3.5 by reverting back to previous MHC release.

Use the Harmony content manager to downgrade the MHC release v3.4.0 to previous release v.3.3.5. See: [Content manager](https://github.com/Microchip-MPLAB-Harmony/contentmanager/wiki)
for content manager tutorial.

1. Navigate to MHC and select v3.3.5 from selection dropdown.
2. Install MHC.
3. Exit and relaunch MHC.
4. Regenerate code.

***

A fix for this issue will be addressed in the next release using ticket MH3-36566.


***

For additional assistance, please reference: http://github.com/Microchip-MPLAB-Harmony/mhc/issues/14