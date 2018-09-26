<p align="right">
            Read this page in other languages:<a href="../Japanese-master/software-tools-system-requirements.md">日本語</a>    <table style="width:100%"><table style="width:100%">
  <tr>

<th width="100%" colspan="6"><img src="https://www.xilinx.com/content/dam/xilinx/imgs/press/media-kits/corporate/xilinx-logo.png" width="30%"/><h1>reVISION Getting Started Guide 2018.2</h1>
</th>

  </tr>
  <tr>
    <td width="17%" align="center"><a href="README.md">1. Introduction</a></td>
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

# 3 Software Tools and System Requirements

## 3.1 Hardware

**Required:**
* [ZCU104 Evaluation Board](https://www.xilinx.com/products/boards-and-kits/zcu104.html), **or**
* [ZCU102 Evaluation Board](https://www.xilinx.com/products/boards-and-kits/ek-u1-zcu102-g.html)
   * rev 1.0 with ES2 silicon **or**
   * rev 1.0 with production silicon
* Micro-USB cable, connected to laptop or desktop computer for the terminal emulator
* SD card (ZCU102) **or**
* micro-SD card (ZCU104)

**Optional (needed for live I/O examples):**
* Monitor with DisplayPort or HDMI input supporting one of the following resolutions:
  * 3840x2160 **or**
  * 1920x1080 **or**
  * 1280x720
* Display Port cable (DP certified) or HDMI cable
* [Leopard LI-IMX274MIPI-FMC](https://leopardimaging.com/product/li-imx274mipi-fmc/)
* [Stereolabs ZED USB stereo camera](https://zedstore.stereolabs.com/products/zed)
* [e-con Systems See3CAM_CU30_CHL_TC USB camera](https://www.e-consystems.com/ar0330-lowlight-usb-cameraboard.asp)
* [Xilinx USB3 micro-B adapter](http://www.whizzsystems.com/usb3-micro-b-plug-adapter)
  * adapter shipped with ZCU102 rev 1.0 + production silicon
  * adapter needs to be purchased separately from Whizz for ZCU102 rev 1.0 with ES2 silicon
  * this adapter is **NOT** required with the ZCU104 board.
* HDMI video source with output supporting one of the following resolutions:
  * 3840x2160 **or**
  * 1920x1080 **or**
  * 1280x720

## 3.2 Software

**Required:**
* Linux or Windows host machine with a minimum memory of 32GB for tool flow tutorials (see [UG1238](https://www.xilinx.com/support/documentation/sw_manuals/xilinx2018_2/ug1238-sdx-rnil.pdf) for supported OS version).
* [SDSoC Development Environment](https://www.xilinx.com/products/design-tools/software-zone/sdsoc.html) version 2018.2 (see [UG1238](https://www.xilinx.com/support/documentation/sw_manuals/xilinx2018_2/ug1238-sdx-rnil.pdf) for installation instructions)
* Serial terminal emulator (for example, Tera Term)
* [7zip](http://www.7-zip.org/) utility to extract the design zip file (**Windows only**).

  **:pushpin: NOTE** Other zip utilities may produce incorrect results!
* Design zip files:
  * ZCU102 ES2 silicon: [zcu102-es2-rv-ss-2018-2.zip](https://www.xilinx.com/member/forms/download/design-license-xef.html?akdm=1&filename=zcu102-es2-rv-ss-2018-2.zip)
  * ZCU102 Production silicon: [zcu102-rv-ss-2018-2.zip](https://www.xilinx.com/member/forms/download/design-license-xef.html?akdm=1&filename=zcu102-rv-ss-2018-2.zip)
  * ZCU104 Production silicon: [zcu104-rv-ss-2018-2.zip](https://www.xilinx.com/member/forms/download/design-license-xef.html?akdm=1&filename=zcu104-rv-ss-2018-2.zip)

## 3.3 Licensing

* **Important:** Certain material in this reference design is separately licensed by third parties and may be subject to the GNU General Public License version 2, the GNU Lesser General License version 2.1, or other licenses. The [Third Party Library Sources](https://www.xilinx.com/member/forms/download/xef.html?akdm=1&filename=zcu10x-rv-ss-2018-2-tpl-sources.zip) zip file provides a copy of separately licensed material that is not included in the reference design.
* You will need only the SDSoC license to build the design. You can evaluate for 60-days or purchase it [here](https://www.xilinx.com/products/design-tools/software-zone/sdsoc.html#buy).

**Steps to generate the license:**
1. Log in [here](http://www.xilinx.com/getproduct) with your work E-mail address (If you do not yet have an account, follow the steps under Create Account)
1. Generate a license from “Create New Licenses” by checking "SDSoC Environment, 60 Day Evaluation License"

   ![](./images/license.png)

1. Under system information, give the host details.
1. Proceed until you get the license agreement and accept it.
1. The License (.lic file) will be sent to the email-id mentioned in the login details.
1. Copy the license file locally and give the same path in the SDSoC license manager.

## 3.4 Compatibility

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
<p align="center"><sup>Copyright&copy; 2018 Xilinx</sup></p>
