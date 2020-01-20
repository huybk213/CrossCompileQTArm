1. Install library for QT5

sudo apt-get install libxkbcommon-dev
sudo apt-get install libxcb1-dev
sudo apt-get install libx11-xcb-dev
sudo apt-get install libxcb-glx0-dev
sudo apt-get install libxcb-keysyms1-dev
sudo apt-get install libxcb-image0-dev
sudo apt-get install libxcb-shm0-dev
sudo apt-get install libxcb-icccm4-dev
sudo apt-get install libxcb-sync0-dev
sudo apt-get install libxcb-xfixes0-dev
sudo apt-get install libxcb-shape0-dev
sudo apt-get install libxcb-randr0-dev
sudo apt-get install libxcb-render-util0-dev

2. Install cross compiler

sudo apt-get install libc6-armel-cross libc6-dev-armel-cross
sudo apt-get install binutils-arm-linux-gnueabihf
sudo apt-get install libncurses5-dev
sudo apt-get install gcc-arm-linux-gnueabihf
sudo apt-get install g++-arm-linux-gnueabihf

3. Download QT 5.5.0 source file
https://download.qt.io/archive/qt/5.5/5.5.0/single/

4. Extract source file
tar -xvzf qt-everywhere-opensource-src-5.5.0.tar.gz

5. Go to folder
qt-everywhere-opensource-src-5.5.0/qtbase/mkspecs/devices

6. Copy folder linux_beagleboard-g++ to folder linux-beaglebone-g++
cp -a linux-beagleboard-g++/ linux-beaglebone-g++

7. Modify qmake.conf in folder linux-bealgebone-g++
Change
--> COMPILER_FLAGS = . . . -mfloat-abi=softfp
--> to
--> COMPILER_FLAGS = . . . -mfloat-abi=hard

8. Back to folder qtbase/mkspecs
cp -r linux-arm-gnueabi-g++ linux-arm-gnueabihf-g++

9. Edit file qmake.conf in folder linux-arm-gnueabihf-g++
Change arm-linux-gnueab- to arm-linux-gnueabihf- 

10. Back to folder
qt-everywhere-opensource-src-5.5.0

11. Configure
sudo ./configure -v -opensource -confirm-license -prefix  /usr/local/qt5-armhf -xplatform linux-arm-gnueabihf-g++ -device linux-beaglebone-g++ -device-option CROSS_COMPILE=/usr/bin/arm-linux-gnueabihf- -qt-libpng -qt-libjpeg -no-nis -qt-xkbcommon-x11

12. Make
sudo make

13. Install
sudo make install

14. Everything done, check output file in /usr/local/qt5-armhf

Reference http://m-embedded.blogspot.com/2015/08/build-qt5-for-beaglebone-balck.html



