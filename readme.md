#OpenCV 3 for Xojo 64-bit
This **an experimental attempt** to use OpenCV C API on 64-bit processors. **Without warranties. Use at your own risk.**
The code was tested with Xojo version 2022, release 1.1 on Apple Silicon M1 (ARM-64) processor, but should work fine on x86-64 Intel processor.

Code is opensource.

##Required Install

First, you need a version of OpenCV >= 3.0 and < 4.0. You'll find the sources here [OpenCV Releases](https://opencv.org/releases/). OpenCV realeases > 3.17 **have removed the C API** and replaced the API by C++ code. 

Once downloaded, you need to compile OpenCV sources with [CMake](https://cmake.org) in order to get 64-bit librairies. After compilation, copy the compiled libs somewhere on your computer such as `/usr/local/lib/opencv3/`. 

And naturally [Xojo](https://www.xojo.com) is required.

##OpenCVX64 module

This code includes several modules that give access to about 600 OpenCV functions for image processing. See [OpenCV documentation](https://docs.opencv.org/3.4.16/d2/df8/group__core__c.html) for detail. 

* calib3D
* core
* highgui
* imgcodecs
* immgproc
* objdetect
* photo
* videoio
* video
* xTools

Each module contains different structures, constants, and external methods for accessing C-API functions. Inside each module there is a constant (e.g. core, immproc, highgui..) which is linked to OpenCV libraries, such as for MacOS: `/usr/local/lib/opencv3/libopencv_core.3.4.16.dylib`. This is important and you have to modify the links according to your OS. 
**xTools** is specific to Xojo and includes for getting matrices and images values There also two methods for converting OpneCV images to Xojo images.

##Using OpenCVX64 module

Very easy. Just open OpenCVX64 module with Xojo IDE. Then drag or copy the module to any application requiring OpenCV image processing. According to your needs you can delete non-used modules, but **core and xTools modules are mandatory**. 


##OpenCVX64 module development

Porting [orginal 32-bit code](https://github.com/ldci/OpenCV-Xojo) was not easy. Just linking to 64-bit libraries was not enough. The first problem was related to the use of Integer data type equivalent to **Int32** on 32-bit apps or **Int64** on 64-bit apps. In fact *OpenCV C-API is only 32-bit*. So now, all variables or returned values are Int32. The second difficulty is related to the pointer data type size: A Ptr is 4 bytes for 32-bit apps and 8 bytes for 64-bit apps. Consequently, many structures that use Ptr have modified sizes and xTools functions are corrected in order to get the correct returned values. Lastly, the original code written in 2016 was adapted to Xojo 2016 version. Many methods I used in 2016 are now obsolete. For example, MemoryBlock class is different.

**This means that many of the methods that use pointers and MemoryBlocks need to be thoroughly reviewed. Not being a Xojo language expert, it would be great if Xojo specialists would look at and improve this first version.**

##OpenCVX64 examples

The examples included are minimalist, but show that it can work. All examples were written on a Silicon Mac M1 for an ARM-64 bit architecture. To be tested for Intel X86 64-bit processors. 

