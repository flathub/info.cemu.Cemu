# Flatpak for Cemu

Cemu is a Nintendo Wii U emulator. For more information, please [visit the project website](https://cemu.info/) or [view the source code](https://github.com/cemu-project/Cemu/).

## Filesystem write permissions

In order to convert files to wua you can run Cemu without filesystem sandboxing from the terminal via:

```
flathub run --filesystem=host info.cemu.Cemu
```

This can be done permanently with [flatseal](https://flathub.org/apps/details/com.github.tchx84.Flatseal) or with:
```
flatpak override --user --filesystem=host info.cemu.Cemu
```
