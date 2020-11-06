# TP-Link and Router Help - Anything you do below or on your own you assume the risk. If you have any questions please be sure to reach out to the TP-Link experts before proceeding!

**NOTE:** If any of the links below do not work I placed the files [HERE](https://github.com/samadril/tech-help/tree/main/tplink/files) In the files folder in this repository.

## Back to old Firmware

### Get `DEBUG` firmware loaded onto your router
- 1. Contact TP-Link Support to get and download a `DEBUG` version of the current or newer firmware then that you are currently running.
  - Current `DEBUG` firmware download link `V1.1.1 P8`  [HERE](https://static.tp-link.com/2020/202010/20201019/ax11000v1-up-ver1-1-1-P8[20201018-rel85979]_beta_2020-10-19_12.57.49.zip)
- 2. Download the `DEBUG` firmware from the link provided in step 1.
- 3. If you just want to get to the OLDER BETA code that did not have issues you can continue on to the next section [Once on the `DEBUG` firmware, edit the `/etc/partition_config/soft-version` file](#once-on-the-debug-firmware-edit-the-etcpartition_configsoft-version-file)
- 4. ***(OPTIONAL FOR FIXING ISSUE)*** Once the `DEBUG` firmware has been downloaded and just prior to installing the `DEBUG` firmware, connect a USB flash drive into the router that has been formatted `FAT32`. <BR> The debug firmware will collect debug logs through the USB Sharing function, it will automatically save the debug log into USB disk which is connected to AX11000. Connecting  the formatted USB to the USB port of AX11000, will automatically record the debug logs. There is no special settings required other then just plugging it in and waiting for the issue to reoccur.<BR>**ATTENTION:** There is no need to enable the USB sharing function. You just need to plug your USB drive. The debug logs are saved in the tplink_log directory. It is recommended to insert the USB flash drive before upgrading the debug firmware to ensure that we can collect the complete debug log.
- 4. Now that you have the `DEBUG` firmware and; if you chose, a USB has been connected, update the `DEBUG` firmware. <BR> If you need help you can get more details about how to update firmware manually from below FAQ:
https://www.tp-link.com/support/faq/2139/
- 5. ***(OPTIONAL FOR FIXING ISSUE)*** Once you are able to reproduce the problem using the above debug firmware, please collect the debug info as the following instruction.
  - Send the tplink_log via email so they can help solve the issue using that log. If the log file is too large work with support on a way to send them the file. One suggestion is that you can send it through Google Drive. Or you can contact support so they can collect log files by remote assistance.

### Once on the `DEBUG` firmware, edit the `/etc/partition_config/soft-version` file
**NOTE:** This is strictly information and meant to help someone with an issue on there current firmware release, This procedure has the potential to brick your router. If you do not understand what you are doing after reading through this procedure, do not attempt without help from TPLink.

- Download the OLDER official firmware from URL:  https://static.tp-link.com/2020/202003/20200312/Archer%20AX11000(US)_V1_200216.zip
- Before continuing with any of the steps below be sure you Update to the most current [debug firmware](https://static.tp-link.com/2020/202010/20201019/ax11000v1-up-ver1-1-1-P8[20201018-rel85979]_beta_2020-10-19_12.57.49.zip) first. This is completed in the first section [`Get `DEBUG` firmware loaded onto your router`](#get-debug-firmware-loaded-onto-your-router)
- Once upgrade completes, and router reboots, reconnect via ethernet cable. (You can do over wifi but not recommended)
- Make sure you have software that will allow you to Telnet
  - An option for Windows users
  - In windows search box, type "Windows features"
  - Click the top box to "Turn windows features on or off"
  - Scroll down to Telnet service, and check the box.
  - Windows will activate telnet
  - In windows search box, type CMD, and click on CMD app to bring up a command prompt
- Telnet to the router DNS Name or IP address using the telnet tool of preference. **Note:** I like Putty!
  - If using Windows telnet feature, In the command prompt screen, type: "telnet tplinkwifi.net" OR "telnet 192.168.*.*" (<- IP address of your Archer AX6000 router)
  - If using putty, click on the `telnet` radio button, enter the IP address of the router, and click the `OPEN` button.
- Once in you will see the following screen

```
BusyBox v1.19.4 (2020-10-17 00:35:37 EDT) built-in shell (ash)
Enter 'help' for a list of built-in commands.

     MM           NM                    MMMMMMM          M       M
   $MMMMM        MMMMM                MMMMMMMMMMM      MMM     MMM
  MMMMMMMM     MM MMMMM.              MMMMM:MMMMMM:   MMMM   MMMMM
MMMM= MMMMMM  MMM   MMMM       MMMMM   MMMM  MMMMMM   MMMM  MMMMM'
MMMM=  MMMMM MMMM    MM       MMMMM    MMMM    MMMM   MMMMNMMMMM
MMMM=   MMMM  MMMMM          MMMMM     MMMM    MMMM   MMMMMMMM
MMMM=   MMMM   MMMMMM       MMMMM      MMMM    MMMM   MMMMMMMMM
MMMM=   MMMM     MMMMM,    NMMMMMMMM   MMMM    MMMM   MMMMMMMMMMM
MMMM=   MMMM      MMMMMM   MMMMMMMM    MMMM    MMMM   MMMM  MMMMMM
MMMM=   MMMM   MM    MMMM    MMMM      MMMM    MMMM   MMMM    MMMM
MMMM$ ,MMMMM  MMMMM  MMMM    MMM       MMMM   MMMMM   MMMM    MMMM
  MMMMMMM:      MMMMMMM     M         MMMMMMMMMMMM  MMMMMMM MMMMMMM
    MMMMMM       MMMMN     M           MMMMMMMMM      MMMM    MMMM
     MMMM          M                    MMMMMMM        M       M
       M
 ---------------------------------------------------------------
   For those about to rock... (Attitude Adjustment, unknown)
 ---------------------------------------------------------------
root@AX11000:/#

```

- Type the following command to edit and make the required change:
  - "vi /etc/partition_config/soft-version"
- You will see the version info on the top of a screen similar to this.

```
soft_ver:1.1.1 Build 20201018 rel.85979
fw_id:2329298F0C44D86F9DF8CB60E01FD32D
cfg_ver:AX11000V1.0.0P1
~
~
~
/etc/partition_config/soft-version 1/3 33%
```

- While in the vi interface. Hit the <insert> key or Type letter "i" to allow you to enter edit mode
in order to make a change to the file.
- Using the arrow keys, navigate on the screen and Change `soft_ver:1.1.1` to `soft_ver:1.0.1`<BR>Note: This may change based on the original code version you are using. In this case I am using `Archer AX11000(US)_V1_200216` which can be found [HERE](https://static.tp-link.com/2020/202003/20200312/Archer%20AX11000(US)_V1_200216.zip)
- Once you are sure you have made this change right and it looks like what you see below, Hit escape (it will not seem like it did anything, but it exited the edit mode).<BR>

**BEFORE**<BR>
```
soft_ver:1.1.1 Build 20201018 rel.85979
fw_id:2329298F0C44D86F9DF8CB60E01FD32D
cfg_ver:AX11000V1.0.0P1
```

**AFTER**<BR>
```
soft_ver:1.0.1 Build 20201018 rel.85979
fw_id:2329298F0C44D86F9DF8CB60E01FD32D
cfg_ver:AX11000V1.0.0P1
```

- Type ":wq" to save & exit.  
- Finally type `cat /etc/partition_config/soft-version` as a final step to verify the change.
```
root@AX11000:/# cat /etc/partition_config/soft-version
soft_ver:1.0.1 Build 20201018 rel.85979
fw_id:2329298F0C44D86F9DF8CB60E01FD32D
cfg_ver:AX11000V1.0.0P1
```

- you can now exit telnet.
- With this change complete you can now log back into your router using `tplinkwifi.net` or the `IP address`
- With the change in the file you are now able to upgrade to the `1.0.7` or other older version of firmware that you downloaded or get from support.
- Proceed with the Upgrade (Which is really a downgrade) to the `1.0.7` or other older version of firmware that you downloaded or get from support.
- Restart the Router
- Verify the Router is now on the older version of Firmware
- If there is a Beta version, of that version you want to go to, you will now be able to upgrade to that beta version.

## File Links

- [Older Official Firmware](https://static.tp-link.com/2020/202003/20200312/Archer%20AX11000(US)_V1_200216.zip)
- [V1.0.7 P1](https://static.tp-link.com/2020/202003/20200317/ax11000v1-up-ver1-0-7-P1[20200311-rel7814]_sign_2020-03-11_14.42.54.zip) - Beta version of `1.0.7 P1`
- [DEBUG V1.1.1 P8](https://static.tp-link.com/2020/202010/20201019/ax11000v1-up-ver1-1-1-P8[20201018-rel85979]_beta_2020-10-19_12.57.49.zip)
- ALL of these files can also be found [HERE](https://github.com/samadril/tech-help/tree/main/tplink/files) in this repository.
