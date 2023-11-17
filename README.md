# Flatpak for Cemu

Cemu is a Nintendo Wii U emulator. For more information, please [visit the project website](https://cemu.info/) or [view the source code](https://github.com/cemu-project/Cemu/).

## Transfarring AppImage user data to flatpak

If you've been using the AppImage you can move your saves and settings to the flatpak sandbox with:

```sh
mv ~/.local/share/Cemu ~/.var/app/info.cemu.Cemu/data/Cemu
```

Shader cache with:
```sh
mv ~/.cache/Cemu ~/.var/app/info.cemu.Cemu/cache/Cemu
```

Setting and controller configs with:
```sh
mv ~/.config/Cemu ~/.var/app/info.cemu.Cemu/config/Cemu
```

## Give Cemu access to Wiimotes

Create a udev rules file at `/etc/udev/rules.d/50-cemu-wiimote.rules` containing the following:
```sh
KERNEL=="hidraw*", KERNELS=="*057E:0306*", TAG+="uaccess"
```

Then load the new rule by running
```sh
sudo udevadm control --reload-rules
```

Disconnect and reconnect the Wiimote then restart Cemu. You should not be able to add the Wiimote as an input:

![Screenshot from 2023-08-30 23-02-20](https://github.com/flathub/info.cemu.Cemu/assets/334272/ab44f97f-8d63-4ed4-ad82-a4415311cf87)


## Filesystem write permissions

In order to convert files to wua you can run Cemu without filesystem sandboxing from the terminal via:

```sh
flathub run --filesystem=host info.cemu.Cemu
```

This can be done permanently with [flatseal](https://flathub.org/apps/details/com.github.tchx84.Flatseal) or with:

```sh
flatpak override --user --filesystem=host info.cemu.Cemu
```

## More udev rules

Create a udev rules file at `/etc/udev/rules.d/50-cemu.rules` containing the following:
```sh
# Bluetooth Wiimote
KERNEL=="hidraw*", KERNELS=="*057E:0306*", TAG+="uaccess"

# PS4 LEGO Toypad
SUBSYSTEM=="usb", ATTRS{idVendor}=="0e6f", ATTRS{idProduct}=="0241", MODE="0666", TAG+="uaccess"
```

Then load the new rule by running
```sh
sudo udevadm control --reload-rules
```

Disconnect and reconect the device then restart Cemu.
