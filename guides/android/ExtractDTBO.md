# Extracting Android Files from recovery/boot image.

## Getting the tools requires
> Simply download [this](https://android.googlesource.com/platform/system/tools/mkbootimg/+/ebf8d50f0e06d1eee9a33521f77c327b1a75f353/unpack_bootimg.py) to a folder in your computer.

## How to run
> type ``python unpack_bootimg.py --boot_img <TheNameOrPathOfYourImage>``
> and you'll get an output like this: dtb, kernel, ramdisk, recovery_dtbo; from there you can modify and do wathever you want with the files.