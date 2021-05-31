<p align="right">
            Read this page in other languages:<a href="../docs-jp/Docs/software-tools-system-requirements.md">日本語</a>    <table style="width:100%"><table style="width:100%">
  <tr>

<th width="100%" colspan="6"><img src="https://github.com/Xilinx/Image-Collateral/blob/main/xilinx-logo.png?raw=true" width="30%"/><h1>Vitis Software Platform: Embedded Vision Reference Platforms User Guide 2019.2 (UG1265)</h1>
</th>

  </tr>
  <tr>
    <td width="17%" align="center"><a href="../README.md">1. Introduction</a></td>
    <td width="16%" align="center"><a href="overview.md">2. Overview</a></td>
    <td width="17%" align="center">3. Software Tools and System Requirements</td>
    <td width="17%" align="center"><a href="design-file-hierarchy.md">4. Design File Hierarchy</a></td>
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

# 3. Software Tools and System Requirements

## 3.1. Hardware

## 3.1.1. Single Sensor Platform

**Required:**
* [ZCU104 Evaluation Board Rev 1.0](https://www.xilinx.com/products/boards-and-kits/zcu104.html)
* Micro USB cable, connected to laptop or desktop computer for the terminal emulator
* Micro SD card

**Optional (required for live I/O examples):**
* Monitor with DisplayPort or HDMI input supporting one of the following resolutions:
  * 3840x2160
  * 1920x1080
  * 1280x720
* DisplayPort cable (DP certified) or HDMI cable
* [Leopard LI-IMX274MIPI-FMC](https://leopardimaging.com/product/li-imx274mipi-fmc/)
* [Stereolabs ZED USB stereo camera](https://zedstore.stereolabs.com/products/zed)
* [e-con Systems See3CAM_CU30_CHL_TC USB camera](https://www.e-consystems.com/ar0330-lowlight-usb-cameraboard.asp)
* HDMI video source with output supporting one of the following resolutions:
  * 3840x2160
  * 1920x1080
  * 1280x720

## 3.1.2. 8-Stream VCU + CNN Platform

**Required:**
* [ZCU104 Evaluation Board Rev 1.0](https://www.xilinx.com/products/boards-and-kits/zcu104.html)
* Micro USB cable, connected to laptop or desktop computer for the terminal emulator
* Micro SD card (>= 4 GB)
* Monitor with HDMI input supporting the following resolutions:
  * 1920x1080
* HDMI cable
* 8-port Gigabit Ethernet switch (for example, TP-LINK TL-SG108E)
* Four IP cameras capable of sending H264 1080p@15fps live video streams over RTSP over Ethernet
* Windows 10 laptop
* Six Ethernet cables

## 3.1.3. ZCU104 Smart Camera Platform

**Required:**
* [ZCU104 Evaluation Board](https://www.xilinx.com/products/boards-and-kits/zcu104.html)
* [Leopard LI-IMX274MIPI-FMC](https://leopardimaging.com/product/li-imx274mipi-fmc/)
* Micro USB cable, connected to laptop or desktop computer for the terminal emulator
* Micro SD card
* Monitor with DP input supporting one of the following resolutions:
  * 3840x2160
  * 1920x1080
* DisplayPort cable (DP certified)

## 3.2. Software

**Required:**
(see [UG1416](https://www.xilinx.com/html_docs/xilinx2019_2/vitis_doc/vhc1571429852245.html) for installation instructions).
* [Vitis™ Software Platform](https://www.xilinx.com/products/design-tools/vitis/vitis-platform.html) version 2019.2.
* Serial terminal emulator (for example, Tera Term)
* [7zip](http://www.7-zip.org/) utility to extract the design .zip file (Windows only).

  **:pushpin: CAUTION:** Other zip utilities might produce incorrect results!

* Design .zip files:
   * Single Sensor ZCU104 platform and demo for Vitis:
            [zcu104_ss_2019_2_platform.zip](https://www.xilinx.com/member/forms/download/design-license-zcu104-rv-ss.html?filename=zcu104_ss_2019_2_platform.zip),
            [zcu104_ss_2019_2_demo.zip](https://www.xilinx.com/member/forms/download/design-license-zcu104-rv-ss.html?filename=zcu104_ss_2019_2_demo.zip)
 
  * 8-stream VCU + CNN ZCU104 platform and demo for Vitis:
            [zcu104_vcu_ml_2019_2_platform.zip](https://www.xilinx.com/member/forms/download/design-license-zcu104-vcu-8channel.html?filename=zcu104_vcu_ml_2019_2_platform.zip),
            [zcu104_vcu_ml_2019_2_demo.zip](https://www.xilinx.com/member/forms/download/design-license-zcu104-vcu-8channel.html?filename=zcu104_vcu_ml_2019_2_demo.zip)

  * ZCU104 Smart Camera platform and demo for Vitis:
            [zcu104_smart_camera_xilinxisp_2019_2_platform.zip](https://www.xilinx.com/member/forms/download/design-license-zcu104-smart-camera.html?filename=zcu104_smart_camera_xilinxisp_2019_2_platform.zip),
            [zcu104_smart_camera_xilinxisp_2019_2_demo.zip](https://www.xilinx.com/member/forms/download/design-license-zcu104-smart-camera.html?filename=zcu104_smart_camera_xilinxisp_2019_2_demo.zip)
    
   * ZCU104 Smart Camera demo for Vitis with Regulus ISP:
            [zcu104_smart_camera_regulusisp_2019_2.zip](https://www.xilinx.com/member/forms/download/design-license-zcu104-smart-camera-regulusisp.html?filename=zcu104_smart_camera_regulusisp_2019_2.zip)

**:pushpin: Note:**
The platform sources used to generate the above pre-built platforms can be found at the [platform generation sources web page](https://github.com/Xilinx/Vitis_Embedded_Platform_Source/tree/2019.2/Xilinx_Official_Platforms). After you have installed the Vitis software platform and the PetaLinux tools, the pre-built platforms can be generated by following the Read Me instructions given in the source page.

## 3.3. Licensing

  **:pushpin: IMPORTANT:** Certain material in this reference design is separately licensed by third parties and may be subject to the GNU General Public License version 2, the GNU Lesser General License version 2.1, or other licenses. The Third Party Library Sources files provide a copy of separately licensed material that is not included in the platform designs. For each platorm design mentioned above, there is a corresponding Third Party Library Sources folder with the name ``DesignName-ThirdPartySources.zip``

### 3.3.1 Third Party Sources Zip Files:
  
   * Single Sensor ZCU104 platform for the Vitis environment:  [zcu104_ss_ThirdPartySources.zip](https://www.xilinx.com/member/forms/download/design-license-zcu104-rv-ss.html?filename=zcu104_ss_ThirdPartySources.zip)
  * 8-stream VCU + CNN ZCU104 platform for the Vitis environment: [zcu104_vcu_ml_2019_2_ThirdPartySources.zip](https://www.xilinx.com/member/forms/download/design-license-zcu104-vcu-8channel.html?filename=zcu104_vcu_ml_2019_2_ThirdPartySources.zip)
  * ZCU104 Smart Camera platform for the Vitis environment with Xilinx ISP: [zcu104_smart_camera_xilinxisp_ThirdPartySources_2019_2.zip](https://www.xilinx.com/member/forms/download/design-license-zcu104-smart-camera.html?filename=zcu104_smart_camera_xilinxisp_ThirdPartySources_2019_2.zip)
  * ZCU104 Smart Camera platform for the Vitis environment with Regulus ISP: [zcu104_smart_camera_regulusisp_ThirdPartySources_2019_2.zip](https://www.xilinx.com/member/forms/download/design-license-zcu104-smart-camera-regulusisp.html?filename=zcu104_smart_camera_regulusisp_ThirdPartySources_2019_2.zip)

You need the Vitis tool to build the Single Sensor, 8-Stream VCU + CNN, and Smart Camera designs. You can access it from [here](https://www.xilinx.com/support/download/index.html/content/xilinx/en/downloadNav/vitis.html).

### 3.3.2. Downloading the Vitis Software Platform

If you experience any issues with the following steps, refer to the [Vitis area on the Xilinx website](https://www.xilinx.com/member/vitis.html).

1. Log in [here](http://www.xilinx.com/getproduct) with your work e-mail address (if you do not yet have an account, follow the steps listed under Create Account).
2. Download the Vitis software platform from the download page [here](https://www.xilinx.com/support/download/index.html/content/xilinx/en/downloadNav/vitis.html).
3. Download the PetaLinux tools available [here](https://www.xilinx.com/support/download/index.html/content/xilinx/en/downloadNav/embedded-design-tools.html).

## 3.4. Compatibility

The reference design has been tested successfully with the following user-supplied components.

**Monitors:**

| **Make/Model** | **Native Resolution** |
|----|----|
| Viewsonic VP2780-4K | 3840x2160 |
| Acer S277HK | 3840x2160 |
| Dell U2414H | 1920x1080 |


**HDMI Sources:**

| **Make/Model** | **Resolutions** |
|----|----|
| Nvidia Shield TV | 3840x2160, 1920x1080 |
| OTT TV BOX M8N | 3840x2160, 1920x1080, 1280x720 |
| Roku 2 XS | 1920x1080, 1280x720 |
| TVix Slim S1 Multimedia Player | 1920x1080, 1280x720 |


**USB3 Cameras:**

| **Make/Model** | **Resolutions** |
|----|----|
| ZED stereo camera | 3840x1080, 2560x720 |
| See3CAM_CU30 | 1920x1080, 1280x720 |


**DisplayPort Cables:**
* Cable Matters DisplayPort Cable-E342987
* Monster Advanced DisplayPort Cable-E194698



<hr/>

:arrow_forward:**Next Topic:**  [4. Design File Hierarchy](design-file-hierarchy.md)

:arrow_backward:**Previous Topic:**  [2. Overview](overview.md)
<hr/>
<p align="center"><sup>Copyright&copy; 2018–2019 Xilinx</sup></p>
