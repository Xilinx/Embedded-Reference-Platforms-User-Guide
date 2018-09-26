<p align="right">
            Read this page in other languages:<a href="../Japanese-master/platform-details.md">日本語</a>    <table style="width:100%"><table style="width:100%">
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
    <td width="17%" align="center"><a href="run-application.md">7. Run the Application</a></td>
    <td width="17%" align="center">8. Platform Details</td>    
  </tr>
<tr>
    <td width="17%" align="center" colspan="2"><a href="known-issues-limitations.md">9. Known Issues and Limitations</a></td>
    <td width="16%" align="center" colspan="2"><a href="additional-references.md">10. Additional References</a></td>
</tr>
</table>

# 8 Platform Details

## 8.1 Vivado Hardware Design

The Vivado hardware design is packaged inside the DSA located at `zcu10[2|4]_[es2_]rv_ss/hw/zcu102_[es2_]rv_ss.dsa`. The DSA also includes the hpfm file that describes the available AXI interfaces, clocks, resets, and interrupts. To open the hardware design in Vivado, run the following command from the tcl console:

```
% open_dsa zcu10[2|4]_[es2_]rv_ss/hw/zcu10[2|4]_[es2_]rv_ss.dsa
```


## 8.2 PetaLinux BSP

The PetaLinux BSP is located at `zcu10[2|4]_[es2_]rv_ss/sw/petalinux_bsp`. The hdf file exported from the corresponding Vivado project is available in the `project-spec/hw-description/` subfolder inside the PetaLinux BSP.

To configure and build the PetaLinux BSP, run the following commands:

```
% cd petalinux
% petalinux-create -t project -s zcu102-prod-rv-ss.bsp -n bsp
% petalinux-config --get-hw-description=../zcu102_base_trd/hw --oldconfig
% petalinux-build
```

**:pushpin: NOTE** The tmp directory might relocated to a different folder especially if your petalinux project is located on a NFS mount. Please check your petalinux configuration.

The generated output products are located inside the `images/linux/` subfolder. The relevant files that are packaged as part of the platform are
* bl31.elf
* pmufw.elf
* u-boot.elf
* zynqmp_fsbl.elf
* image.ub

To generate the SDK/sysroot run the following command:

```
% petalinux-build -s
```

The generated SDK installer will be located at `images/linux/sdk.sh`.

## 8.3 Video Command Line Utility

The Xilinx `video_cmd` utility is used to initialize the media pipeline of an associated V4L2 capture device. A prebuilt version of this utility is available at `zcu10[2|4]_[es2_]rv_ss/sw/a53_linux/a53_linux/image/video_cmd` and will be automatically placed in the `sd_card` folder of the generated SDx project.

The `video_cmd`, `video_lib`, and `gst_lib` sources are provided as XSDK projects and are located at `zcu10[2|4]_[es2_]rv_ss/workspaces/ws_video`. Perform the following steps to build the application using the SDx GUI:

1. Make sure the `SYSROOT` environment variable is set correctly before starting SDx (see design example tutorials for details).
2. Start SDx and select the `zcu10[2|4]_[es2_]rv_ss/workspaces/ws_video` directory as your workspace.
3. From the SDx menu bar, select 'File -> Import -> General -> Existing Projects into Workspace'. Click 'Next'.
4. In the 'Import Project' dialog, browse to the workspace root directory at `zcu102_[es2_]rv_ss/workspaces/ws_video`. Make sure the `gst_lib`, `video_lib`, and `video_cmd` projects are checked and click 'Finish'.
5. Right-click the newly added `video_cmd` project in the 'Project Explorer' and select 'Build Project'. The `video_cmd` output product will be placed inside the `Debug` or `Release` subfolder depending on the chosen build configuration.

<hr/>

:arrow_forward:**Next Topic:**  [9. Known Issues and Limitations](known-issues-limitations.md)

:arrow_backward:**Previous Topic:**  [7. Run the Application](run-application.md)
<hr/>
<p align="center"><sup>Copyright&copy; 2018 Xilinx</sup></p>
