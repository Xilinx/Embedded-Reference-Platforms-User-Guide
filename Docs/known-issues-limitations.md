<p align="right">
            Read this page in other languages:<a href="../docs-jp/Docs/known-issues-limitations.md">日本語</a>    <table style="width:100%"><table style="width:100%">
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
    <td width="17%" align="center"><a href="platform-details.md">8. Platform Details</a></td>    
  </tr>
<tr>
    <td width="17%" align="center" colspan="2">9. Known Issues and Limitations</td>
    <td width="16%" align="center" colspan="2"><a href="additional-references.md">10. Additional References</a></td>
</tr>
</table>

# 9. Known Issues and Limitations

## 9.1. Known Issues

* The following error message is shown when compiling the SDx project:

  `WARNING: [DMAnalysis 83-4492] Unable to determine the memory attributes passed to _mapx_mat.data of function w1_xf_remap at /home/workspaces/ws_sv/stereo/src/stereo_sds.cpp:257, please use mem_attribute pragma to specify`

  **Solution:** The message is benign and can be ignored.

* The following error message is shown while booting the Single Sensor platforms on the board:

  `waiting for X server to begin accepting connections Xorg: ../../xorg-server-1.20.1/include/privates.h:121: 	dixGetPrivateAddr: Assertion key->initialized' failed.`

  **Solution:** The message is benign and can be ignored. See [AR 72363](http://xkb/Pages/72/72363.aspx).

* The following error message is shown while booting the Single Sensor platforms on the board:

    `drm_atomic_helper_wait_for_vblanks.part.9+0x270/0x288.`

  **Solution:** The message is benign and can be ignored.

## 9.2. Limitations

* Do not connect a DisplayPort cable and an HDMI TX at the same time.
* Make sure the DisplayPort or HDMI TX cable is plugged in when you power on the board.
* DP-to-HDMI adapters are not supported. See [AR 67462](https://www.xilinx.com/support/answers/67462.html).
* An HDMI RX does _not_ support the following:
  * YUV 4:2:0 input.
  * HDCP encrypted input.
  * Hotplug or dynamic resolution changes while the application is running.
* The provided image signal processor (ISP) pipeline does not include any auto algorithms. The IMX274, gamma, and color correction controls have to be adjusted manually based on the surrounding environment.
* The `optical_flow` live I/O sample does not have a software implementation of the algorithm; only the hardware optimized implementation is available.
* The Single Sensor platform with See3cam is supported only for pass through mode. Both pass through and stereo filter can be tested using the stereo ZED camera.
* The 8-stream VCU + CNN platform demo is tested with the provided input files only. With different input files (that is, with different encoding rates, file resolution/quality, and number of streams), the results might be different.
* In the Regulus ISP version of the ZCU104 Smart Camera platform, Regulus ISP is configured to operate only for 30 minutes. When the 30 minute timer expires, the board must be restarted.
* For the ZCU104 Smart Camera platform, the latency of the RTSP stream when viewed on the VLC player is approximately two seconds due to the software decoding in the player. If the RTSP stream is decoded using the ZCU104 8-stream VCU + CNN platform, the latency reduces to approximately 650 milliseconds because of the integrated VCU decoder.
* A full understanding of the system is required for effective usage.

<hr/>

:arrow_forward:**Next Topic:**  [10. Additional References](additional-references.md)

:arrow_backward:**Previous Topic:**  [8. Platform Details](platform-details.md)
<hr/>
<p align="center"><sup>Copyright&copy; 2018–2019 Xilinx</sup></p>
