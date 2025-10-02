# Linux

## Fedora

Flatpak Librewolf having no access to camera.

```sh
# set
flatpak override --user io.gitlab.librewolf-community --device=all

# unset
flatpak override --reset io.gitlab.librewolf-community
```
