eeGeo 3D Maps mobile-sdk-harness
================================

Additional documentation available at http://sdk.eegeo.com

Dependencies
============

The eeGeo SDK makes use of CMake, the cross-platform open-source build system (http://www.cmake.org)

* Download CMake 3.0 from http://www.cmake.org/cmake/resources/software.html
* Install CMake and ensure that cmake 3.0 is available on your path
* For specific documentation for CMake, refer to http://www.cmake.org/cmake/help/v3.0/

iOS
===

* Run ./build.sh -p ios to download the latest platform libraries and headers, create an Xcode project with CMake, and build the project on the command line
* The Xcode project eegeo-sdk-project.xcodeproj is generated out-of-source, and placed in the /ios/build/ directory
* Run ./update.platform.sh -p ios to get the latest platform libraries and headers in future
* The generated project will attempt to use your default code-signing identity
* To regenerate the Xcode project, run make_project.sh from the ios directory
* To build for an iOS device or simulator in Xcode, build the 'eegeo-sdk' target
* CMake includes two targets ('ALL_BUILD' and 'ZERO_CHECK'), which rebuild all targets and re-run CMake commands specified in the CMakeLists.txt; these targets are created by automatically by CMake. 
* To change the project settings, edit the CMakeLists.txt file under ios and build the ZERO_CHECK target
* The platform needs an API key to operate. Sign up at https://appstore.eegeo.com/ to get your API key and introduce it into the following line in ViewController.mm : 
	#define API_KEY "OBTAIN API_KEY FROM https://appstore.eegeo.com AND INSERT IT HERE".
* Scroll between the examples using the Next and Previous buttons; the current example name is displayed at the top of the screen.


Android
=======

* Install the Android SDK and NDK
* Run ./build.sh -p android to get the latest platform libraries and headers and build the APK, generating Android NDK build process files as artefacts
* Run ./update.platform.sh -p android to get the latest platform libraries and headers in future
* Open an ADT Eclipse workspace, importing this repository as an Android project
* Set the NDK location in the ADT Eclipse workspace to where it was installed (Menu->ADT->Android->NDK)
* Configure your workspace:
    * File -> Import -> Android: 'Existing Android Code Into Workspace'
    * Select the 'android' directory in the repository
    * ADT -> Preferences -> Android -> NDK : Set NDK location
    * Select imported activity -> Android Tools : 'Add native support'
    * Select jni directory -> New folder -> Advanced -> Linked folder : mobile-sdk-harness/src
* Bring up the project menu, from within Android Tools add native support to the project
* The platform needs an API key to operate. Sign up at https://appstore.eegeo.com/ to get your API key and introduce it into the following line in jni/main.cpp : 
	#define API_KEY "OBTAIN API_KEY FROM https://appstore.eegeo.com AND INSERT IT HERE"
* Build and debug from within ADT Eclipse
* build.sh can be used to generate the native library if you want to manually package the .apk
* Scroll between the examples using the Next and Previous buttons, or select the example from the drop-down list; the current example name is displayed at the top of the screen. 
* To build at the command line, run ./build -p android from the repository root.

iOS c++11 support
=================
* ./update.platform.sh -p ios -c will fetch c++11/libc++ ABI compatible versions of the SDK for libc++
* ./build -p ios -c from the command line will build targeting c++11 / libc++
* CMake will automatically generate a project such that the eegeo-sdk target uses the appropriate libraries for c++11
* To generate a c++11 project using CMake, run make_project.sh -c. This assumes you have obtained a c++11 version of the platform using ./update.platform.sh -p ios -c

android c++11 support
=====================
* Android c++11 support is EXPERIMENTAL due to the experimental nature of c++11 support in the NDK (see https://developer.android.com/tools/sdk/ndk/index.html & https://gcc.gnu.org/gcc-4.8/cxx0x_status.html)
* Only tested against Android NDK version r9d - https://developer.android.com/tools/sdk/ndk/index.html
* Only tested against gcc 4.8 & gnu libstd++ (see android/jni/Application.mk for how to target these)
* ./update.platform.sh -p android -c will fetch c++11/gnu libstdc++ ABI compatible versions of the SDK
* ./build -p android -c from the command line will build targeting c++11
* Pass COMPILE_CPP_11=1 to ndk-build to build cpp11
