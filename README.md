# How to test it.

First of all. You must follow the official libreboot [lbmk building guide.](https://libreboot.org/docs/build/index.html) Remeber to clone the repo:

```bash
git clone https://codeberg.org/libreboot/lbmk
```
For some reason it's not mentioned in the guide above.

The next step is copying the custom files for the X280 to their respective paths.

```bash
git clone https://github.com/AlguienSasaki/X280Libreboot
cd X280Libreboot
cp -rf config/coreboot/x280_vfsp_16mb /path/to/lbmk/config/coreboot
cp -rf config/ifd/x280 /path/to/your/lbmk/config/ifd
cp -rf config/vendor/x280 /path/to/your/lbmk/config/vendor
```

You compile the Libreboot ROM with the following command:
(Remember to move to the lbmk directory)

```bash
./mk -b coreboot x280_vfsp_16mb
```
For now it's not working (but eventually it will, trust me)
so, you need to provide your own $me.bin$ file in the following path

```bash
/path/to/your/lbmk/vendorfiles/x280/me.bin
```

Follow the official coreboot guide to generate a [deguarded me.bin file.](https://doc.coreboot.org/mainboard/lenovo/skylake.html#preparing-the-me-with-deguard) If you already have coreboot flashed in your x280 you can just put whatever as the $me.bin$ (a t480 me.bin for example) and compile the final ROM. If you do this ONLY FLASH THE BIOS REGION OR YOU WILL BRICK YOUR X280 !!!!!
You can do this with the following command:

```bash
sudo flashprog -p internal:boardmismatch=force -w bin/x280_vfsp_16mb/seagrub_x280_vfsp_16mb_libgfxinit_corebootfb_usqwerty.rom --ifd -i bios -N
```

And the result should be something like this:
![First X280 in the world running Libreboot!!! or so I tought](https://github.com/AlguienSasaki/X280Libreboot/blob/main/imgs/2026-02-28-00-22-24-552.jpg?raw=true)

This all the progress I made. When it's finished I'll try to pull request it to the lbmk project so you can just get a final image with:

```bash
./mk -b coreboot x280_vfsp_16mb
```
Or with a direct download from the official site.



