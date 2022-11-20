# 2022-2023 member "cyber security" computer environment

All 2022-2023 members, including probationary members, should be comfortable using sandboxed windows, linux, and android environments. Use httptoolkit and wireshark to view the traffic within these environments. 
{{< hint warning >}}
**RAM requirement**

Your host computer should have 16GB of RAM, or ideally 32GB.
{{< /hint >}}

{{< hint danger >}}
**x86_64 required**

This environment will not work on Apple m1 CPUs
{{< /hint >}}



## 1. Windows and Ubuntu virtual machines

Download and install VirtualBox. Try installing both Windows and Ubuntu virtual machines.

{{< hint info >}}
Microsoft offers [free Windows machines](https://developer.microsoft.com/en-us/windows/downloads/virtual-machines/), although you may choose to install from your own iso.

Please use Ubuntu Desktop 22.04
{{< /hint >}}


## 2. Docker Android Packet Inspection 
### Android Emulator 

Please install docker-compose and scrcpy, then start the example docker-compose.yml below and view it.

```bash
sudo apt install docker-compose scrcpy
# accept and continue

# create a folder called "my-android" in your home directory "~":
mkdir ~/my-android
# enter the directory
cd ~/my-android
# paste the docker-compose.yml and save it:
gedit docker-compose.yml
# start the emulator:
sudo docker-compose up -d
# connect to the emulator
scrcpy -s localhost:5555
```


{{< expand "Android emulator's docker-compose.yml" "..." >}}
## docker-compose.yml
```yml
# Note: It requires docker-compose version 1.13.0 or more.
#
# Usage: docker-compose up -d
version: "2.2"

services:
  # Selenium hub
  selenium_hub:
    image: ${DOCKER_REGISTRY}selenium/hub:3.14.0-curium
    ports:
      - 4444:4444

  appium_server:
    image: appium/appium
    depends_on:
      - selenium_hub
    network_mode: "service:selenium_hub"
    privileged: true
    volumes:
      - /dev/bus/usb:/dev/bus/usb
      - ~/.android:/root/.android
      - $PWD/example/sample_apk:/root/tmp
    environment:
      - CONNECT_TO_GRID=true
      - SELENIUM_HOST=selenium_hub
      - RELAXED_SECURITY=true


  nexus_emulator:
    image: ${DOCKER_REGISTRY}budtmo/docker-android-x86-12.0
    privileged: true
    scale: 1
    depends_on:
      - selenium_hub
      - appium_server
    ports:
      - 6080:6080
      - 4723:4723
      - 5554:5554
      - 5555:5555
    volumes:
      - $PWD/example/sample_apk:/root/tmp/sample_apk
      - ./video-nexus_7.1.1:/tmp/video
    environment:
      - DEVICE=Nexus 5
      - CONNECT_TO_GRID=true
      - APPIUM=true
      - SELENIUM_HOST=selenium_hub
      - AUTO_RECORD=true
      - EMULATOR_ARGS=-memory 8192 -partition-size 8096

```
{{< /expand >}}

![](https://www.omgubuntu.co.uk/wp-content/uploads/2020/05/scrcpy-screenshot.jpg)

### HTTP Toolkit

[Install](https://httptoolkit.com/docs/getting-started/installing/) HTTP Toolkit and [connect to android using adb](https://httptoolkit.com/docs/guides/android/). 

![](https://httptoolkit.com/screenshot.png)

## 3. WireShark

Install WireShark on your guest virtual machines, and test it.

## 4. Windows Android Studio

1. [Download Android Studio](https://developer.android.com/studio). 

2. After starting, click "More Actions" and choose "Virtual Device Manager". Create a device, then choose Pixel 6 Pro -> Tiramisu -> Finish.

	If you receive an error saying you could not download intel haxm, it may be because intel vt-x is not enabled. [Click here for how to enable intel vt-x](https://www.howtogeek.com/213795/how-to-enable-intel-vt-x-in-your-computers-bios-or-uefi-firmware/)

3. Start the device, then enable developer setting and USB connectivity by going to the android Settings -> About Emulated Device -> Build Number, click this 5 times or until it says you are a developer

![](https://tinypic.host/images/2022/11/19/AndroidPixel6inSettings.png)

4. If you have installed HTTP Toolkit, you should now be able to connect via ADB.





