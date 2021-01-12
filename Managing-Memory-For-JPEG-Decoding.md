# ![Microchip Technology](images/mhgs.png) Managing Memory for JPEG Decoding

## Managing Memory for JPEG Decoding

The runtime JPEG decoder utilizes a single 16 x 16, 24-bit RGB888 (768 bytes) sample buffer to decode an image, regardless of the resolution of the full image.  This memory is larger than the largest micro buffer in the Fixed Pool.  The Legato memory allocator will draw from the Variable Heap during runtime.

If JPEG decoding is required, make sure the Variable Heap has at least this amount of memory configured.

During runtime, if the Legato Graphics Library fails to allocate memory for the JPEG decoder, the JPEG decoding operation would be halt.  It will proceed to render the remainder of the UI design without the JPEG image.

***

If you are new to MPLAB Harmony, you should probably start with these tutorials:

* [MPLAB® Harmony v3 software framework](https://microchipdeveloper.com/harmony3:start) 
* [MPLAB® Harmony v3 Configurator Overview](https://microchipdeveloper.com/harmony3:mhc-overview)
* [Create a New MPLAB® Harmony v3 Project](https://microchipdeveloper.com/harmony3:new-proj)

***

**Is this page helpful**? Send [feedback](https://github.com/Microchip-MPLAB-Harmony/gfx/issues).