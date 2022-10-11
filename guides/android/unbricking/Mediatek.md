# How to unbrick a device - Mediatek.

### Getting the required firmware.
> Some manufacturers release it on their website, some don't and you may require firmware from 3rd party websites.
>
> For Samsung device you require using some tool like **mtk_meta_utility** to extract the samsung firmware and get a scatter one instead.

### Getting the required tools.
> [**MTK Auth Bypass utility**](https://github.com/MTK-bypass/bypass_utility).
>
> [**Exploits Collection**](https://github.com/MTK-bypass/exploits_collection). *[__/payloads__ folder & __default_config.json5__ needed by the Bypass Utility.]*
>
> [**SP Flash Tool v5.1936**](https://mega.nz/file/HbpTQSbT#a-N4QTxDMivVUe04sTvPmO-0z6nOwwM876IHqfZ4hHc) - url provided by Blackview. *[We'll be using it to flash the firmware or the bootloader.]*

### Getting the scatter firmware (If provided in other way that can be extracted via mtk_meta_utility).
> 1 - Download mtk_meta_utility (url not provided in here)
>
> 2 - Open it and extract you firmware using the button meant for your manufacturer.
>
> 3 - Wait until it finishes and enjoy.

### Bypassing Manufacturer's preloader flashing Authentication. (Needed to flash via 3rd party software.)
> 1 - Get **MTK Auth Bypass utility** and its **Exploits Collection** and extract both on the same directory, meaning you now have a folder with main.py, /payloads folder, a json5 file, etc.
>
> 2 - Follow the [**Usage Guide**](https://github.com/MTK-bypass/bypass_utility/blob/master/README.md) from the official repository.

### Flashing the bricked partitions back.
> 1 - Open **SP Flash Tool v5.1936**
>
> 2 - Select your respective **scatter** file from the firmware you found on 3rd party provides, manufacturer's page or you got using some tools.
>
> 3 - When flashing **ONLY** select the affected partitions like __param & up_param__ on samsung a.k.a **The Bootloader** to be able to restore the other partitions the right way via **Odin Flash Tool** or your manufacturer's provided **Flash Tool**.
>
> 4 - If you still being a *"No risk, no fun"* man then continue with your adventure of flashing the entire firmware, I don't recommend it but it's your choice. I just tell you **TO NOT** flash the preloader, just to be safe.

### Fixing ["SECURE CHECK FAIL : : PIT"] on Samsung Devices after unbricking.
> 1 - Open [**The Odin Flash Tool**](https://forum.xda-developers.com/attachments/odin3-v3-14-1_3b_patched-zip.5158507/)
>
> 2 - Go to your original firmware and open the **CSC Slot** using some archive extractor like [7-Zip](https://7-zip.org/) and extract the file with the **.pit extension**.
>
> 3 - Now go to **The Odin Flash Tool**, select all your firmware slots like BL, AP, CP (If Avaible), CSC.
>
> 4 - Go to the **Options** tab and check the **Re-Partition** check-box.
>
> 5 - Go to the **Pit** tab and select the .pit file you extracted on the previous step 2.
>
> 6 - Your device should be ready to start flashing and enjoy AndroidOS once again.

### Supported SoCs
- mt6261
- mt6572
- mt6580
- mt6582
- mt6592
- mt6595
- mt6735
- mt6737
- mt6739
- mt6750
- mt6753
- mt6755
- mt6757
- mt6761
- mt6763
- mt6765
- mt6768
- mt6771
- mt6779
- mt6785
- mt6795
- mt6797
- mt6799
- mt6833
- mt6853
- mt6873
- mt6885
- mt8127
- mt8163
- mt8167
- mt8173
- mt8590
- mt8695