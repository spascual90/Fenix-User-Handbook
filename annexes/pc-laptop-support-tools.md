# PC/Laptop Support Tools

## Putty

PuTTY is a free (MIT-licensed) Windows Telnet client to communicate with Fenix Autopilot.

{% file src="../.gitbook/assets/putty.zip" %}
Download PuTTY: latest release (0.74)
{% endfile %}

### Configuration parameters in Putty

* Session
  * Serial line: COM#
  * Speed: 9600
  * Connection type: Serial
* Terminal
  *
    * [x] Implicit CR in every LF
    * [x] Implicit LF in every CR
  * Local echo: Force on
  * Local line editing: Force on
* Window
  * Selection
    * Auto-copy selected text to system clipboard
      * Mouse paste action: System clipboard
* Connection
  * Serial
    * Serial line to connect to: COM#
    * Speed: 9600
    * Data bits: 8
    * Stop bits: 1
    * Parity: None
    * Flow control: RTS/CTS

{% hint style="info" %}
\# is the COM port number where Autopilot is connected. If you don't know the value, try numbers sequencialy starting from 1.
{% endhint %}

{% hint style="info" %}
It is recommended to Save Session to ease recovery of settings at the begining of each session.
{% endhint %}

## How to save the Serial I/F backlog

Move the cursor to the upper-left corner of PuTTY and left-click.

Select "Copy All to Clipboard".

![](<../.gitbook/assets/Sending serial.png>)

Open Notepad and paste the Clipboard to a txt file.

## Autopilot SW Uploader

Microsoft Windows Tool for flashing Fenix SW (HEX file) to  Fenix autopilot (Arduino).&#x20;

{% file src="../.gitbook/assets/xloader-v1.00[1].zip" %}
Download xloader-v1.00 Tool for flashing Fenix SW (HEX file)
{% endfile %}

### Configuration Parameters in XLoader

* Hex file: Select HEX file from your file system
* Device: Mega (ATMEGA2560)
* COM port: COM#
* Baud rate: 11520

{% hint style="info" %}
\# is the COM port number where Autopilot is connected. If you don't know the value, try numbers sequencialy starting from 1.
{% endhint %}

###

### Flashing Steps

1. Download [xLoader.zip](https://github.com/xinabox/xLoader/releases/latest) file.
2. Unzip the `xLoader.zip` file
3. Insert Fenix USB cable into an available USB port
4. Wait for eventual drivers to be installed, if driver installation fail, goto [USB Driver](https://github.com/xinabox/xLoader#usb-driver)
5. Execute the `xLoader.exe` file
6. Select Configuration Parameters.
7. Choose your COM port. If no COM port is available, goto [USB Driver](https://github.com/xinabox/xLoader#usb-driver)
8. Click `Upload`
9. Wait for the text `Uploading...` to be replaced by `<nnnn> bytes uploaded`
10. Unplug USB cable.
