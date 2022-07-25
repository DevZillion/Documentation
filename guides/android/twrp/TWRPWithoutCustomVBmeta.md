# How to make your twrp boot without any vbmeta

### Getting avbtool.py
Get it from here: https://android.googlesource.com/platform/external/avb/+/refs/heads/master/avbtool.py

### Getting info from stock recovery.img
```sh
python avbtool.py info_image --image recovery.img
```

### Setting up BoardConfig.mk
```mk
# Be sure to have these flags as they are avb related
BOARD_AVB_ENABLE := true
BOARD_AVB_ROLLBACK_INDEX := $(PLATFORM_SECURITY_PATCH_TIMESTAMP)
BOARD_AVB_RECOVERY_KEY_PATH := external/avb/test/data/testkey_rsa4096.pem
BOARD_AVB_RECOVERY_ALGORITHM := SHA256_RSA4096
```

```mk
# Set this according to the info given by avbtool.py
BOARD_AVB_RECOVERY_ROLLBACK_INDEX := 0
BOARD_AVB_RECOVERY_ROLLBACK_INDEX_LOCATION := 0
BOARD_AVB_MAKE_VBMETA_IMAGE_ARGS += --flag 0
```

### Setting up the device tree in general
Remove any ``mkbootimg`` file if it is present.

Be sure to remove this reference to a custom bootimg.mk in the device device tree like:
```mk
# BOARD_CUSTOM_BOOTIMG_MK := $(DEVICE_PATH)/bootimg.mk
```

Also check that these flags are correct and corresponding to your device:
```mk
# Kernel
TARGET_PREBUILT_KERNEL := $(DEVICE_PATH)/prebuilt/
TARGET_PREBUILT_DTB := $(DEVICE_PATH)/prebuilt/
BOARD_PREBUILT_DTBOIMAGE := $(DEVICE_PATH)/prebuilt/
BOARD_INCLUDE_DTB_IN_BOOTIMG :=
BOARD_INCLUDE_RECOVERY_DTBO :=
TARGET_KERNEL_ARCH :=

# Boot
BOARD_BOOT_HEADER_VERSION :=
BOARD_BOOT_HEADER_SIZE :=
BOARD_KERNEL_BASE :=
BOARD_KERNEL_CMDLINE :=
BOARD_KERNEL_IMAGE_NAME :=
BOARD_KERNEL_PAGESIZE :=
BOARD_KERNEL_OFFSET :=
BOARD_RAMDISK_OFFSET :=
BOARD_KERNEL_SECOND_OFFSET :=
BOARD_KERNEL_TAGS_OFFSET :=
BOARD_DTB_OFFSET :=
BOARD_DTB_SIZE :=
BOARD_MKBOOTIMG_ARGS := \
	--kernel_offset $(BOARD_KERNEL_OFFSET) \
	--ramdisk_offset $(BOARD_RAMDISK_OFFSET) \
	--tags_offset $(BOARD_KERNEL_TAGS_OFFSET) \
	--second_offset $(BOARD_KERNEL_SECOND_OFFSET) \
	--header_version $(BOARD_BOOT_HEADER_VERSION) \
	--pagesize $(BOARD_KERNEL_PAGESIZE) \
	--board "DummyBoard" \
	--dtb $(TARGET_PREBUILT_DTB) \
	--dtb_offset $(BOARD_DTB_OFFSET) \
	--recovery_dtbo $(BOARD_PREBUILT_DTBOIMAGE)
```


