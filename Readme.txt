######## rkdeveloptool on Linux ########

For Linux, we build the latest rkdeveloptool (version >=1.32), from source code.

To build rkdeveloptool on a Debian based Linux distribution, follow the instruction below:

Install build dependency:

 sudo apt-get install libudev-dev libusb-1.0-0-dev dh-autoreconf
Clone the source code and build:

 git clone https://github.com/DmitryTyazhlov/rkdeveloptool
 cd rkdeveloptool
 autoreconf -i
 ./configure
 make
If you encounter compile error like below

 ./configure: line 4269: syntax error near unexpected token `LIBUSB1,libusb-1.0'
 ./configure: line 4269: `PKG_CHECK_MODULES(LIBUSB1,libusb-1.0)'
You should install pkg-config libusb-1.0

 sudo apt-get install pkg-config libusb-1.0
Then re-run

 autoreconf -i
 ./configure
 make
Now you have rkdeveloptool executable at the current directory.

 sudo cp rkdeveloptool /usr/local/bin/
 sudo ldconfig
Make sure that its version is 1.32.or later

 rkdeveloptool -v
 rkdeveloptool ver 1.32


######## rkdeveloptool on macOS(Intel & Apple Silicon) ########

To build rkdeveloptool on macOS, you need homebrew(or similar package manager) to install required packages.

Install build dependency:

 brew install automake autoconf libusb
Clone the source code and build:

 git clone https://github.com/DmitryTyazhlov/rkdeveloptool
 cd rkdeveloptool
 autoreconf -i
 ./configure
 make
If you encounter compile error like below

 ./configure: line 5384: syntax error near unexpected token `LIBUSB1,libusb-1.0'
 ./configure: line 5384: `PKG_CHECK_MODULES(LIBUSB1,libusb-1.0)'
You should install pkg-config libusb-1.0

 brew install pkg-config
Then re-run

 autoreconf -i
 ./configure
 make
Now you have rkdeveloptool executable at the current directory.

 sudo cp rkdeveloptool /opt/homebrew/bin/

Make sure that its version is 1.32 or later.

 rkdeveloptool -v
 rkdeveloptool ver 1.32


###################################################################################


Begin Installation USB -> eMMC
Linux/macOS

On your PC, run the rkdeveloptool

sudo rkdeveloptool ld        # List the device
DevNo=1	Vid=0x2207,Pid=0x330c,LocationID=305	Maskrom

Download the loader (flash helper) to init the ram and prepare the flashing environment etc.

sudo rkdeveloptool db rk3399_loader_v1.27.126.bin

Write the GPT image to eMMC, start to write from offset 0
sudo rkdeveloptool wl 0 /path/to/rockpi4b-xxx-gpt.img

Reboot the device:
sudo rkdeveloptool rd

