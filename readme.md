Unoficial CM-10.2 for Sony Xperia U

Getting Started :

    mkdir cm-10.2
    cd cm-10.2
    repo init -u git://github.com/CyanogenMod/android.git -b cm-10.2
    repo sync -j16
    cd device
    mkdir sony
    cd sony
    git clone https://github.com/XperiaNovathor/android_device_sony_kumquat.git -b master kumquat
    cd kumquat

Now connect your phone which have runing FXP CM10 :

    ./extract-files.sh
    cd ../../..
    cd hardware
    git clone https://github.com/munjeni/aosp_4.3_hardware_semc.git -b master semc
    cd ..
    mkdir -p kernel/sony
    cd kernel/sony
    git clone https://github.com/munjeni/android_kernel_xperiago.git -b jb-dev u8500
    cd ../..

Patch android source code :

    patch -p1 < device/sony/kumquat/patches/framework_av.patch
    patch -p1 < device/sony/kumquat/patches/framework_native.patch
    patch -p1 < device/sony/kumquat/patches/hardware_libhardware.patch
    patch -p1 < device/sony/kumquat/patches/hardware_libhardware_legacy.patch
    patch -p1 < device/sony/kumquat/patches/system_core.patch

Our step is optional!!! Use only if you going to sync CM source code daily, than simple revert each patch before you sync CM source code :

    patch -p1 -R < device/sony/kumquat/patches/framework_av.patch
    patch -p1 -R < device/sony/kumquat/patches/framework_native.patch
    patch -p1 -R < device/sony/kumquat/patches/hardware_libhardware.patch
    patch -p1 -R < device/sony/kumquat/patches/hardware_libhardware_legacy.patch
    patch -p1 -R < device/sony/kumquat/patches/system_core.patch
    repo forall -p -c 'git checkout -f'
    repo sync
    patch -p1 < device/sony/kumquat/patches/framework_av.patch
    patch -p1 < device/sony/kumquat/patches/framework_native.patch
    patch -p1 < device/sony/kumquat/patches/hardware_libhardware.patch
    patch -p1 < device/sony/kumquat/patches/hardware_libhardware_legacy.patch
    patch -p1 < device/sony/kumquat/patches/system_core.patch

Download CM prebuilts :
   cd vendor/cm
   ./get-prebuilts
   cd ../..

You are ready to build :

    . build/envsetup.sh
    lunch cm_kumquat-userdebug
    make otapackage

ENJOY! 
