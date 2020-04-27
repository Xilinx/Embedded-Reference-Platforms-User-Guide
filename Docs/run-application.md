<p align="right">
            Read this page in other languages:<a href="../docs-jp/Docs/run-application.md">日本語</a>    <table style="width:100%"><table style="width:100%">
  <tr>

<th width="100%" colspan="6"><img src="https://www.xilinx.com/content/dam/xilinx/imgs/press/media-kits/corporate/xilinx-logo.png" width="30%"/><h1>Vitis Software Platform: Embedded Vision Reference Platforms User Guide 2019.2 (UG1265)</h1>
</th>

  </tr>
  <tr>
    <td width="17%" align="center"><a href="../README.md">1. Introduction</a></td>
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

# 7. Run the Application

To use the GStreamer plugins, a video pipeline that includes them must be set up and launched. The command line utility `gst-launch-1.0` can be used to do this. Use your laptop connected to the target board over a serial terminal emulator, interacting with the system using a standard Linux console session  (see [Build the Live I/O Optical Flow Sample Application](tool-flow-tutorials.md#611-build-the-live_io-optical-flow-sample-application)). You can construct video pipeline graphs consisting of one or more sources, zero, one or more accelerators, and one sink. GStreamer is responsible for initializing the capture, memory-to-memory, and display pipelines as well as managing the video buffer flow through the pipeline stages.

The ``gst-launch`` utility is really a debugging tool. The other way to set up and launch your plugins is with a compiled application that sets up and runs the pipeline using API calls to the GStreamer libraries. The sample code is provided for test apps that do this. See the `./gst/apps/<name> `folder in the Single Sensor SDSoC platform for each of the live I/O samples.


## 7.1. Run the Live I/O Sample Applications (Single Sensor Platform)

<details>
<br>
	
The bottom project containing the hardware accelerated code is an SDx™ environment project (for example, `./ws_f2d/filter2d`). When it completes, it creates an SD card image with files you need to copy to the SD card you'll use on the target board. All the libraries and plugins must be copied to the ``sd_card`` root directory. The following sections list the exact files for each case.



:pushpin: **IMPORTANT**: For the stereo case, you also need the camera configuration file on the SD card (see [Single Sensor Platform Stereo Demo: Special Considerations](#76-single-sensor-platform-stereo-demo-special-considerations)).

### 7.1.1. Files for filter2d

After building the bottom library, your ``sd_card`` directory will contain the following files:
* `./ws_f2d/filter2d/Release/sd_card/image.ub`
* `./ws_f2d/filter2d/Release/sd_card/BOOT.BIN`
* `./ws_f2d/filter2d/Release/sd_card/libfilter2d.so`

The top projects generate the shared library and the demo app.
* `./ws_f2d/gst/plugins/filter2d/Debug/libgstsdxfilter2d.so`
* `./ws_f2d/gst/apps/filter2d/Debug/gstdemo.`

>**:information_source: TIP** Copy all images  directly into the root folder of the SD card.

### 7.1.2. Files for opticalflow

After building the bottom library, your ``sd_card`` directory will contain the following files:
* `./ws_of/opticalflow/Release/sd_card/image.ub`
* `./ws_of/opticalflow/Release/sd_card/BOOT.BIN`
* `./ws_of/opticalflow/Release/sd_card/libopticalflow.so`

The top projects generate the shared library and the demo app.
* `./ws_of/gst/plugins/optical_flow/Debug/libgstsdxopticalflow.so`
* `./ws_of/gst/apps/optical_flow/Debug/gstdemo.`

>**:information_source: TIP** Copy all images  directly into the root folder of the SD card.

### 7.1.3. Files for stereo

After building the bottom library, your ``sd_card`` directory will contain the following files:
* `./ws_sv/stereo/Release/sd_card/image.ub`
* `./ws_sv/stereo/Release/sd_card/BOOT.BIN`
* `./ws_sv/stereo/Release/sd_card/libstereo.so`

The top projects generate the shared library and the demo app.
* `./ws_sv/gst/plugins/stereo/Debug/libgstsdxstereo.so`
* `./ws_sv/gst/apps/stereo/Debug/gstdemo.`

>**:information_source: TIP** Copy all images  directly into the root folder of the SD card.

### 7.1.4. Instructions

1. Insert the SD card in the SD card slot on your target board.
2. Power on the board; make sure the large INIT_B LED and the DONE LED next to it go green after a few seconds.
3. Control the system from your computer: start a terminal session using TeraTerm, PuTTY or similar (see [Build the Live I/O Optical Flow Sample Application](tool-flow-tutorials.md#611-build-the-live_io-optical-flow-sample-application)). With the USB-UART cable connected and the board powered up, you can locate the COM port that is responsive. You'll see several pages of Linux bootstrap and debug messages scroll by, finishing at the Linux command line prompt.
4. Using ``cd``, go to the `/media/card` directory. This directory contains all the files you copied to your SD card.
```
# cd /media/card

```
5. Copy the shared libraries where they need to go; see the examples for each case below.

**:pushpin: NOTE:** The following steps are not required if you are using pre-built SD card binaries, because the ``PATH`` environment variable is appended to ``/media/card/``.

  * filter2d case:

	```
	# cp libfilter2d.so /usr/lib
	# cp libgstsdxfilter2d.so /usr/lib/gstreamer-1.0

	```
  * opticalflow case:

	```
	# cp libopticalflow.so /usr/lib
	# cp libgstsdxopticalflow.so /usr/lib/gstreamer-1.0

	```

  * stereo case:
	```

	# cp libstereo.so /usr/lib
	# cp libgstsdxstereo.so /usr/lib/gstreamer-1.0

	```

### 7.1.5 GStreamer Application

To create and run the GStreamer pipeline, you can either use the ``gst`` demo applications that are compiled from source, or you can use the prebuilt `gst-launch` utility. Use your compiled demo program:
```

# ./gstdemo

```

  * All the demo programs use the HDMI output, through the mixer.
  * The filter2d demo uses the HDMI input.
  * The opticalflow demo uses the MIPI input.
  * The stereo demo uses the USB ZED stereo camera input.

The following code example is a ``gst-launch`` command to run the ``filter2d`` pipeline, from MIPI, 1920x1080, YUY2, to the HDMI output through mixer plane 29.
```

gst-launch-1.0 \
    xlnxvideosrc  io-mode=3 src-type="mipi" ! \
    "video/x-raw, width=1920, height=1080, format=YUY2" ! \
    sdxfilter2d filter-preset=4 filter-mode=1 ! queue ! \
    xlnxvideosink sink-type="hdmi" plane-id=29 sync=false fullscreen-overlay=true

```

The following code example is a ``gst-launch`` command to run the ``opticalflow`` pipeline, from HDMI, 1920x1080, YUY2, to the HDMI output through mixer plane 29.
```

gst-launch-1.0 \
    xlnxvideosrc io-mode=3 src-type="hdmi" ! \
    "video/x-raw, width=1920, height=1080, format=YUY2" ! \
    sdxopticalflow filter-mode=1 ! queue ! \
    xlnxvideosink sink-type="hdmi" sync=false fullscreen-overlay=true

```


The following code example is a ``gst-launch`` command to run the stereo pipeline, from USB, 3840x1080 side-by-side input, YUY2, 1920x1080 output to HDMI through mixer plane 29. You must substitute your camera serial number for the ``config-filename`` property. See the section below on [Single Sensor Platform Stereo Demo: Special Considerations](#76-single-sensor-platform-stereo-demo-special-considerations).
```

gst-launch-1.0 \
    xlnxvideosrc io-mode=3 src-type="usbcam"  ! \
    "video/x-raw, width=3840, height=1080, format=YUY2" ! \
    sdxstereo filter-mode=1 config-filename=/media/card/SN12263.conf ! queue ! \
    xlnxvideosink sink-type="hdmi" plane-id=29 sync=false fullscreen-overlay=true

```


The following example shows an alternative way to run ``filter2d`` with frames-per-second display enabled. Notice the output pipe stage is ``fpsdisplaysink``, and that the previously used ``xlnxvideosink....`` string is a property of ``fpsdisplaysink`` called ``video-sink``.
```

gst-launch-1.0 \
    xlnxvideosrc io-mode=3 src-type="mipi" ! \
    "video/x-raw, width=1920, height=1080, format=YUY2" ! \
    sdxfilter2d filter-preset=4 filter-mode=1 ! queue ! \
    fpsdisplaysink video-sink="xlnxvideosink sink-type=hdmi plane-id=29 fullscreen-overlay=true" sync=false text-overlay=false -v

```
You can also refer to the ``gst`` scripts provided as part of `./workspaces/ws_f2d/scripts` or `./workspaces/ws_of/scripts` or `./workspaces/ws_sv/scripts`. In case of any issue with running the application, make sure the `plane-id` is given correctly.

The following example shows an example ``gst`` command to run the See3CAM USB 3.0 camera. Unlike the other MIPI camera or HDMI sources, this camera supports a different color format (UYVY). Get the ``plane-id`` of the ``kmssink`` for UYVY format using the command `modetest -D b00c0000.v_mix`.

```
gst-launch-1.0 \
    xlnxvideosrc src-type="usbcam"  ! \
    "video/x-raw, width=1920, height=1080, format=UYVY" ! \
    xlnxvideosink sink-type="hdmi" plane-id=32 sync=false fullscreen-overlay=true

```
</details>

## 7.2. Run the RTSP (Real Time Streaming Protocol) Sample Application (8-Stream VCU + CNN Platform)
<details>
<br>
	
The C-callable project containing the hardware accelerated code is a Vitis™ environment project (for example, `./<DPU_workspace>/binary_container_1/sd_card`). When it completes, it creates an SD card image with files you need to copy to the SD card you'll use on the target board. All the libraries and plugins must be copied to the SD card root directory. The following sections list the exact files for each case.

### 7.2.1. Files for RTSP application (Traffic and Face Detect)

After building the C-callable library, your ``sd_card`` directory will contain the following files:
* `./<DPU_workspace>/binary_container_1/sd_card/image.ub`
* `./<DPU_workspace>/binary_container_1/sd_card/BOOT.BIN`
* `./<DPU_workspace>/binary_container_1/sd_card/dpu.xclbin`

The ``gstsdxtrafficdetect`` and ``gstsdxfacedetect`` projects generate the shared libraries and copy them to the SD card.

* `./workspaces/gstsdxtrafficdetect/Debug/libgstsdxtrafficdetect.so`
* `./workspaces/gstsdxtrafficdetect/Debug/libgstsdxtrafficdetect.so`

The ``gstsdxbase``, ``gstxclallocator``, and ``xrtutils`` projects generate the shared libraries and copy them to the SD card.

* `workspaces/sdcard/libgstxclallocator.so`
* `workspaces/sdcard/libgstsdxbase.so`
* `workspaces/sdcard/libxrtutils.so`

The ``rtsp`` application project generates the executable application and copy it to the SD card.

Copy the following pre-built libraries to the SD card:

* `workspaces/sdcard/libn2cube.so`
* `workspaces/sdcard/libdputils.so`
* `workspaces/sdcard/libdpumodeldensebox.so`
* `workspaces/sdcard/libdpumodelssd.so`

Copy the following scripts and test video inputs to the SD card:
The required examples scripts to run the demo are present in `sdcard` folder of the package. Update the inputs.conf file to have the correct RTSP URLs preapred in server side. These URLs should have the same IP address that is being set on server side as explained in the `Installation and Operating Instructions` section.

* `workspaces/sdcard/setup.sh`
* `workspaces/sdcard/inputs.conf`
* `workspaces/sdcard/*.sh`
* `workspaces/sdcard/demo_inputs`
* `workspaces/sdcard/test_videos`

>**:information_source: TIP** Copy all images  directly into the root folder of the SD card.

### 7.2.2. Instructions

1. Insert the SD card into the SD card slot on your target board.

2. Power on the board; make sure the large INIT_B LED and the DONE LED next to it go green after a few seconds.
3. Control the system from your computer: start a terminal session using TeraTerm, PuTTY or similar (see [Build the Live I/O Optical Flow Sample Application](tool-flow-tutorials.md#611-build-the-live_io-optical-flow-sample-application)). With the USB-UART cable connected and the board powered up, you can locate the COM port that is responsive. You'll see several pages of Linux bootstrap and debug messages scroll by, finishing at the Linux command line prompt.

4. Using ``cd``, go to the `/media/card` directory. This directory contains all the files you copied to your SD card.
```
# cd /media/card

```
5. Copy the shared libraries where they need to go.

**:pushpin: NOTE:** The following steps are not required if you are using pre-built SD card binaries, because the ``PATH`` environment variable is appended to ``/media/card/``.

>
```
# cp libn2cube.so /usr/lib
# cp libdpuaol.so /usr/lib
# cp libhineon.so /usr/lib
# cp libdpumodelssd.so /usr/lib
# cp libdpumodeldensebox.so /usr/lib
# cp libgstsdxtrafficdetect.so /usr/lib/gstreamer-1.0
# cp libgstsdxtrafficdetect.so /usr/lib/gstreamer-1.0

```

6. Set up the host machine (Windows 10) to disable the firewall if any firewall software is running, install VLC player, configure the network settings, and run the eight streams of video by launching the 8 VLC media player instances that work as RTSP servers. If IP cameras are being used for some of these streams, run the media files for the remaining streams.

7. Set up the device by running the following command from the booted Linux from ``/media/card``. Update the `setup.sh` file (if needed) for the ``plane-id`` before running the command.

`source setup.sh`

8. Running the following command from the booted Linux from ``/media/card`` sets the DDR ports for performance optimization:

`source qos.sh`

### 7.2.3. Examples

There are multiple ways of testing this platform by giving eight streams of inputs; either from file source media files or from Ethernet streams. These can be run for either face detect, traffic detect, or both.

For the 8-stream VCU + CNN platform, four face detect and four traffic detect streams can be run with a different mixer ``plane-id`` numbered from 30 to 37. Check `8_ch_traffic_face.sh` for the complete pipeline. If you have a 1920x1080 resolution monitor, run the script as shown in the following example:

```
  source 8_ch_traffic_face.sh
```

For the 8-stream VCU + CNN platform, when the streams are transmitted over Ethernet, run the following script from the ``sdcard`` folder (`/media/card`):

```
  source urls_demo_2019_1080p.sh
```

The same script can also be run from the application executable that is generated using the given `rtsp` application project workspace. This executable has an extra feature: it displays the count of faces and objects.

```
  ./rtsp
```
If you experience any issues in running the `rtsp` application, perform the following steps:

1. Close all the VLC media player instances from the Windows task manager.
2. Check that the firewall is disabled on your Windows machine. 
3. Check that Ethernet cables are connected properly between the laptop/IP camera and the Ethernet switch, and between the Ethernet switch and the ZCU104 board. 
4. Check that the IP address settings match with the RTSP server addresses and the inputs.conf URL addresses.
5. Run all eight instances of the RTSP servers by VLC player or the IP cameras.
6. Reboot the ZCU104 board. Go to `/media/card`, source the `setup.sh` file, and run `./rtsp`.

#### 7.2.3.1 Face Detect

The following code example is a ``gst-launch`` command to run the single-stream VCU + CNN  pipeline for face detect, with input from an H264 encoded file already in the ``demo_input`` folder, and HDMI output through mixer plane 30:

```

	gst-launch-1.0 filesrc location=demo_inputs/face_15fps.mp4 ! qtdemux ! h264parse ! omxh264dec internal-entropy-buffers=3 ! xlnxvideoscale !  \
	video/x-raw, width=$WIDTH, height=$HEIGHT, format=BGR !  \
	sdxfacedetect ! queue ! \
	fpsdisplaysink video-sink="kmssink plane-id=30 bus-id="a2070000.v_mix" render-rectangle=\"<$WOFF,$HOFF,$WIDTH,$HEIGHT>\"" text-overlay=false sync=false -v


```

For the 8-stream platform, eight similar instances could be run with a different mixer ``plane-id`` numbered from 30 to 37. Check `8_ch_face.sh` for the complete pipeline. If you have a 1920x1080 resolution monitor, run the script as shown in the following example:

```
  source 8_ch_face.sh
```

#### 7.2.3.2 Traffic Detect

The following code example is a ``gst-launch`` command to run the single-stream VCU + CNN  pipeline for traffic detect, with input from an H264 encoded file already in the ``demo_input`` folder, and HDMI output through mixer plane 30.

```

	gst-launch-1.0 multifilesrc location=demo_inputs/file_%02d.dmp loop=true ! h264parse ! omxh264dec internal-entropy-buffers=3 ! xlnxvideoscale !  \
	video/x-raw, width=$WIDTH, height=$HEIGHT, format=BGR !  \
	sdxtrafficdetect ! queue ! \
	fpsdisplaysink video-sink="kmssink plane-id=30 bus-id="a2070000.v_mix" render-rectangle=\"<$WOFF,$HOFF,$WIDTH,$HEIGHT>\"" text-overlay=false -v


```

For the 8-stream platform, eight similar instances could be run with a different mixer ``plane-id`` numbered from 30 to 37. Check `8_ch_face.sh` for the complete pipeline. If you have a 1920x1080 resolution monitor, run the script as shown in the following example:

```
  source 8_ch_traffic.sh
```
</details>

## 7.3. Run the Face Detect Application (ZCU104 Smart Camera Platform)

<details>
<br>
The C-callable project containing the hardware-accelerated code is a Vitis™ environment project (for example, `<TBD>`). When it completes, it creates an SD card image with files you need to copy to the SD card you'll use on the target board. All the libraries and plugins must be copied to the ``sd_card`` root directory. [Tool Flow Tutorials](#6-tool-flow-tutorials.md) provides details about the files to be copied to ``sdcard``.

### 7.3.2. Instructions

Before starting the example run, configure the network of the host machine. Create a loopback connection between target and host:

**:pushpin: NOTE:** The instructions assume a scenario where VLC media player is already installed on the host machine, and plays the transmitted frames from a ZCU104 board.

### 7.3.2.1. Setting Up the Host Machine

1. Set the host IP to 192.168.1.112. Make sure the firewall configuration in the host machine allows traffic from this network configuration.

2. Set the IP of the ZCU104 target device to IP 192.168.1.113. See the following command for an example of how to set up the IP manually from the command line:

``netsh int ip set address "Ethernet" static 192.168.1.112 255.255.255.0 192.168.1.113``

**:pushpin: NOTE:** Before testing the demo application, make sure that the ZCU104 device and host are able to communicate with each other; that is to say, ensure that the Ethernet connection is working correctly. You can verify the Ethernet connection by performing the following checks:
  * From the host, ping 192.168.1.113. The host should be able to send and receive data from the ZCU104 device.
  * From the ZCU104 device, ping 192.168.1.112. The device should be able to send and receive data from the ZCU104 device.
  * If the previous commands do not work, make sure that you are using a cross-over Ethernet cable, that you have set up the IP addresses of the host and device correctly, and that the firewall is disabled.

### 7.3.2.2. Setting Up the ZCU104 Device and Running the Demo

1. Insert the SD card in the SD card slot on your target board.
2. Power on the board; make sure the large INIT_B LED and the DONE LED next to it go green after a few seconds.
3. Control the system from your computer: start a terminal session using TeraTerm, PuTTY or similar (see [Build the Live I/O Optical Flow Sample Application](tool-flow-tutorials.md#611-build-the-live_io-optical-flow-sample-application)). With the USB-UART cable connected and the board powered up, you can locate the COM port that is responsive. You'll see several pages of Linux bootstrap and debug messages scroll by, finishing at the Linux command line prompt.
4. Using ``cd``, go to the `/run/media/mmcblk0p1` directory. This directory contains all the files you copied to your SD card.
```
# cd /run/media/mmcblk0p1

```

5. Configure the IP of the target ZCU104 device:

```
ifconfig eth0 192.168.1.113 up

```
6. Set up an environment for XRT:
```
export XILINX_XRT=/usr
export LD_LIBRARY_PATH=$XILINX_XRT/lib:$LD_LIBRARY_PATH
export PATH=$XILINX_XRT/bin:$PATH
export PYTHONPATH=$XILINX_XRT/python:$PYTHONPATH
export DPU_COMPILATIONMODE=1

```

### 7.3.2.3. RTSP Stream Example

Use the ``demo.sh`` script provided as part of the package to run the RTSP stream server. A VLC player in the host can then be used to receive and display the stream.

1. Run the `demo.sh` application available as part of a package:

```
./demo.sh

```

In the ZCU104 device UART console, wait for the message ``stream ready at rtsp://<IP>:8554/test`` to appear.

2. In the host, start a VLC instance. Go to **Media** → **Open Network Stream** → **Network**. Enter ``rtsp://192.168.1.113:8554/test`` in the **Network Protocol** box. Click the play button (make sure the firewall is disabled in the host machine). The DNNDK-processed facedetect stream will start playing in the VLC player. Simultaneously, the original stream **_not_** processed by DNNDK will appear in the DisplayPort monitor.

### 7.3.2.3. Running the Demo for Regulus ISP

1. Extract the ``zcu104_smart_camera_regulusisp.zip`` and copy the contents of ``zcu104_smart_camera_regulusisp_2019_1/sdcard`` to the SD card.
2. Insert the SD card in the SD card slot on your target board.
3. Power on the board; make sure the large INIT_B LED and the DONE LED next to it go green after a few seconds.
4. Control the system from your computer: start a terminal session using TeraTerm, PuTTY or similar (see [Build the Live I/O Optical Flow Sample Application](tool-flow-tutorials.md#611-build-the-live_io-optical-flow-sample-application)). With the USB-UART cable connected and the board powered up, you can locate the COM port that is responsive. You'll see several pages of Linux bootstrap and debug messages scroll by, finishing at the Linux command line prompt.
5. Using ``cd``, go to the `/run/media/mmcblk0p1` directory. This directory contains all the files you copied to your SD card.
```
# cd /run/media/mmcblk0p1

```

6. Configure the IP of the target ZCU104 device:

```
ifconfig eth0 192.168.1.113 up

```
7. Set up an environment for XRT:
```
export XILINX_XRT=/usr
export LD_LIBRARY_PATH=$XILINX_XRT/lib:$LD_LIBRARY_PATH
export PATH=$XILINX_XRT/bin:$PATH
export PYTHONPATH=$XILINX_XRT/python:$PYTHONPATH
export DPU_COMPILATIONMODE=1

```

8. Run the `demo.sh`:

```
./demo.sh

```

In the zcu104 device UART console, wait for the message ``stream ready at rtsp://<IP>:8554/test`` to appear.

10. In the host, start a VLC instance. Go to **Media** → **Open Network Stream** → **Network**. Enter ``rtsp://192.168.1.113:8554/test`` in the **Network Protocol** box. Click the play button. (Make sure the firewall is disabled in the host machine). The DNNDK-processed facedetect stream will start playing in the VLC player. Simultaneously, the original stream **_not_** processed by DNNDK will appear in the DisplayPort monitor.
</details>

## 7.4. GStreamer Elements

<details>
<br>
	
These pipelines use the elements `xlnxvideosrc`, `queue`, `xlnxvideosink`, and `sdxfilter2d` (or `sdxopticalflow`, or `sdxstereo`). You can display properties and other information about any of these elements using the `gst-inspect-1.0` GStreamer utility.

### 7.4.1. xlnxvideosrc

```

# gst-inspect-1.0 xlnxvideosrc

```

  * ``src-type`` property
    - (-1): none: Video Source NONE
    - (0): vivid: Virtual Video Device
    - (1): mipi: MIPI CSI2 RX
    - (2): hdmi: HDMI Input
    - (3): usbcam: USB Webcam
    - (4): tpg: Test Pattern Generator
    - (5): mipi_quad_vc0: MIPI Quad Virtual Channel 0
    - (6): mipi_quad_vc1: MIPI Quad Virtual Channel 1
    - (7): mipi_quad_vc2: MIPI Quad Virtual Channel 2
    - (8): mipi_quad_vc3: MIPI Quad Virtual Channel 3

  * Children:
    - ``v4l2src0``



### 7.4.2. queue

This is not strictly necessary, but using it delivers better performance (that is, the highest possible frame rate).

### 7.4.3. xlnxvideosink

To inspect the xlnxvideosink plugin:
```

gst-inspect-1.0 xlnxvideosink

```

* ``sink-type`` property
  * (-1): none: None.
  * (0): dp: DisplayPort.
  * (1): hdmi: HDMI output.

* ``plane-id`` property
  - If you are using ``b00c0000.v_mix`` (HDMI output):
    - ``29`` is a YUY2 plane.
    - ``30`` is a YUY2 plane.
    - ``31`` is a UYUV plane.
* If you are using ``fd4a0000.zynqmp-display`` (DP output):
    - ``35`` supports a number of RGB.
    - ``34`` supports YUY2 and UYVY.
* Children:
  - ``kmssink0``

### 7.4.4. xlnxvideoscale

  To inspect the ``xlnxvideoscale`` plugin:
  ```

  # gst-inspect-1.0 xlnxvideoscale

  ```

### 7.4.5. sdx&lt;accelerator&gt;

To inspect the ``sdxfilter2d`` plugin:
```

# gst-inspect-1.0 sdxfilter2d

```

* ``filter_mode`` property
  * 1: Use HW acceleration.
  * 0: Use SW (the filter2d code executes entirely on the Arm™ processor).
* ``filter_preset`` property
  * Values 1 - 10 select a number of preset filters. The example uses 4, which is the emboss or edge enhancement filter.
* ``coefficients`` property
  * Array with a 3x3 coefficient matrix (for example,`coefficients="<<0,0,0>,<0,-1,0>,<0,0,0>>"`).

To inspect the ``sdxopticalflow`` plugin:
```

# gst-inspect-1.0 sdxopticalflow

```

* ``filter_mode`` property
  * 1: Use HW acceleration.
  * 0: Use SW (the optical flow code executes entirely on the Arm processor).

To inspect the ``sdxstereo`` plugin:
```

# gst-inspect-1.0 sdxstereo

```

* ``filter_mode`` property
  * 1: Use HW acceleration.
  * 0: Use SW (the optical flow code executes entirely on the Arm processor).
* ``config-filename`` property
  * This is how you specify the ZED camera configuration file, which must be present on the SD card (see [Single Sensor Platform Stereo Demo: Special Considerations](#76-single-sensor-platform-stereo-demo-special-considerations)).
</details>

## 7.5. Run the Live I/O Sample Applications (Single Sensor Platform for the Vitis Environment)

<details>
<br>
The bottom project contains the hardware accelerated code is a Vitis™ environment project (for example, `./ws_sv/stereo`). When it completes, it creates an SD card image with files you need to copy to the SD card you'll use on the target board. All the libraries and plugins must be copied to the ``sd_card`` root directory. The following sections list the exact files for each case.

:pushpin: **IMPORTANT**: For the stereo case, you also need the camera configuration file on the SD card (see [Single Sensor Platform Stereo Demo: Special Considerations](#76-single-sensor-platform-stereo-demo-special-considerations)).

### 7.5.1. Files for filter2d

After building the bottom library, your ``sd_card`` directory will contain the following files:
* `./ws_f2d/filter2d/System/sd_card/image.ub`
* `./ws_f2d/filter2d/System/sd_card/binary_container_1.xclbin`
* `./ws_f2d/filter2d/System/sd_card/BOOT.BIN`

The top projects generate the shared library files for GStreamer and the XRT mapping layer:
* `./workspaces/ws_f2d/gst/allocators/Debug/libgstxclallocator.so`
* `./workspaces/ws_f2d/gst/base/Debug/libgstsdxbase.so`
* `./workspaces/ws_f2d/gst/plugins/gstsdxfilter2d/Debug/libgstsdxfilter2d.so`
* `./workspaces/ws_f2d/xcl_filter2d/Debug/libxcl_filter2d.so`
* `./workspaces/ws_f2d/xrtutils/Debug/libxrtutils.so`

>**:information_source: TIP** Copy all the images listed above directly into the root folder of the SD card. Source the ``qos.sh`` file from the terminal before running the ``gst`` commands. Doing this sets the DDR controller link for video traffic and ensures the display works correctly for a resolution of 3840x2160.

### 7.5.2. Files for opticalflow

After building the bottom library, your ``sd_card`` directory will contain the following files:
* `./ws_of/opticalflow/System/sd_card/image.ub`
* `./ws_of/opticalflow/System/sd_card/binary_container_1.xclbin`
* `./ws_of/opticalflow/System/sd_card/BOOT.BIN`

The top projects generate the shared library files for GStreamer and the XRT mapping layer:
* `./workspaces/ws_of/gst/allocators/Debug/libgstxclallocator.so`
* `./workspaces/ws_of/gst/base/Debug/libgstsdxbase.so`
* `./workspaces/ws_of/gst/plugins/gstsdxopticalflow/Debug/libgstsdxopticalflow.so`
* `./workspaces/ws_of/xcl_opticalflow/Debug/libxcl_opticalflow.so`
* `./workspaces/ws_of/xrtutils/Debug/libxrtutils.so`

>**:information_source: TIP** Copy all the images listed above directly into the root folder of the SD card. Copy the `qos.sh` file from the `sd_card/optical_flow` folder of the package. Source the ``qos.sh`` file from Linux before running the ``gst`` commands. Doing this sets the DDR controller link for video traffic and ensures the display works correctly for a resolution of 3840x2160.

### 7.5.3. Files for stereo

After building the bottom library, your ``sd_card`` directory will contain the following files:
* `./ws_sv/stereo/System/sd_card/image.ub`
* `./ws_sv/stereo/System/sd_card/binary_container_1.xclbin`
* `./ws_sv/stereo/System/sd_card/BOOT.BIN`

The top projects generate the shared library files for GStreamer and the XRT mapping layer:
* `./workspaces/ws_sv/gst/allocators/Debug/libgstxclallocator.so`
* `./workspaces/ws_sv/gst/base/Debug/libgstsdxbase.so`
* `./workspaces/ws_sv/gst/plugins/gstsdxstereo/Debug/libgstsdxstereo.so`
* `./workspaces/ws_sv/xcl_stereo/Debug/libxcl_stereo.so`
* `./workspaces/ws_sv/xrtutils/Debug/libxrtutils.so`

>**:information_source: TIP** Copy all the images listed above directly into the root folder of the SD card. Copy the ``gst`` scripts to the filter workspaces `./workspaces/<ws_f2d or ws_of or ws_sv>/scripts/gst` into the SD card. Update the script so that it includes the correct plane IDs for video-sink before running these scripts.

### 7.5.5. Instructions

1. Insert the SD card in the SD card slot on your target board.
2. Power on the board; make sure the large INIT_B LED and the DONE LED next to it go green after a few seconds.
3. Control the system from your computer: start a terminal session using TeraTerm, PuTTY or similar (see [Build the Live I/O Optical Flow Sample Application](tool-flow-tutorials.md#611-build-the-live_io-optical-flow-sample-application)). With the USB-UART cable connected and the board powered up, you can locate the COM port that is responsive. You'll see several pages of Linux bootstrap and debug messages scroll by, finishing at the Linux command line prompt.
4. Using ``cd``, go to the `/media/card` directory. This directory contains all the files you copied to your SD card.
```
# cd /media/card

```

### 7.5.6 GStreamer Application

To create and run the GStreamer pipeline, use the prebuilt `gst-launch` utility. The following code example is a ``gst-launch`` command to run the ``filter2d`` pipeline, from MIPI, 1920x1080, YUY2, to the HDMI output through mixer plane 29.
```

gst-launch-1.0 \
    xlnxvideosrc src-type="mipi" ! \
    "video/x-raw, width=1920, height=1080, format=YUY2" ! \
    sdxfilter2d filter-preset=4 filter-mode=1 ! queue ! \
    xlnxvideosink sink-type="hdmi" plane-id=29 sync=false fullscreen-overlay=true

```
```
Giving an incorrect ``plane-id`` number for the ``gst-launch-1.0`` command causes the following error message: ERROR: Pipeline doesn't want to pause. To find out the ``plane-id`` for DP/HDMI sink, run the following ``cat`` command, get the dri name for DP/HDMI, and use the `modetest -D <unique-name>` command to get the ``plane-id`` for the YUYV color format:

cat /sys/kernel/debug/dri/*/name
xlnx dev=fd4a0000.zynqmp-display unique=fd4a0000.zynqmp-display
xlnx dev=b00c0000.v_mix unique=b00c0000.v_mix
modetest -D b00c0000.v_mix for HDMI sink and modetest -D fd4a0000.zynqmp-display for DP Sink`
```

The following code example is a ``gst-launch`` command to run the ``opticalflow`` pipeline, from HDMI, 1920x1080, YUY2, to the HDMI output through mixer plane 29.
```

gst-launch-1.0 \
    xlnxvideosrc src-type="hdmi" ! \
    "video/x-raw, width=1920, height=1080, format=YUY2" ! \
    sdxopticalflow filter-mode=1 ! queue ! \
    xlnxvideosink sink-type="hdmi" sync=false fullscreen-overlay=true

```


The following code example is a ``gst-launch`` command to run the stereo pipeline, from USB, 3840x1080 side-by-side input, YUY2, 1920x1080 output to HDMI through mixer plane 29. You must substitute your camera serial number for the ``config-filename`` property. See the section below on [Single Sensor Platform Stereo Demo: Special Considerations](#76-single-sensor-platform-stereo-demo-special-considerations).
```

gst-launch-1.0 \
    xlnxvideosrc src-type="usbcam"  ! \
    "video/x-raw, width=3840, height=1080, format=YUY2" ! \
    sdxstereo filter-mode=1 config-filename=/media/card/SN12263.conf ! queue ! \
    xlnxvideosink sink-type="hdmi" plane-id=29 sync=false fullscreen-overlay=true

```


The following example shows an alternative way to run ``filter2d`` with frames-per-second display enabled. Notice the output pipe stage is ``fpsdisplaysink``, and that the previously used ``xlnxvideosink....`` string is a property of ``fpsdisplaysink`` called ``video-sink``.
```

gst-launch-1.0 \
    xlnxvideosrc src-type="mipi" ! \
    "video/x-raw, width=1920, height=1080, format=YUY2" ! \
    sdxfilter2d filter-preset=4 filter-mode=1 ! queue ! \
    fpsdisplaysink video-sink="xlnxvideosink sink-type=hdmi plane-id=29 fullscreen-overlay=true" sync=false text-overlay=false -v

```
You can also refer to the ``gst`` scripts provided as part of `./workspaces/ws_f2d/scripts` or `./workspaces/ws_of/scripts` or `./workspaces/ws_sv/scripts`. Copy the `*.sh` files from these folders into the SD card, update the ``plane-id`` numbers and the source and sink types, and run them from booted Linux. In the case of any issues with running the application, make sure the `plane-id` is given correctly.
</details>

## 7.6. Single Sensor Platform Stereo Demo: Special Considerations

<details>
<br>
	
	
The stereo vision demo is special in several ways. First, you _must_ use the ZED stereo camera connected to the USB video input. Second, and particular to this app, the width of the input image resolution is twice the width of the output resolution. The input consists of two images side-by-side, with the synchronized left and right stereo input supplied by the camera. Two cases are possible: 2560x720 in to 1280x720 out, and 3840x1080 in to 1920x1080 out. The default 3840x2160 output resolution is not supported by the Stereo Vision app.

The other special consideration is that a configuration file must be used that corresponds to the camera you have connected to your system. Each StereoLabs ZED camera has a unique parameters file associated with it. This text file comes from StereoLabs, and must be present on the SD Card for the Stereo Vision demo to work properly. You need the file unique to your camera, identified by its serial number (found on the ZED camera box and also on a black tag near the USB plug of the ZED camera itself). This number will be, for example, S/N 000012345. The parameter file for that camera would be named ``SN12345.conf``. To download your parameter file, enter the following URL into your browser, http://calib.stereolabs.com/?SN=XXXXX, adding the correct serial number. This downloads the configuration file to your computer.

The stereo block-matching algorithm calculates depth based on binocular parallax, similar to the way human eyes perceive depth. The depth map is coded in false colors. Objects far away appear deep blue. Closer objects appear in rainbow succession: green, yellow, orange, red, purple and finally white at about two feet from the camera in the 720p case, and about five feet away in the 1080p case. Any object closer than that cannot be tracked, and smooth areas with no texture in the image cannot be tracked, and show up as black. Areas with a lot of detail (especially with lots of vertical edges) are tracked best. It is normal that a large area on the left is black; this is 128 pixels wide, representing the range of the horizontal search for the best match between the right and left binocular images.

</details>

<hr/>

:arrow_forward:**Next Topic:**  [8. Platform Details](platform-details.md)

:arrow_backward:**Previous Topic:**  [6. Tool Flow Tutorials](tool-flow-tutorials.md)
<hr/>
<p align="center"><sup>Copyright&copy; 2018–2019 Xilinx</sup></p>
