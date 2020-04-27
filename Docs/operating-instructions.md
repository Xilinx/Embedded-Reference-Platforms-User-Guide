<p align="right">
            Read this page in other languages:<a href="../docs-jp/Docs/operating-instructions.md">日本語</a>    <table style="width:100%"><table style="width:100%">
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
    <td width="17%" align="center">5. Installation and Operating Instructions</td>
    <td width="16%" align="center"><a href="tool-flow-tutorials.md">6. Tool Flow Tutorials</a></td>
    <td width="17%" align="center"><a href="run-application.md">7. Run the Application</a></td>
    <td width="17%" align="center"><a href="platform-details.md">8. Platform Details</a></td>    
  </tr>
<tr>
    <td width="17%" align="center" colspan="2"><a href="known-issues-limitations.md">9. Known Issues and Limitations</a></td>
    <td width="16%" align="center" colspan="2"><a href="additional-references.md">10. Additional References</a></td>
</tr>
</table>

# 5. Installation and Operating Instructions

## 5.1. Board Setup

- [5.1.1. Single Sensor Setup](#511-single-sensor-setup)
- [5.1.2. 8-Stream VCU + CNN Setup](#512-8-stream-vcu--cnn-setup)
- [5.1.3. ZCU104 Smart Camera Setup](#513-zcu104-smart-camera-setup)

### 5.1.1. Single Sensor Setup

##### 5.1.1.1. Required Actions
* Connect the power supply to the 12V power connector.
* Display options:
  * Connect a DisplayPort cable to DisplayPort connector on the board; connect the other end to a monitor, _or_
  * Connect an HDMI cable to the HDMI output (*top* HDMI connector) on the board; connect the other end to a monitor.

**:warning: WARNING** Make sure you only connect _either_ the DisplayPort _or_ the HDMI output to the board, not both. Otherwise, the design might malfunction.

**:pushpin: NOTE** Certain monitors have multiple HDMI ports supporting different HDMI standards. Make sure you choose an HDMI 2.0 capable port (if available) for 4k60 performance.

* Connect the Micro USB cable to the USB-UART connector; use the following settings for the terminal emulator:
  * Baud Rate: 115200
  * Data: 8 bit
  * Parity: None
  * Stop: 1 bit
  * Flow Control: None

* Insert an SD card (FAT formatted) with pre-built images copied from one of the following directories:
  * `sd_card/optical_flow`
  * `sd_card/stereo`
  * `sd_card/filter2d`

##### 5.1.1.2. Optional Actions
* Connect an HDMI cable to the HDMI input (_bottom_ HDMI connector) on the board; connect the other end to an HDMI source.
* Connect the See3CAM_CU30 or ZED USB camera to the USB3 Micro AB connector using the Xilinx USB3 Micro B adapter.

  **:pushpin: NOTE** VADJ needs to be set to **1.2V** for the correct operation of the daughter card. If the FMC card does not function, please follow the instructions explained in Answer Record [AR67308](https://www.xilinx.com/support/answers/67308.html) for rev 1.0 and beyond to check and/or set VADJ.

#### 5.1.1.3. ZCU104 Jumpers & Switches
* Set the boot mode to the SD card:
  * SW6[4:1]: **off, off, off, on**

  ![](images/zcu104_board_setup_2017.4.jpg)

### 5.1.2. 8-Stream VCU + CNN Setup

#### 5.1.2.1. Required Actions

* Connect the power supply to the 12V power connector.
* For the display, connect an HDMI cable to the HDMI output (_top_ HDMI connector) on the board; connect the other end to a monitor.
* Connect the micro USB cable to the USB-UART connector; use the following settings for the terminal emulator:
  * Baud Rate: 115200
  * Data: 8 bit
  * Parity: None
  * Stop: 1 bit
  * Flow Control: None
* Server-side setup (Windows 10 laptop):
  * Firewall and Ethernet settings:
    * Disable the antivirus software firewall if it is installed in your Windows PC. For examples, with McAfee, the steps to disable the firewall are as follows: **Notification Area**  →  **McAfee**  →  **Quick Settings**  →  **Disable Endpoint Security Firewall**.

   ![](images/scout_5_firewall.png)

    * Set up the IP address in the Ethernet network area. Go to **Control Panel** → **Network & Internet** → **Network & Sharing Center**. Click on **Change Adapter Settings** and open **Ethernet Properties**. Configure the settings as shown below.

   ![](images/scout_5_ethernet.png)

* Host eight RTSP servers in the Windows 10 laptop by launching eight VLC instances using the below syntax:

            `vlc.exe --loop <input_h264_stream.mp4> :sout=#duplicate{dst=display,dst="gather:rtp{sdp=rtsp://<IP>:<port>/<stream_name>}"} :network-caching=1500 :sout-all :sout`

    *  Example procedure:
          * Copy the ``test_videos`` folder from ``sdcard`` to the C: directory of the Windows 10 laptop.
          * Open the ``cmd`` window on the Windows 10 laptop.
          * Go to the VLC installed folder, and enter the following commands:

![](images/scout_5_cmd_vlc.png)

                      ```
                      vlc.exe --loop C:\test_videos\face_15fps.mp4 :sout=#duplicate{dst=display,dst="gather:rtp{sdp=rtsp://192.168.1.99:8554/face}"} :network-caching=1500 :sout-all :sout-keep
                      vlc.exe --loop C:\test_videos\face_15fps.mp4 :sout=#duplicate{dst=display,dst="gather:rtp{sdp=rtsp://192.168.1.99:8556/face}"} :network-caching=1500 :sout-all :sout-keep
                      vlc.exe --loop C:\test_videos\face_15fps.mp4 :sout=#duplicate{dst=display,dst="gather:rtp{sdp=rtsp://192.168.1.99:8558/face}"} :network-caching=1500 :sout-all :sout-keep
                      vlc.exe --loop C:\test_videos\face_15fps.mp4 :sout=#duplicate{dst=display,dst="gather:rtp{sdp=rtsp://192.168.1.99:8560/face}"} :network-caching=1500 :sout-all :sout-keep

                      vlc.exe --loop C:\test_videos\traffic4.mp4 :sout=#duplicate{dst=display,dst="gather:rtp{sdp=rtsp://192.168.1.99:8564/traffic}"} :network-caching=1500 :sout-all :sout-keep
                      vlc.exe --loop C:\test_videos\traffic4.mp4 :sout=#duplicate{dst=display,dst="gather:rtp{sdp=rtsp://192.168.1.99:8566/traffic}"} :network-caching=1500 :sout-all :sout-keep
                      vlc.exe --loop C:\test_videos\traffic4.mp4 :sout=#duplicate{dst=display,dst="gather:rtp{sdp=rtsp://192.168.1.99:8568/traffic}"} :network-caching=1500 :sout-all :sout-keep
                      vlc.exe --loop C:\test_videos\traffic4.mp4 :sout=#duplicate{dst=display,dst="gather:rtp{sdp=rtsp://192.168.1.99:8570/traffic}"} :network-caching=1500 :sout-all :sout-keep

                      ```
              *  Recommended parameters:
                  * MP4 file with H264 1080p@11fps.
                  * Host each RTSP stream on one of the even-numbered ports of an IP (that is, use ports 8554, 8556, 8558, 8560, and so on).

* If IP cameras are being used, start all four IP cameras and get corresponding RTSP URLs to connect using RTSP clients:
  * Example IP camera RTSP URL: rtsp://admin:xilinx1234@192.168.1.99/profile2/media.smp
  * Recommended RTSP stream parameters:
                        Resolution: 1080p
                        Video codec: H264
                        Framerate: 15fps

* For the client-side (ZCU104 board) setup, open the ``inputs.conf`` file and update the RTSP URLs prepared on the server, as shown in the following example:

            ```
            [urls]
            faceurl_1=rtsp://192.168.1.99:8554/face
            faceurl_2=rtsp://192.168.1.99:8556/face
            faceurl_3=rtsp://192.168.1.99:8558/face
            faceurl_4=rtsp://192.168.1.99:8560/face
            trafficurl_1=rtsp://192.168.1.99:8564/traffic
            trafficurl_2=rtsp://192.168.1.99:8566/traffic
            trafficurl_3=rtsp://192.168.1.99:8568/traffic
            trafficurl_4=rtsp://192.168.1.99:8570/traffic
            ```
* For the server-client connection setup, connect the server and client through Ethernet cables as shown below.

![](images/scout_5_ethernet_connections.png)

* Insert an SD card (FAT formatted) with pre-built images copied from the `sdcard` directories.

#### 5.1.2.3. ZCU104 Jumpers and Switches

* Set the boot mode to the SD card:
  * SW6[4:1]: **off, off, off, on**

  ![](images/vcu_8stream_cnn.jpg)

### 5.1.3. ZCU104 Smart Camera Setup

#### 5.1.2.1. Required Actions
* Connect the power supply to the 12V power connector.
* For the display, connect a DisplayPort cable to the DisplayPort output on the board; connect the other end to a monitor.
* Connect the micro USB cable to the USB-UART connector; use the following settings for the terminal emulator:
  * Baud Rate: 115200
  * Data: 8 bit
  * Parity: None
  * Stop: 1 bit
  * Flow Control: None
* Connect a LAN cable to the Ethernet port (marked as Ethernet port) on the ZCU104 board.
* Insert an SD card (FAT formatted) with pre-built images from the `sd_card` directories.

#### 5.1.2.2. ZCU104 Jumpers and Switches
* Set the boot mode to the SD card:
  * SW6[4:1]: **off, off, off, on**

  ![](images/zcu104_smartcamera_board_setup.jpg)

## 5.2. Extracting the Design Files

Download and unzip the reference design .zip file matching your silicon version (see [Software](software-tools-system-requirements.md#32-software)).
* For Linux, use the `unzip` utility.
* For Windows, make sure that the reference design .zip file is unzipped in a directory path which contains no spaces. Use the 7zip utility and follow the steps below. You can download 7zip [here](http://www.7-zip.org/).


**:pushpin: NOTE** When prompted to confirm the file replace, select **Auto Rename** (Windows only).

  ![](images/7zip-1.jpg)
<hr/>

:arrow_forward:**Next Topic:**  [6. Tool Flow Tutorials](tool-flow-tutorials.md)

:arrow_backward:**Previous Topic:**  [4. Design File Hierarchy](design-file-hierarchy.md)
<hr/>
<p align="center"><sup>Copyright&copy; 2018–2019 Xilinx</sup></p>
