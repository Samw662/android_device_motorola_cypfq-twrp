# TWRP Device configuration for Motorola Moto G51 5G

## Device specification

Basic   | Spec Sheet
-------:|:------------------------
CHIPSET | Qualcomm SM4350 (SM4350 "Holi") Snapdragon 480+
GPU     | Adreno 619
Memory  | 4GB, 6GB, 8GB
Shipped Android Version | 11
Storage | 128GB
Battery | 5000 mAh
Dimensions | 170,5 × 76,5 × 9,1 mm
Display | LCD IPS a 6,8, HD+, 120Hz
Rear Camera 1 | 50mp (main)
Rear Camera 2 | 8mp
Rear Camera 3 | 2mp

### Kernel Source
From user 12 S2RYAS32.58-13-12-5-1-3 release-keys

### How to compile
First repo init the twrp-12.1 tree:

```
mkdir ~/android/twrp-12.1
cd ~/android/twrp-12.1
repo init -u git://github.com/minimal-manifest-twrp/platform_manifest_twrp_aosp.git -b twrp-12.1
mkdir -p .repo/local_manifests
```

Then add to a local manifest (if you don't have .repo/local_manifest then make that directory and make a blank file and name it something like twrp.xml):

```xml
<?xml version="1.0" encoding="UTF-8"?>
<manifest>
  <project name="osm0sis/twrp_abtemplate" path="bootable/recovery/installer" remote="github" revision="master"/>
  <project name="android_device_motorola_cypfq" path="device/motorola/cypfq" remote="TeamWin" revision="android-12.1"/>
</manifest>
```

Now you can sync your source:

```
repo sync -j$(nproc --all)
```

To automatically make the TWRP installer zip, you need to import this commit in the build/make path: https://gerrit.twrp.me/c/android_build/+/5445

Finally execute these:

```
. build/envsetup.sh
export ALLOW_MISSING_DEPENDENCIES=true
export LC_ALL=C
lunch twrp_cypfq-eng
mka bootimage -j$(nproc --all)
```
