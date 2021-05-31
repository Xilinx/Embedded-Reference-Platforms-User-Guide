<p align="right">
            Read this page in other languages:<a href="../docs-jp/Docs/platform-details.md">日本語</a>    <table style="width:100%"><table style="width:100%">
  <tr>

<th width="100%" colspan="6"><img src="https://github.com/Xilinx/Image-Collateral/blob/main/xilinx-logo.png?raw=true" width="30%"/><h1>Vitis Software Platform: Embedded Vision Reference Platforms User Guide 2019.2 (UG1265)</h1>
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
    <td width="17%" align="center"><a href="run-application.md">7. Run the Application</a></td>
    <td width="17%" align="center">8. Platform Details</td>    
  </tr>
<tr>
    <td width="17%" align="center" colspan="2"><a href="known-issues-limitations.md">9. Known Issues and Limitations</a></td>
    <td width="16%" align="center" colspan="2"><a href="additional-references.md">10. Additional References</a></td>
</tr>
</table>

# 8. Platform Details

The below instructions refer to the ZCU104 Single Sensor platform. Follow the same instructions, replacing only the file name, for the 8-stream VCU + CNN and ZCU104 Smart Camera platforms.

## 8.1. Vivado Hardware Design

The Vivado® hardware design is packaged as source and XSA. Using platform sources to generate the pre-built platform, the XSA is generated in the `hw` folder of the platform (example: `zcu104_ss/hw/zcu104_ss.xsa`). The XSA also includes the `hpfm` file that describes the available AXI interfaces, clocks, resets, and interrupts. To open the hardware design in Vivado, run the following command from the Tcl console in Vivado:

```
% cd <proj>/vivado
% vivado
% Run below command in vivado tcl console 
source <pfm_name>_xsa.tcl
```
Vivado will recreate the hardware block design. Feel free to check the details in hardware designs. The hardware design of a Vitis platform provides I/O interfaces, enable bus interfaces, clocks, and interrupts for acceleration kernels. Platform I/O details are described in  the [Overview](overview.md) chapter.

## 8.2. PetaLinux Design

PetaLinux design is distributed as source with the platforms. The sources can be found at ``<proj>/petalinux`` for each of the platforms.

To configure and build the PetaLinux BSP, run the following commands:

```
% cd <proj>/petalinux
% petalinux-config --get-hw-description=../pre-built/<pfm>/hw/<pfm>.xsa --silentconfig
% petalinux-build
```

**:pushpin: NOTE** The `tmp` directory might relocate to a different folder, especially if your PetaLinux project is located on an NFS mount. Check your PetaLinux configuration at `<proj>/petalinux/project-spec/configs/config` to update the `CONFIG_TMP_DIR_LOCATION` switch.

The generated output products are located in the `<proj>/petalinux/images/linux/` subfolder. The relevant files that are packaged as part of the platform are listed below:

* ``bl31.elf``
* ``pmufw.elf``
* ``u-boot.elf``
* ``zynqmp_fsbl.elf``
* ``image.ub``

To generate the sysroot, run the following command:

```
% petalinux-build -s
% petalinux-package --sysroot -d ../
```

The generated sysroot installer is located in ``<proj>/petalinux/images/linux/sdk.sh``. The sysroot is generated under the directory ``../``. Alternatively, the sysroot can be downloaded from [Embedded Platforms page](https://www.xilinx.com/support/download/index.html/content/xilinx/en/downloadNav/embedded-platforms.html).

<hr/>

:arrow_forward:**Next Topic:**  [9. Known Issues and Limitations](known-issues-limitations.md)

:arrow_backward:**Previous Topic:**  [7. Run the Application](run-application.md)
<hr/>
<p align="center"><sup>Copyright&copy; 2018–2019 Xilinx</sup></p>
