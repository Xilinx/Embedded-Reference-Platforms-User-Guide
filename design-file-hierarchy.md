<p align="right">
            Read this page in other languages:<a href="../Japanese-master/design-file-hierarchy.md">日本語</a>    <table style="width:100%"><table style="width:100%">
  <tr>

<th width="100%" colspan="6"><img src="https://www.xilinx.com/content/dam/xilinx/imgs/press/media-kits/corporate/xilinx-logo.png" width="30%"/><h1>reVISION Getting Started Guide 2018.2</h1>
</th>

  </tr>
  <tr>
    <td width="17%" align="center"><a href="README.md">1. Introduction</a></td>
    <td width="16%" align="center"><a href="overview.md">2. Overview</a></td>
    <td width="17%" align="center"><a href="software-tools-system-requirements.md">3. Software Tools and System Requirements</a></td>
    <td width="17%" align="center">4. Design File Hierarchy</td>
</tr>
<tr>
    <td width="17%" align="center"><a href="operating-instructions.md">5. Installation and Operating Instructions</a></td>
    <td width="16%" align="center"><a href="tool-flow-tutorials.md">6. Tool Flow Tutorials</a></td>
    <td width="17%" align="center"><a href="run-application.md">7. Run the Application</a></td>
    <td width="17%" align="center"><a href="platform-details.md">8. Platform Details</a></td>    
  </tr>
<tr>
    <td width="17%" align="center" colspan="2"><a href="known-issues-limitations.md">9. Known Issues and Limitations</a></td>
    <td width="16%" align="center" colspan="2"><a href="additional-references.md">10. Additional References</a></td>
</tr>
</table>

# 4 Design File Hierarchy

The Zynq UltraScale+ MPSoC reVISION Platform zip file is released with the binary and source files required to create Xilinx SDx projects and build the sample applications. The sample applications are built as GStreamer plugins and test designs to exercise them. The provided samples include five file I/O examples and four live I/O examples. The file I/O examples read an input image file and produce an output image file whereas the live I/O examples take live video input from a video source and output live video on a display.

The single-sensor reVISION platform contain the following components:
* **zcu102_rv_ss** SDSoC Platform
  * **hw** contains the .dsa file describing the hardware platform.
  * **samples** contains sample app code. Each sample directory has a .json file describing the build process. These are the SDx sample apps that appear in the "Template" dialog when creating a new project using the reVISION platform.
    * **file_IO** projects are self-contained.
    * **live_IO** projects are more complex, and are built in several steps. See section 7.
  * **sw** contains software - bootloaders and other code and support files for the processors on the ZCU10x target board.
* **petalinux** contains a petalinux bsp with device tree info, hardware description files, and other system setup files. An advanced user has the option of creating their own platform. A sysroot is included as zip file.
* **sd_card** contains pre-built SD card images that enable the user to run the live I/O example applications on the ZCU10x board.
* **workspaces** contains a workspace directory structure you may use to build the live_IO samples. See section 7.

```
zcu102-rv-ss-2018-2
├── IMPORTANT_NOTICE_CONCERNING_THIRD_PARTY_CONTENT.txt
├── petalinux
│   ├── zcu102_rv_ss.bsp
│   └── sdk.zip
├── README.txt
├── sd_card
│   ├── filter2d
│   ├── optical_flow
│   ├── stereo
│   └── triple
├── workspaces
│   ├── ws_f2d
│   │   └── gst
│   │       ├── allocators
│   │       ├── apps
│   │       ├── base
│   │       └── plugins
│   ├── ws_of
│   │   └── gst
│   │       ├── allocators
│   │       ├── apps
│   │       ├── base
│   │       └── plugins
│   ├── ws_sv
│   │   └── gst
│   │       ├── allocators
│   │       ├── apps
│   │       ├── base
│   │       └── plugins
│   ├── ws_triple
│   │   └── gst
│   │       ├── allocators
│   │       ├── apps
│   │       ├── base
│   │       └── plugins
│   └── ws_video
│       ├── gst_lib
│       ├── video_cmd
│       └── video_lib
└── zcu102_rv_ss
    ├── hw
    │   └── zcu102_rv_ss.dsa
    ├── samples
    │   ├── file_IO
    │   │   ├── bilateral_fileio
    │   │   ├── harris_fileio
    │   │   ├── opticalflow_fileio
    │   │   ├── steoreolbm_fileio
    │   │   └── warptransform_fileio
    │   └── live_IO
    │       ├── filter2d
    │       ├── optical_flow
    │       ├── stereo
    │       └── triple
    ├── sw
    │   ├── a53_linux
    │   ├── prebuilt
    │   └── zcu102_rv_ss.spfm
    └── zcu102_rv_ss.xpfm
```

<hr/>

:arrow_forward:**Next Topic:**  [5. Installation and Operating Instructions](operating-instructions.md)

:arrow_backward:**Previous Topic:**  [3. Software Tools and System Requirements](software-tools-system-requirements.md)
<hr/>
<p align="center"><sup>Copyright&copy; 2018 Xilinx</sup></p>
