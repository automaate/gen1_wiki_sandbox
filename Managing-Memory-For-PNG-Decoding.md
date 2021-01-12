# ![Microchip Technology](images/mhgs.png) Managing Memory for PNG Decoding

PNG should only be used in applications that fits the following criteria:

1.	Color space RGBA8888.
2.	Requires transparency for revealing details underneath the image.

Runtime PNG decoding is memory intensive.  It is recommended for MCUs/MPUs with megabytes of volatile memory available.

This memory is larger than the largest micro buffer in the Fixed Pool.  The Legato memory allocator will draw from the Variable Heap during runtime.  

During runtime, if the Legato Graphics Library fails to allocate memory for the PNG decoder, the PNG decoding operation would be halt.  It will proceed to render the remainder of the UI design without the PNG image.

The memory requirement can vary depending on resolution of the image.  For example, to decode a 40x40 32-bit RGBA PNG image, requires upwards of 26 kilobytes set in Variable Heap.  A 480x320 32-bit RGBA PNG image requires 1 megabyte of Variable Heap memory.

Here are some conditions to consider:

1.	The runtime PNG decoder allocates multiple sample buffers for each image.  These buffers must be drawn from the Variable Heap.  They are allocated and freed during the decoding operation.
2.	Depending on how these buffers fit in the Variable Heap, the Variable Heap can become fragmented.
3.	Memory allocation can fail if the Variable Heap memory becomes overly fragmented.
To reduce the risk of memory fragmentation it is important to set Best Fit mode for the Variable Heap. Budgeting a surplus in the Variable Heap memory settings will help as well.
The amount needed is not straightforward to determine and may require some trial and error.

***

If you are new to MPLAB Harmony, you should probably start with these tutorials:

* [MPLAB® Harmony v3 software framework](https://microchipdeveloper.com/harmony3:start) 
* [MPLAB® Harmony v3 Configurator Overview](https://microchipdeveloper.com/harmony3:mhc-overview)
* [Create a New MPLAB® Harmony v3 Project](https://microchipdeveloper.com/harmony3:new-proj)

***

**Is this page helpful**? Send [feedback](https://github.com/Microchip-MPLAB-Harmony/gfx/issues).