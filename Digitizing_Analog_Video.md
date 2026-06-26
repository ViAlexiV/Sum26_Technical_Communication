[Digitizing_Analog_Video.md](https://github.com/user-attachments/files/29392946/Digitizing_Analog_Video.md)
# Guide to Digitizing Analog Video from a Camcorder to a PC

## Introduction

This guide describes the process of converting an analog video signal into a digital format. The instructions cover the entire digitization lifecycle: from hardware setup and cabling to software configuration. The reference equipment used in this guide includes a Sony CCD-TR730E analog camcorder, an AV-to-HDMI converter, and a Razer Ripsaw HD capture card.

**Target Audience:** Users who want to transfer archive video recordings from magnetic tapes to a computer hard drive for long-term storage and editing.

## 1\. Hardware and Software Requirements

### 1.1. Hardware

* **Analog signal source:** Camcorder (e.g., Sony CCD-TR730E) or VCR.
* **Analog-to-digital converter (ADC):** Best way here is using Retro tink upscaler, but for more budget-friendly way exists RCA composite to HDMI converter.
* **Video capture card:** A capture device with an HDMI interface, or better direct AV interface (Razer Ripsaw HD).
* **Cables:**

  * Composite RCA cable (Yellow/White/Red plugs) — 1 pc.
  * HDMI cable — 2 pcs.
  * USB 3.0 cable (Type-C to Type-A) to connect the capture card to the PC.
* **PC:** A computer running Windows/Linux/mac with an available USB 3.0 port.

### 1.2. Software

* **OBS Studio** (version 29.0 or newer is recommended).
* **Hardware Drivers:** (Optionally if needed) capture card drivers.

## 2\. Hardware Setup

Follow the steps below to assemble the hardware chain. Connect all devices while the main power is turned off to prevent static discharge.

1. Connect the composite RCA cable to the analog output of the camcorder. Strictly observe the color coding: the yellow plug is for video, the white plug is for the left audio channel, and the red plug is for the right audio channel.
2. Connect the opposite end of the composite cable to the **Input** ports of the AV-to-HDMI converter.
3. Connect the power cable to the AV-to-HDMI converter. Typically, a mini-USB or micro-USB cable connected to an external power supply (5V) is used.
4. Connect the **Output** of the AV-to-HDMI converter to the **HDMI In** port of the capture card using the first HDMI cable.
5. Connect the Razer Ripsaw HD capture card to the PC using the USB 3.0 cable. Use a port directly on the motherboard.
6. Turn on the camcorder and switch it to playback mode (VCR/Play/Player).

> \*\*Warning:\*\* Ensure the resolution switch on the AV-to-HDMI converter is set to PAL or NTSC depending on your Camcoder region. The analog signal has a low native resolution (576i); the converter performs hardware upscaling.

## 3\. OBS Studio Configuration

Configure the scene and sources to capture video and audio properly in OBS Studio.

### 3.1. Adding a Video Source

1. Launch OBS Studio.
2. In the **Sources** panel, click the **+** (Add) button and select **Video Capture Device**.
3. Enter a descriptive name for the source (e.g., `Razer Ripsaw`) and click **OK**.
4. In the properties window, select **Razer Ripsaw HD HDMI** from the **Device** drop-down list.
5. Set the **Resolution/FPS Type** parameter to **Custom**.
6. In the **Resolution** field, select `1280x720`50HZ.
7. Click **OK**.

### 3.2. Configuring Deinterlacing

Analog video contains interlacing (a "comb" effect during fast motion), which you must eliminate via software for comfortable viewing on modern progressive-scan monitors.

1. Right-click the added video source in the **Sources** panel.
2. Select **Deinterlacing** -> **Yadif 2x**.
3. Set the field order to **Top Field First**.

### 3.3. Configuring Audio Capture

1. In the **Sources** panel, click the **+** button and select **Audio Input Capture**.
2. Select the **Razer Ripsaw HD** device and click **OK**.
3. In the **Audio Mixer** panel, click the gear icon next to the added audio source.
4. Select **Advanced Audio Properties**.
5. In the **Audio Monitoring** column, set the value to **Monitor and Output**. This setting allows you to hear the audio from the tape through your PC speakers during digitization and records it to the final file simultaneously.

## 4\. Digitization Process

1. Go to **File** -> **Settings** -> **Output**.
2. In the **Recording** section, specify the destination path to save the files.
3. Select the recording format. `MKV` is highly recommended because it prevents file corruption if the recording is unexpectedly interrupted. You can remux it to `MP4` later.
4. Set the Video Bitrate to `5000 Kbps` to `8000 Kbps`. This provides sufficient quality for an upscaled standard-definition signal. Click **OK** to save the settings.
5. Click the **Start Recording** button in the main OBS Studio window.
6. Press the **Play** button on the camcorder.
7. After the tape finishes playing, click **Stop Recording**. The file will be saved in the specified directory.

## 5\. Troubleshooting

|Problem|Possible Cause|Solution|
|-|-|-|
|**Black screen in the OBS preview window**|No signal from the converter or camcorder.|Check the AV-to-HDMI converter power supply. Ensure the camera is switched to playback mode (VCR), not recording mode (Camera). Check Windows Privacy settings to ensure desktop apps have access to cameras.|
|**The image "jitters" or shows horizontal lines**|Deinterlacing is disabled or configured incorrectly.|Apply a deinterlacing filter to the source in OBS (see section 3.2). Try changing the field order to "Bottom Field First".|
|**Audio lags behind the video**|USB audio processing latency.|Open "Advanced Audio Properties" in OBS. In the "Sync Offset" column for the audio source, set a positive value between `100 ms` and `300 ms` (adjust empirically until synchronized).|
|**The image is in black and white**|Incorrect video signal standard (PAL/NTSC).|Open the video capture device properties in OBS and manually specify the video signal standard corresponding to your camera (for Europe and CIS, this is usually PAL).|



