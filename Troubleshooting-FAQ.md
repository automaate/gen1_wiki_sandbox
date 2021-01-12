# ![Microchip Technology](images/mhgs.png) Troubleshooting FAQ

A collection of MPLAB® Harmony Graphics Suite Frequently Asked Questions (FAQs) and answers are provided for additional support on application development.

You may encounter an issue in the course of using MPLAB Harmony Graphics Suite. Many issues are resolved once you become more familiar on how MPLAB Harmony Graphics Suite works, while others might require you to dig deeper into the suite.

The following list has been compiled over the course of years of MPLAB Harmony Graphics Suite usage. 

If you can't find a reference to the problem you're having here, it may be covered in a [post-release errata](Issues-and-Errata), in a [reported github issue](https://github.com/Microchip-MPLAB-Harmony/gfx/issues) or in the [MPLAB Harmony Forum](https://www.microchip.com/forums/f291.aspx).

In addition to this section, specific platform FAQs are available at [MPLAB Harmony v3](https://microchipdeveloper.com/harmony3:start).

## Graphics FAQs
<details><summary>How to Migrate Resistive Touch to Harmony v2.06? </summary>
<p>

The following link provides helpful customer dialog concerning Resistive Touch.

https://www.microchip.com/forums/m1069348.aspx

If this is not helpful, [Send Feedback](https://github.com/automaate/GFX_sandbox/issues).

</p>
</details>

<details><summary>How to set laListWidget Scroll Bar Size? </summary>
<p>

https://www.microchip.com/forums/m1097504.aspx

If this is not helpful, [Send Feedback](https://github.com/automaate/GFX_sandbox/issues).

</p>
</details>

<details><summary>Can I use Focaltech FT53x6 Series Capacitive Touch? </summary>
<p>

https://www.microchip.com/forums/m1035459.aspx

If this is not helpful, [Send Feedback](https://github.com/automaate/GFX_sandbox/issues).

</p>
</details>

<details><summary>Does PIC32MZ EF support WVGA 800x480 resolution? </summary>
<p>

https://www.microchip.com/forums/m1098138.aspx

</p>
</details>

<details><summary>Why is there no graphic display on MEB-II board using PIC32MZ DA?</summary>
<p>
It is possible the display black light is not enabled (whether the driver setting or the actual pin is not hooked up).  If that is the case, the frame buffer data may be getting to the display and just not easily visible because the backlight is off.

See: [QuickStart on Multimedia Expansion Board II with PIC32MZ DA](QuickStart-on-Multimedia-Expansion-Board-II-with-PIC32MZ-DA-WQVGA) for hardware configuration and pin settings.

</p>
</details>

<details><summary>Why is the display distorted on MEB-II board using PIC32MZ DA?</summary>
<p>
Verify that SYSCLK, REFCLK5, and MPLL are set appropriately for your design. For an example of default settings, see: [QuickStart on Multimedia Expansion Board II with PIC32MZ DA](QuickStart-on-Multimedia-Expansion-Board-II-with-PIC32MZ-DA-WQVGA).

If these settings are not working your your device, [Send Feedback](https://github.com/automaate/GFX_sandbox/issues).
</p>
</details>

<details><summary>Why is my screen freezing and then fading? laWidget_SetScheme</summary>
<p>

If your screen display freezes or seems to fade away it may be a result of a memory leak during screen transitions.

If trying to initiate screen change and scheme change from application code.  Every time the application requests some changes to the screen be it a screen change or scheme change, the requests get put in a draw queue for the library to process.  The draw queue uses dynamically allocated memory from the heap to perform.

Since the actual drawing of the pixels on screen takes the library some time, if the change events are fired at a high enough frequency, the draw queue backlog grows and eventually all the heap memory can be used up or become too fragmented.  This is probably what is causing the crash.

The reason laWidget_SetScheme causes this and laContext_SetActiveScreen does not is because laWidget_SetScheme asks the library to apply draw change to the widget and all of its child widget, which can be a large queue while SetActiveScheme is a single item.

There are two ways to solve this:

1) Use the best practice of using laContext_IsDrawing in DISPLAY_Tasks to safe guard every SetActiveScreen and SetScheme calls.  This way the application is not overwhelming the graphics library.

2) Increase the heap size to mitigate against crash from over usage and memory fragmentation.

If this is not helpful, [Send Feedback](https://github.com/automaate/GFX_sandbox/issues).

</p>
</details>

***

If you are new to MPLAB Harmony, you should probably start with these tutorials:

* [MPLAB® Harmony v3 software framework](https://microchipdeveloper.com/harmony3:start) 
* [MPLAB® Harmony v3 Configurator Overview](https://microchipdeveloper.com/harmony3:mhc-overview)
* [Create a New MPLAB® Harmony v3 Project](https://microchipdeveloper.com/harmony3:new-proj)

***

**Is this page helpful**? Send [feedback](https://github.com/automaate/GFX_sandbox/issues).