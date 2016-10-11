Pre requisites for Running the Azure IOTHub SDK on a RaspberryPI. 
This project runs on Python.

The following information on how to set up your RasPi to run Python Code and connect to the Azure IoT Hub via SDK was gotten from: http://iottopic.com/azure-iot-hub-raspberry-pi-3/
The Author of the post is Chris Den Arden.
This is the ONLY guide I got working on my Raspberry Pi 3 and my Raspberry Pi 2 running the lastest version of Jessie.

Setting up your Pi:

1) Write raspbian Jessie on sd card https://www.raspberrypi.org/documentation/installation/installing-images/README.md
2) Connect your raspberry to a screen and move on with step 3. Or work headless and move on to step 2.1.
  2.1) Share your internet connection
  2.2) Connect your raspberry with your PC with a UTP cable
  2.3) Find your raspberry IP with arp -a in cmd
  2.4) Connect to you raspberry with ssh, default credentials u:pi p:raspberry (I use WinSCP and Putty)
3) Update stuff sudo apt-get update
4) Upgrade stuff sudo apt-get upgrade
Configure wifi (or keep using the UTP cable and move on to step 6), navigate to network config sudo nano /etc/wpa_supplicant/wpa_supplicant.conf
Enter settings at bottom of file, after connected to wifi you can find the ip address on the router network={ ssid=”ssid” psk=”password” }
 

Followed this instruction: https://github.com/Azure/azure-iot-sdks/blob/master/c/doc/devbox_setup.md

Install cmake sudo apt-get install cmake
Clone repo git clone –recursive https://github.com/Azure/azure-iot-sdks.git
Run script sudo ./setup.sh in c/build_all/linux
Run script sudo ./build.sh in c/build_all/linux
ERROR: first time error missing CMakeLists.txt in a subdirectory.

Solution: Removed azure-iot-sdks directory, cloned again and run setup and build with sudo. Worked. So maybe it was because of the sudo, maybe the first clone was not completed (submodules stuff).

 

Followed this instruction: https://github.com/Azure/azure-iot-sdks/blob/master/doc/get_started/python-devbox-setup.md

Run script sudo ./setup.sh in python/build_all/linux
Run script sudo ./build.sh in python/build_all/linux
Find iothub_client in python/device/samples
ERROR: after 100% costs a lot of time, ends with some makefile recipe error.

Solution: https://www.bitpi.co/2015/02/11/how-to-change-raspberry-pis-swapfile-size-on-rasbian/

 

Followed this instruction: https://github.com/Azure/azure-iot-sdks/blob/master/doc/get_started/python-run-sample.md

Install nodejs npm sudo apt-get install nodejs npm
Update stuff sudo apt-get update
Upgrade stuff sudo apt-get upgrade
Update npm sudo npm install -g npm
Install iothub-explorer sudo npm install -g iothub-explorer
Register device iothub-explorer “<iothub-connection-string>” create <device-name> –connection-string
Open python/device/samples/iothub_client_sample_amqp.py nano iothub_client_sample_amqp.py
Replace [device connection string] with the connection string for your device
Run the script python iothub_client_sample_amqp.py



