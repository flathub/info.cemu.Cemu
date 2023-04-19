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

## Filesystem write permissions

In order to convert files to wua you can run Cemu without filesystem sandboxing from the terminal via:

```sh
flathub run --filesystem=host info.cemu.Cemu
```

This can be done permanently with [flatseal](https://flathub.org/apps/details/com.github.tchx84.Flatseal) or with:

```sh
flatpak override --user --filesystem=host info.cemu.Cemu
```
