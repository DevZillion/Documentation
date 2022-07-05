# How to build your own TeamWin Recovery Project device tree - Mediatek.

### Getting a similar device tree as a start point.
> Some things like the processor & motherboard could help you pick a start point, it's recommended to pick a similar processor from the same brand/manufacturer.

### twrp_device.mk
```mk
# Release name
PRODUCT_RELEASE_NAME := <device>

# Inherit from common AOSP config
$(call inherit-product, $(SRC_TARGET_DIR)/product/aosp_base.mk)

# Inherit some common TWRP stuff.
# For PitchBlack use vendor/pb/config/common.mk
$(call inherit-product, vendor/twrp/config/common.mk)

# Inherit device configuration
$(call inherit-product, device/samsung/<device>/device.mk)

# Charger
PRODUCT_PACKAGES += \
    charger_res_images

PRODUCT_COPY_FILES += $(call find-copy-subdir-files,*,device/samsung/<device>/recovery/root,recovery/root)

## Device identifier. This must come after all inclusions
PRODUCT_NAME := twrp_<device>
PRODUCT_DEVICE := <device>
PRODUCT_MODEL := <device-model>
PRODUCT_BRAND :=
PRODUCT_MANUFACTURER :=
PRODUCT_GMS_CLIENTID_BASE := android-<manufacturer>
```

### twrp.dependencies
> If your device doesn't depend in any other stuff it will look like this:
```
[
]

```

### system.prop
> You can get the required values by doing ``adb shell getprop <prop>``.
> It usually looks like this one:
```prop
ro.display.series=Samsung A31
ro.product.board=k68v1_64_titan
ro.board.platform=mt6768
sys.usb.controller=musb-hdrc
ro.boot.dynamic_partitions=true
ro.boot.boot_devices=bootdevice,11230000.mmc

```

### mkbootimg is pretty universal so keep the same you got.
### device.mk - you may be interested in changing some device specific stuff in here.
### bootimg.mk - you may require to modify some paths in there, but leave it as it is.

### AndroidProducts.mk
```mk
PRODUCT_MAKEFILES := \
	$(LOCAL_DIR)/twrp_<device>.mk
COMMON_LUNCH_CHOICES := twrp_<device>-eng
```

### Device.mk - leave it as it is.
### BoardConfig.mk - it will require you to modify some values, the values will have specific guides in here.
### /prebuilt/dtbo - you'll get it using [this method](https://devzillion.github.io/Documentation/guides/android/ExtractDTBO.html).
### /prebuilt/Image - Your kernel's Image.
### /prebuilt/Dtb - Your kernel's ``.dts``.

### /recovery/root/ - Replace the files in there with the ones extracted from your stock recovery.img, you may want to do a custom twrp.flags for your device.