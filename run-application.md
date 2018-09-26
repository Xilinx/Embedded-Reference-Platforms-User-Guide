<p align="right">
            Read this page in other languages:<a href="../Japanese-master/run-application.md">日本語</a>    <table style="width:100%"><table style="width:100%">
  <tr>

<th width="100%" colspan="6"><img src="https://www.xilinx.com/content/dam/xilinx/imgs/press/media-kits/corporate/xilinx-logo.png" width="30%"/><h1>reVISION Getting Started Guide 2018.2</h1>
</th>

  </tr>
  <tr>
    <td width="17%" align="center"><a href="README.md">1. Introduction</a></td>
    <td width="16%" align="center"><a href="overview.md">2. Overview</a></td>
    <td width="17%" align="center"><a href="software-tools-system-requirements.md">3. Software Tools and System Requirements</a></td>
    <td width="17%" align="center"><a href="design-file-hierarchy.md">4. Design File Hierarchy</a></td>
</tr>
<tr>
    <td width="17%" align="center"><a href="operating-instructions.md">5. Installation and Operating Instructions</a></td>
    <td width="16%" align="center"><a href="tool-flow-tutorials.md">6. Tool Flow Tutorials</a></td>
    <td width="17%" align="center">7. Run the Application</td>
    <td width="17%" align="center"><a href="platform-details.md">8. Platform Details</a></td>    
  </tr>
<tr>
    <td width="17%" align="center" colspan="2"><a href="known-issues-limitations.md">9. Known Issues and Limitations</a></td>
    <td width="16%" align="center" colspan="2"><a href="additional-references.md">10. Additional References</a></td>
</tr>
</table>

# 7 Run the Application

To use the GStreamer plugins, a video pipeline that includes them must be set up and launched. The command line utility `gst-launch-1.0` may be used to do this. Use your laptop connected to the target board over a serial terminal emulator, interacting with the system via a standard Linux console session. See [section 6.1](tool-flow-tutorials.md#61-build-the-live_io-optical-flow-sample-application). You may construct video pipeline graphs consisting of one or more sources, zero, one or more accelerators, and one sink. GStreamer is responsible for initializing the capture, memory-to-memory, and display pipelines as well as managing the video buffer flow through the pipeline stages.

The gst-launch utility is really a debugging tool. The other way to set up and launch your plugins is with a compiled application that sets up and runs the pipeline using API calls to the GStreamer libraries. The sample code is provided for test apps that do this. See the `./gst/apps/<name> `folder for each of the live_IO samples.

The HDMI and MIPI input channels are themselves hardware pipelines that must be configured. This task is done by the `video_cmd` utility, run once before starting up a pipeline that uses that video input. The `video_cmd` utility is present on the sd_card directory. It is needed only when the MIPI or HDMI input channels are used.

## 7.1 Run the live_IO sample applications

* The "bottom" project containing the HW accelerated code is an SDx project, e.g. `./ws_f2d/filter2d`. When it completes, it creates an sd_card image with files you need to copy to your SD card you'll use on the target board.
* While copying the sd_card directory to the SD card please create two directories in SD card namely 'lib' and 'gstreamer-1.0'
* All the libraries should be copied to lib directory, sample plugin should be copied to gstreamer-1.0 and remaining images must be copied to the sd_card root directory.
* The following sections list the exact files for each case.
* For the stereo and triple case (because it includes stereo) you will also need the camera configuration file on the sd_card. (see below: [Particularities about the Stereo demo](#73-particularities-about-the-stereo-demo)).

**filter2d case**

After building the "bottom" library, your sd_card directory will contain these files:
* `./ws_f2d/filter2d/Release/sd_card/image.ub`
* `./ws_f2d/filter2d/Release/sd_card/BOOT.BIN`
* `./ws_f2d/filter2d/Release/sd_card/libfilter2d.so`
* `./ws_f2d/filter2d/Release/sd_card/video_cmd`

The "top" projects generate shared libraries and the demo app.
* `./ws_f2d/gst/plugins/filter2d/Debug/libgstsdxfilter2d.so`
* `./ws_f2d/gst/base/Debug/libgstsdxbase.so`
* `./ws_f2d/gst/allocators/Debug/libgstsdxallocator.so`
* `./ws_f2d/gst/apps/filter2d/Debug/gstdemo.`

>**:information_source: TIP**
> * Copy libfilter2d.so, libgstsdxbase.so and libgstsdxallocator.so in lib directory.
> * Copy libgstsdxfilter2d.so in gstreamer-1.0.
> * Rest all images copy directly in sdcard's root folder.

**opticalflow case**

After building the "bottom" library, your sd_card directory will contain these files:
* `./ws_of/opticalflow/Release/sd_card/image.ub`
* `./ws_of/opticalflow/Release/sd_card/BOOT.BIN`
* `./ws_of/opticalflow/Release/sd_card/libopticalflow.so`
* `./ws_of/opticalflow/Release/sd_card/video_cmd`

The "top" projects generate shared libraries and the demo app.
* `./ws_of/gst/plugins/optical_flow/Debug/libgstsdxopticalflow.so`
* `./ws_of/gst/base/Debug/libgstsdxbase.so`
* `./ws_of/gst/allocators/Debug/libgstsdxallocator.so`
* `./ws_of/gst/apps/optical_flow/Debug/gstdemo.`

>**:information_source: TIP**
> * Copy libopticalflow.so, libgstsdxbase.so and libgstsdxallocator.so in lib directory.
> * Copy libgstsdxopticalflow.so in gstreamer-1.0 directory.
> * Rest all images copy directly in sdcard's root folder.

**stereo case**

After building the "bottom" library, your sd_card directory will contain these files:
* `./ws_sv/stereo/Release/sd_card/image.ub`
* `./ws_sv/stereo/Release/sd_card/BOOT.BIN`
* `./ws_sv/stereo/Release/sd_card/libstereo.so`
* `./ws_sv/stereo/Release/sd_card/video_cmd`

The "top" projects generate shared libraries and the demo app.
* `./ws_sv/gst/plugins/stereo/Debug/libgstsdxstereo.so`
* `./ws_sv/gst/base/Debug/libgstsdxbase.so`
* `./ws_sv/gst/allocators/Debug/libgstsdxallocator.so`
* `./ws_sv/gst/apps/stereo/Debug/gstdemo.`

>**:information_source: TIP**
> * Copy libstereo.so, libgstsdxbase.so and libgstsdxallocator.so in lib directory.
> * Copy libgstsdxstereo.so in gstreamer-1.0 directory.
> * Rest all images copy directly in sdcard's root folder.

**triple case**

After building the "bottom" library, your sd_card directory will contain these files:
* `./ws_triple/triple/Release/sd_card/image.ub`
* `./ws_triple/triple/Release/sd_card/BOOT.BIN`
* `./ws_triple/triple/Release/sd_card/libtriple.so`
* `./ws_triple/triple/Release/sd_card/video_cmd`

The "top" projects generate shared libraries and the demo app.
* `./ws_triple/gst/plugins/filter2d/Debug/libgstsdxfilter2d.so`
* `./ws_triple/gst/plugins/optical_flow/Debug/libgstsdxopticalflow.so`
* `./ws_triple/gst/plugins/stereo/Debug/libgstsdxstereo.so`
* `./ws_triple/gst/base/Debug/libgstsdxbase.so`
* `./ws_triple/gst/allocators/Debug/libgstsdxallocator.so`
* `./ws_triple/gst/apps/triple/Debug/gstdemo.`

>**:information_source: TIP**
> * Create a lib directory in sdcard's root folder and copy libtriple.so, libgstsdxbase.so and libgstsdxallocator.so in lib directory.
> * Copy libgstsdxfilter2d.so, libgstsdxstereo.so and libgstsdxopticalflow.so in gstreamer-1.0 directory.
> * Rest all images copy directly in sdcard's root folder.


* Insert SD card in the SD card slot on your target board.
* Power on the board; make sure the large "INIT_B" LED and the "DONE" LED next to it go green after a few seconds.
* Control the system from your computer: start a terminal session using TeraTerm, PuTTY or the like. See [section 6.1](tool-flow-tutorials.md#61-build-the-live_io-optical-flow-sample-application). With the USB-UART cable connected and the board powered up, you can locate the COM port that is responsive. You'll see several pages of Linux bootstrap and debug messages scroll by, finishing at the linux command line prompt.
* cd over to directory `/media/card . ` This directory contains all the files you copied to your SD card.
```
# cd /media/card

```
* Copy the shared libraries where they need to go.
  * filter2d case:

	```
	# cp lib/libfilter2d.so /usr/lib
	# cp gstreamer-1.0/libgstsdxfilter2d.so /usr/lib/gstreamer-1.0
	# cp lib/libgstsdxbase.so /usr/lib/gstreamer-1.0
	# cp lib/libgstsdxallocator.so /usr/lib/gstreamer-1.0

	```
  * opticalflow case:

	```
	# cp lib/libopticalflow.so /usr/lib
	# cp gstreamer-1.0/libgstsdxopticalflow.so /usr/lib/gstreamer-1.0
	# cp lib/libgstsdxbase.so /usr/lib/gstreamer-1.0
	# cp lib/libgstsdxallocator.so /usr/lib/gstreamer-1.0

	```

  * stereo case:
	```

	# cp lib/libstereo.so /usr/lib
	# cp gstreamer-1.0/libgstsdxstereo.so /usr/lib/gstreamer-1.0
	# cp lib/libgstsdxbase.so /usr/lib/gstreamer-1.0
	# cp lib/libgstsdxallocator.so /usr/lib/gstreamer-1.0

	```

  * triple case:
	```

	# cp lib/libtriple.so /usr/lib
	# cp gstreamer-1.0/libgstsdxfilter2d.so /usr/lib/gstreamer-1.0
	# cp gstreamer-1.0/libgstsdxopticalflow.so /usr/lib/gstreamer-1.0
	# cp gstreamer-1.0/libgstsdxstereo.so /usr/lib/gstreamer-1.0
	# cp lib/libgstsdxbase.so /usr/lib/gstreamer-1.0
	# cp lib/libgstsdxallocator.so /usr/lib/gstreamer-1.0

	```


**Media pipeline initialization**

Use the `video_cmd` utility to list the available video sources and to configure the media pipeline. This needs to be done before running the gstreamer demo app or the `gst-launch` utility.
* To list all available video sources, their source IDs and corresponding video nodes:
```

# video_cmd -S
    VIDEO SOURCE        ID         VIDEO DEVNODE
    MIPI CSI2 Rx        0       /dev/video3
      HDMI Input        1       /dev/video2
      USB Webcam        2       /dev/video4
Virtual Video De        3       /dev/video0

```

>**:pushpin: NOTE**
> The output depends on the peripherals connected to the board and can be different in your case. The middle column shows the source ID which is needed for the next step to initialize the media pipeline (-s switch).

The MIPI, HDMI and vivid video sources support the YUY2 and UYVY pixel formats. For USB, the supported pixel format depends on the camera firmware e.g. the e-con USB camera only supports UYVY whereas the ZED stereo camera supports only YUYV (which is identical with YUY2). Make sure you set the input parameters correctly when configuring the media pipeline.

* Configure MIPI media pipeline for 1920x1080 resolution and YUY2 pixel format:
```

# video_cmd -s 0 -i 1920x1080@YUY2 -X

```

  * `-s 0` is the input source ID, in this case MIPI CSI
  * `-i 1920x1080@YUY2` means the MIPI source will be set up for 1080p resolution and YUY2 format
  * `-X` causes `video_cmd` to exit immediately after setting up MIPI.
  * returns video node that corresponds to the input ID selected by -s. The video node needs to be passed to the v4lsrc plugin via the device property

* Configure HDMI media pipeline for 1920x1080 resolution and UYVY pixel format:
```

# video_cmd -s 1 -i 1920x1080@UYVY -X

```

  * `-s 1` is the input source ID, in this case is HDMI
  * `-i 1920x1080@UYVY` means the MIPI source will be set up for 1080p resolution and UVYV fomat
  * `-X` causes `video_cmd` to exit immediately after setting up HDMI.
  * returns video node that corresponds to the input ID selected by -s. The video node needs to be passed to the v4lsrc plugin via the device property

**Display controller initialization**

Use the `video_cmd` utility to initialize the display controller. The command should be run in the background as the display mode will otherwise be reset to its original value after `video_cmd` exits. This needs to be done before running the gstreamer demo app or the `gst-launch` utility.

* Configure DP display controller
```

# video_cmd -d 0 &

```

  * `-d 0` is the display ID for DP

* Configure HDMI display controller
```

# video_cmd -d 1 &

```

  * `-d 1` is the display ID for HDMI

**Gstreamer application**

To create and run the gstreamer pipeline, you can either use the gst demo applications that are compiled from source or you can use the prebuilt `gst-launch` utility.

* Use your compiled demo program:
```

# ./gstdemo

```

  * All the demo programs use HDMI output, via the mixer.
  * The filter2d demo uses HDMI input.
  * The opticalflow demo uses the MIPI input
  * The stereo demo used the USB "ZED" stereo camera input
  * The triple demo uses all of the above

* Here is a gst-launch command to run the filter2d pipeline, from MIPI, 1920x1080, YUY2, to HDMI output via mixer plane 29.
```

gst-launch-1.0 \
    v4l2src device=/dev/video3 io-mode=dmabuf ! \
    "video/x-raw, width=1920, height=1080, format=YUY2" ! \
    sdxfilter2d filter-preset=4 filter-mode=1 ! queue ! \
    kmssink bus-id=b00c0000.v_mix plane-id=29 sync=false fullscreen-overlay=true

```


* Here is a gst-launch command to run the opticalflow pipeline, from HDMI, 1920x1080, YUY2, to HDMI output via mixer plane 29.
```

gst-launch-1.0 \
    v4l2src device=/dev/video2 io-mode=dmabuf ! \
    "video/x-raw, width=1920, height=1080, format=YUY2" ! \
    sdxopticalflow filter-mode=1 ! queue ! \
    kmssink bus-id=b00c0000.v_mix plane-id=29 sync=false fullscreen-overlay=true

```


* Here is a gst-launch command to run the stereo pipeline, from USB, 3840x1080 side-by-side input, YUY2, 1920x1080 output to HDMI via mixer plane 29. You must substitute your camera serial number for the config-filename property. See section below on "**[Particuliarities about the Stereo Demo](#73-particularities-about-the-stereo-demo)**".
```

gst-launch-1.0 \
    v4l2src device=/dev/video4 io-mode=dmabuf ! \
    "video/x-raw, width=3840, height=1080, format=YUY2" ! \
    sdxstereo filter-mode=1 config-filename=/media/card/SN12263.conf ! queue ! \
    kmssink bus-id=b00c0000.v_mix plane-id=29 sync=false fullscreen-overlay=true

```


* Here is an alternate way of running filter2d, with frames-per-second display enabled. Notice the output pipe stage is 'fpsdisplaysink' and that the 'kmssink...." string we used before is a property of fpsdisplaysink called 'video-sink'.
```

gst-launch-1.0 \
    v4l2src device=/dev/video3 io-mode=dmabuf ! \
    "video/x-raw, width=1920, height=1080, format=YUY2" ! \
    sdxfilter2d filter-preset=4 filter-mode=1 ! queue ! \
    fpsdisplaysink video-sink="kmssink bus-id=b00c0000.v_mix plane-id=29 fullscreen-overlay=true" sync=false text-overlay=false -v

```


## 7.2 Gstreamer elements

These pipelines are using the elements **v4l2src**, **sdxfilter2d** (or **sdxopticalflow**, or **sdxstereo**), **queue**, and **kmssink**. You may display properties and other info about any of these elements using the gstreamer utility gst-inspect-1.0.

**v4l2src**

```

# gst-inspect-1.0 v4l2src

```

* You will see a lot of information. Of interest to us here is the v4l2src "device" property that is set in each of the above commands to select the video source
  * /dev/video2 is HDMI
  * /dev/video3 is MIPI
  * /dev/video4 is US
* The io-mode property
  * 4 is "dmabuf" - it means that we will not have to copy images in between pipe stages - the frames are passed by reference.

* Following the first '!' character is an expression "video/x-raw, ....". This is a "capabilities filter" that informs the v4l2src element which of the many formats it supports are suitable for the downstream pipe element. Specifically:
  * "raw" video (uncompressed)
  * width and height
  * pixel format - YUY2 is 16 bit per pixel 4:2:2 with 'Y' on the LOW byte of each word. UYVY is also 16 bit 4:2:2, with 'Y' on the HIGH byte of each word.

**queue**

This is not strictly necessary, but using it will give better performance - i.e. the highest possible frame rate.

**kmssink**

To inspect the kmssink plugin:
```

# gst-inspect-1.0 kmssink

```

* property 'bus-id'
  * 'b00c0000.v_mix' means HDMI output (via the video mixer)
  * 'fd4a0000.zynqmp-display' means DP output
* property 'plane-id'
  * if you are using b00c0000.v_mix (HDMI output)
       * '29' is a YUY2 plane
       * '30' is a YUY2 plane
       * '31' is a UYUV plane
  * if you are using fd4a0000.zynqmp-display (DP output)
       * '35' supports a number of RGB
       * '34' supports YUY2 and UYVY

**sdx&lt;accelerator&gt;**

To inspect the sdxfilter2d plugin:
```

# gst-inspect-1.0 sdxfilter2d

```

* property 'filter_mode'
  * 1: use HW acceleration
  * 0: use SW (the filter2d code executes entirely on the ARM processor)
* property 'filter_preset'
  * 1 - 10 select a number of preset filters. The example uses '4' which is the 'emboss' or edge enhancement filter.
* property 'coefficients'
  * Array with a 3x3 coefficients matrix e.g. `coefficients="<<0,0,0>,<0,-1,0>,<0,0,0>>"`

To inspect the sdxopticalflow plugin:
```

# gst-inspect-1.0 sdxopticalflow

```

* property 'filter_mode'
  * 1: use HW acceleration
  * 0: use SW (the optical flow code executes entirely on the ARM processor)

To inspect the sdxstereo plugin:
```

# gst-inspect-1.0 sdxstereo

```

* property 'filter_mode'
  * 1: use HW acceleration
  * 0: use SW (the optical flow code executes entirely on the ARM processor)
* property 'config-filename'
  * This is how you specify the ZED camera configuration file, which must be present on the SD card. See section 7.3 below.

## 7.3 Particularities about the Stereo demo

The stereo vision demo is special in several ways. First, you MUST use the ZED stereo camera connected to the USB video input. Second, and particular to this app, the width of the input image resolution is twice the width of the output resolution. The input consists of two images side-by-side, the synchronized left and right stereo input supplied by the camera. Two cases are possible: 2560x720 in to 1280x720 out, and 3840x1080 in to 1920x1080 out. The default 3840x2160 output resolution is not supported by the Stereo Vision app.

The other special thing about this app is that a configuration file must be used that corresponds to the camera you have connected to your system . Each StereoLabs ZED camera has a unique parameters file associated with it. This text file comes from StereoLabs, and must be present on the SD Card for the Stereo Vision demo to work properly. You need the file unique to your camera, identified by its Serial Number (found on the ZED camera box and also on a black tag near the USB plug of the ZED camera itself). This number will be, e.g., S/N 000012345. The parameter file for that camera would be named SN12345.conf. To download your parameter file, enter this URL into your browser:
http://calib.stereolabs.com/?SN=12345 (using your serial number in place of 12345)
This will download your configuration file to your computer.

The stereo block-matching algorithm calculates depth based on binocular parallax, similar to the way human eyes perceive depth. The depth map is coded in false colors. Objects far away appear deep blue. Closer and closer objects appear in rainbow succession green, yellow, orange, red, purple and finally white at about two feet from the camera in the 720p case, and about five feet away in the 1080p case. Any object closer than that cannot be tracked, and smooth areas with no texture in the image cannot be tracked, and show up as black. Areas with a lot of detail (especially with lots of vertical edges) are tracked best. It is normal that a large area on the left is black - this is 128 pixels wide, representing the range of the horizontal search for best match between the right and left binocular images.



<hr/>

:arrow_forward:**Next Topic:**  [8. Platform Details](platform-details.md)

:arrow_backward:**Previous Topic:**  [6. Tool Flow Tutorials](tool-flow-tutorials.md)
<hr/>
<p align="center"><sup>Copyright&copy; 2018 Xilinx</sup></p>
