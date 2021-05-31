<p align="right">
            Read this page in other languages:<a href="docs-jp/README.md">日本語</a>          
</p>
<table style="width:100%">
  <tr>

<th width="100%" colspan="6"><img src="https://github.com/Xilinx/Image-Collateral/blob/main/xilinx-logo.png?raw=true" width="30%"/><h1>Vitis Software Platform: Embedded Vision Reference Platforms User Guide 2019.2 (UG1265)</h1>
</th>

  </tr>
  <tr>
    <td width="17%" align="center">1. Introduction</td>
    <td width="16%" align="center"><a href="./Docs/overview.md">2. Overview</a></td>
    <td width="17%" align="center"><a href="./Docs/software-tools-system-requirements.md">3. Software Tools and System Requirements</a></td>
    <td width="17%" align="center"><a href="./Docs/design-file-hierarchy.md">4. Design File Hierarchy</a></td>
</tr>
<tr>
    <td width="17%" align="center"><a href="./Docs/operating-instructions.md">5. Installation and Operating Instructions</a></td>
    <td width="16%" align="center"><a href="./Docs/tool-flow-tutorials.md">6. Tool Flow Tutorials</a></td>
    <td width="17%" align="center"><a href="./Docs/run-application.md">7. Run the Application</a></td>
    <td width="17%" align="center"><a href="./Docs/platform-details.md">8. Platform Details</a></td>    
  </tr>
<tr>
    <td width="17%" align="center" colspan="2"><a href="./Docs/known-issues-limitations.md">9. Known Issues and Limitations</a></td>
    <td width="16%" align="center" colspan="2"><a href="./Docs/additional-references.md">10. Additional References</a></td>
</tr>
</table>

# 1. Introduction

The Vitis™ unified software platform is a new software development product based on a unified flow using XRT (Xilinx runtime). New embedded platforms are supported on the Vitis software platform, and SDSoC platforms are now deprecated. The Vitis software platform replaces the  SDK, SDSoC™, and SDAccel™ development environments. It offers the original SDx environment features along with new features, such as improved profiling and emulation, extensible open-source runtime, and scalable library/application development across data center and embedded technologies. The new DFX version of the platforms provides a shell where the kernel can be programmed without reimplementing the complete hardware design. For more information, visit the [Vitis software platform web page](https://www.xilinx.com/products/design-tools/vitis/vitis-platform.html).

This guide covers the following embedded vision reference platforms for the Vitis environment. These reference platforms enable you to build computer vision and machine learning accelerators using Vitis platforms which have video source and video sink pipelines running on Zynq® SoCs and MPSoCs:

  - ZCU104 Single Sensor
  - 8-stream VCU + CNN
  - ZCU104 Smart Camera

These Vitis embedded platforms can be generated using [sources](https://github.com/Xilinx/Vitis_Embedded_Platform_Source/tree/2019.2). The [pre-built platforms](https://www.xilinx.com/support/download/index.html/content/xilinx/en/downloadNav/embedded-platforms.html) are also available if you wish to use them directly to build the accelerators.

**:pushpin: NOTE:**
>The ZCU104 Smart Camera platform is supported by both Xilinx and Regulus image signal processing (ISP). The design with the Regulus ISP is not provided here due to licensing limitations; only the SD card image is available for evaluation. For access to the Regulus ISP design, contact Regulus.

For other versions, refer to the [reVISION Getting Started Guide](http://www.wiki.xilinx.com/reVISION%20Getting%20Started%20Guide) overview page on the Xilinx wiki.

## 1.1. Revision History

**2019.2**
* All the platforms from 2019.1 are migrated to the 2019.2 Vitis software platforms.
* Platforms are being released with platform sources as well as the pre-built platforms.
* Added new Zynq-7000 SoC base platforms (ZC702 and ZC706).
* Added DFX (Dynamic Function eXchange) version of ZCU102 base platform.
* Removed support for SDSoC platforms.
* Updated to the 2019.2 version of the Vitis Vision libraries (previously known as xfOpenCV libraries).
* Updated to the 2019.2 version of Vivado.
* Updated to the 2019.2 version of PetaLinux.
* Smart Camera with ROI support.

**2019.1**
* All the SDSoC platforms from 2018.3 are moved to the Vitis software platform. In 2019.1, the Vitis tool is early access only.
* Added new ZCU104 Smart Camera platform for the Vitis software platform.
* Added new ZCU104 8-Stream VCU + CNN platform for the Vitis software platform.
* Added ZCU104 Single Sensor platform support for the Vitis software platform along with SDSoC.
* Updated to 2019.1 SDSoC version for reVISION MIN and Single Sensor platforms.
* Updated to 2019.1 xfOpenCV libraries version.
* Updated to 2019.1 Vivado version.
* Updated to 2019.1 PetaLinux version.
* Removed support for ZCU102 Single Sensor platform.

**2018.3**
* Added new 8-stream VCU + CNN platform.
* Updated to 2018.3 SDSoC version.
* Updated to 2018.3 xfOpenCV libraries version.
* Updated to 2018.3 Vivado version.
* Updated to 2018.3 PetaLinux version.
* Removal of `video_cmd` and addition of new `xlnxvideosrc` and `xlnxvideosink` plugins.
* Minor fixes and improvements.


**2018.2**
* Updated to 2018.2 SDSoC version.
* Updated to 2018.2 xfOpenCV libraries version.
* Updated to 2018.2 Vivado version.
* Updated to 2018.2 PetaLinux version.
* Minor fixes and improvements.



## 1.3. Technical Support

Go to the [Xilinx Answers Database](https://www.xilinx.com/support.html) to locate answers to known issues. Go to the [Xilinx Community Forums](https://forums.xilinx.com/) to ask questions or discuss technical details and issues. Make sure to browse the existing topics first before filing a new topic. If you do file a new topic, make sure it is filed in the sub-forum that best describes your issue or question (for example, Embedded Linux for any Linux-related questions). Include the platform name (for example, ZCU104 Smart Camera) and the release version in the topic name along with a brief summary of the issue.

<hr/>

:arrow_forward:**Next Topic:**  [2. Overview](./Docs/overview.md)

<hr/>
<p align="center"><sup>Copyright&copy; 2018–2019 Xilinx</sup></p>
