# How to build your own TeamWin Recovery Project from source.

### Updating Ubuntu repos and packages.
```sh
	sudo apt-get update
	sudo apt-get upgrade
```

### Installing ADB & Fastboot tools.
```sh
	sudo apt-get install android-tools-adb android-tools-fastboot
```

### Installing the required dependencies.
```sh
sudo apt-get install bc bison build-essential ccache curl flex g++-multilib gcc-multilib git gnupg gperf imagemagick lib32ncurses5-dev lib32readline-dev lib32z1-dev liblz4-tool libncurses5 libncurses5-dev libsdl1.2-dev libssl-dev libxml2 libxml2-utils lzop pngcrush rsync schedtool squashfs-tools xsltproc zip zlib1g-dev
```

### Getting OpenJDK.
> Get the right package for your Ubuntu version in [here](https://packages.ubuntu.com/source/openjdk-lts).
### Installing repo.
```sh
	mkdir -p ~/bin
	echo export PATH=\$PATH:\$HOME/bin >> ~/.bashrc
	source ~/.bashrc
	curl https://storage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
	chmod a+rx ~/bin/repo
```

### Getting TWRP Source Code.
Set the -b argument to ``twrp-11`` for Android 11 or ``twrp-12.1`` for Android 12
```sh
mkdir twrp && cd twrp
repo init --depth=1 -u git://github.com/minimal-manifest-twrp/platform_manifest_twrp_aosp.git -b twrp-11
repo sync
```

### Setting up TWRP for building.
> - Get the right stuff inside .repo/local_manifest/roomservice.xml
```xml
<manifest>
  <project path="device/<brand>/<device>" name="<repo-owner-name>/<repo-name>" remote="github" revision="<branch>"/>
</manifest>
```

> - Here is an example of a roomservice.xml
```xml
<manifest>
  <project path="device/samsung/a31" name="Galaxy-MT6768/android_device_samsung_a31nsxx" remote="github" revision="android-11"/>
  <project path="device/samsung/a41" name="Galaxy-MT6768/android_device_samsung_a41xx" remote="github" revision="android-11"/>
</manifest>

```
### Setting up device trees.
```sh
repo sync --force-sync device/<brand>/<device>
```

### Building
> For a device with recovery partition:
```sh
source build/envsetup.sh; lunch twrp_<device>-eng; mka recoveryimage
```
> For a device with boot partition:
```sh
source build/envsetup.sh; lunch twrp_<device>-eng; mka bootimage
```
