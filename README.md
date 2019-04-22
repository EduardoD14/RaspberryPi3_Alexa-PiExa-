# RaspberryPi3_Alexa(PiExa)
Build your very own PiExa with this guide like I did!
> NOTE : I did not come up with the project on my own. I simply took a lot of incomplete resources off the web and combined them to make my project work. 

## About 
I have been wanting to put together a RaspberryPi3 project but for one reason or another it kept getting delayed. I finally decided to just go ahead and schedule a time to move forward with a project regardless of how busy I was and I am sure glad I did. In this guide I will show you how to access Amazon's Alexa voice service using a Java client installed on a Raspberry Pi along with a Node.js server.  You will use the Node.js server to obtain a Login with Amazon for your authorization code that will allow you to register your "Alexa enabled device" with Amazon. Amazon provides their own guide but I found it to be not too easy to follow for someone who has never touched a Raspberry Pi so hopefully this will be a little easier to follow. Have fun!

___
# 1) Let's Get Started!

### Hardware 
I wanted to use the bare minimum so be aware that you could totally opt for higher quality products.


1. **Element14 Raspberry Pi 3 B+ Motherboard**  - Buy at Amazon - [Pi3](https://www.amazon.com/gp/product/B07BDR5PDW/ref=ppx_yo_dt_b_asin_title_o00_s01?ie=UTF8&psc=1).
![IMG_4465](https://user-images.githubusercontent.com/47153835/56514722-e9d9ca00-64ea-11e9-96da-b1d28ea35203.png)

2. **CanaKit 5V 2.5A Raspberry Pi 3 B+ Power Supply/Adapter** to power Raspberry Pi. [5V](https://www.amazon.com/gp/product/B00MARDJZ4/ref=ppx_od_dt_b_asin_title_s01?ie=UTF8&psc=1).

![IMG_4473](https://user-images.githubusercontent.com/47153835/56515147-10e4cb80-64ec-11e9-8ce9-38e59534fcee.png)

4. **Micro SD Card** to host operating system install files. [SD](https://www.amazon.com/gp/product/B073K14CVB/ref=ppx_od_dt_b_asin_title_s01?ie=UTF8&psc=1)![IMG_4474](https://user-images.githubusercontent.com/47153835/56515321-7fc22480-64ec-11e9-9505-8d3a300dea2c.png)
5. **USB 2.0 Mini Microphone** You'll need one to talk to Alexa [Mic](https://www.amazon.com/gp/product/B01KLRBHGM/ref=ppx_od_dt_b_asin_title_s01?ie=UTF8&psc=1)
![IMG_4470](https://user-images.githubusercontent.com/47153835/56515352-91a3c780-64ec-11e9-8b0c-e5d12eb41969.png)
6. **External Speaker** 3.5mm audio speaker [Sound](https://www.amazon.com/gp/product/B00L4RFC5Q/ref=ppx_od_dt_b_asin_title_s01?ie=UTF8&psc=1)
![IMG_4468](https://user-images.githubusercontent.com/47153835/56515419-b730d100-64ec-11e9-99c9-f8454747b76e.png)
7.  **USB Keyboard & Mouse** To control your Pi3 before using SSH.[K&M](https://www.amazon.com/Verbatim-99202-Slimline-Keyboard-Mouse/dp/B017M4J1BU/ref=sr_1_4?crid=3AGEMJ0TF5NJO&keywords=usb+keyboard&qid=1555951022&s=wireless&sprefix=usb+keyb%2Cmobile%2C192&sr=1-4)![IMG_4478](https://user-images.githubusercontent.com/47153835/56515606-1858a480-64ed-11e9-8177-04b59ebe610c.png)
8. **HDMI Visual** -Plug in your Pi3 to any monitor with HDMI.
![IMG_4787](https://user-images.githubusercontent.com/47153835/56515693-5786f580-64ed-11e9-98da-250487cbba04.png)

### Raspberry Pi Setup
First and foremost we need to setup our brand new Raspberry Pi with an operating system. The easiest way to do this is by using Raspbian NOOBS OS. NOOBS stands for New Out Of the Box Software. When you have a completely new Raspberry Pi this will help you load the operating system with little to no work.  

You can find the latest NOOBS download at [downloads.raspberrypi.org/NOOBS_latest](https://downloads.raspberrypi.org/NOOBS_latest).

Downloading this zip file will take a while but once it is complete you simply open the file and then click on "extract all". ![extract](https://user-images.githubusercontent.com/47153835/56516329-0841c480-64ef-11e9-9e51-6d7d72ece6ea.PNG)
Then you just simply clock on extract and it will bring you to the files. 
![all](https://user-images.githubusercontent.com/47153835/56516337-0e37a580-64ef-11e9-8583-03c949dd3fff.PNG)Next you plug in your MicroSD card and open it up. Last, but certainly not least, you drag all of contents of the new folder onto the empty MicroSD card. Before you pull out the MicroSD card, make sure to properly eject the card. Once you have take the card out simply place it into the Raspberry Pi 3 on the underside of the motherboard with the notches facing outward and the lettering facing towards you. 

Now we move onto installing the operating system. Plug in all of your cables, including your keyboard & mouse, the usb microphone, the 3.5 mm audio jack for the speaker/headphones, the HDMI to the monitor and then 2.5A Micro USB power cable. 

When you plug in the power cable your Raspberry Pi will automatically begin to boot. You will see the loading screen on your HDMI output screen go through the boot process.  Once the Raspberry Pi loads up correctly you will be asked to configure a few things. Check the box next to the "Raspbian[Recommended} and make sure to pick your language at the bottom of the screen. Once you have configured your preferences, click on the Install button on the upper left-hand side. 

Now we wait.. this will take a while. Eventually you will see a success message. Click OK and then your desktop will populate. Now you will have the opportunity to connect to your Wi-Fi network, if you so choose to. Being connected to the Wi-Fi however will increase download speeds and allow you to remote into the Raspberry Pi remotely. The default login for Raspbian is username **pi** with the password **raspberry**. At this point we will make sure sound will be coming out of the audio jack. To do so, right-click the speaker icon on the top right hand of the screen on the desktop and select **Analog**. 


## 2 - Utilities - SSH & Node
**NOTE**: With the latest Pi3's we have VNC already installed. To make sure it is active open click on the terminal icon on the top left of the screen. Then type in *sudo raspi-config*. Navigate down to SSH and VNC and make sure they are enabled. This will allow for you to be able to remote in from other devices such as your laptop or even your phone.

Now log onto your mobile device. If you will be remoting in from your iPhone then download the VNC viewer app. If you will be remoting in using your laptop then download the [VNC viewer application](https://www.realvnc.com/en/connect/download/viewer/).
Once  you have VNC Viewer setup remote into your Raspberry PI. 
You will need to know your Raspberry Pi's IP address and it will need to be connected to the same Wi-FI network as your mobile device. Once you connect to the Wi-Fi network use the terminal program to find the ip address by using the following command: 
*hostname -I *
Your terminal will spit out an ip address which will be determined by the type of network you are on. It may look something like this:

	> 192.168.1.5

Once you have this IP address you are can attempt to remote into the Raspberry Pi. Open your VNC application which will look something like this:
![image](https://user-images.githubusercontent.com/47153835/56533224-1f42df80-650c-11e9-987c-75213c6ac3c7.png)

Here I already have two connections setup but your screen will most likely be blank. Right click anywhere in the white space and click on new connection like so:

![image](https://user-images.githubusercontent.com/47153835/56533349-5618f580-650c-11e9-9e79-f073b3d5e9b9.png)

Once you click on the *New Connection* option, a new window will populate. 

![image](https://user-images.githubusercontent.com/47153835/56533397-6630d500-650c-11e9-876d-afe246a610b8.png)

In the box where it says *IP address or hostname*, type in your Raspberry Pi's ip address that we found up above. You can name this connection something specific to remind yourself what the connection is. Up above I have to connections named *HomeNetwork* and *Hotspot* so that I know which connection to use depending on whether I am at home or on the go. Leave all the other options as they are. If you are prompted to enter a username and password remmember that the default username is **pi** and the default password is **raspberry**. 


>note: I am still making this guide and will continue to add to it over the next few days.
