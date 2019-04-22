# RaspberryPi3_Alexa(PiExa)
Build your very own PiExa with this guide like I did!
> NOTE : I did not come up with the project on my own. I simply took a lot of incomplete resources off the web and combined them to make my project work. 

## About 
I have been wanting to put together a RaspberryPi3 project but for one reason or another it kept getting delayed. I finally decided to just go ahead and schedule a time to move forward with a project regardless of how busy I was and I am sure glad I did. In this guide I will show you how to access Amazon's Alexa voice service using a Java client installed on a Raspberry Pi along with a Node.js server.  You will use the Node.js server to obtain a Login with Amazon for your authorization code that will allow you to register your "Alexa enabled device" with Amazon. Amazon provides their own guide but I found it to be not too easy to follow for someone who has never touched a Raspberry Pi so hopefully this will be a little easier to follow. Have fun!

___
# Let's Get Started!

### Hardware 
I wanted to use the bare minimum so be aware that you could totally opt for higher quality products.

1. **Element14 Raspberry Pi 3 B+ Motherboard**  - Buy at Amazon - [Pi3](https://www.amazon.com/gp/product/B07BDR5PDW/ref=ppx_yo_dt_b_asin_title_o00_s01?ie=UTF8&psc=1).
2. **CanaKit 5V 2.5A Raspberry Pi 3 B+ Power Supply/Adapter** to power Raspberry Pi. [5V](https://www.amazon.com/gp/product/B00MARDJZ4/ref=ppx_od_dt_b_asin_title_s01?ie=UTF8&psc=1).
3. **Micro SD Card** to host operating system install files. [SD](https://www.amazon.com/gp/product/B073K14CVB/ref=ppx_od_dt_b_asin_title_s01?ie=UTF8&psc=1)
4. **USB 2.0 Mini Microphone** You'll need one to talk to Alexa [Mic](https://www.amazon.com/gp/product/B01KLRBHGM/ref=ppx_od_dt_b_asin_title_s01?ie=UTF8&psc=1)
5. **External Speaker** 3.5mm audio speaker [Sound](https://www.amazon.com/gp/product/B00L4RFC5Q/ref=ppx_od_dt_b_asin_title_s01?ie=UTF8&psc=1)
6.  **USB Keyboard & Mouse** To control your Pi3 before using SSH.[K&M](https://www.amazon.com/Verbatim-99202-Slimline-Keyboard-Mouse/dp/B017M4J1BU/ref=sr_1_4?crid=3AGEMJ0TF5NJO&keywords=usb+keyboard&qid=1555951022&s=wireless&sprefix=usb+keyb%2Cmobile%2C192&sr=1-4)
7.  **HDMI Visual** -Plug in your Pi3 to any monitor with HDMI.

### Raspberry Pi 
