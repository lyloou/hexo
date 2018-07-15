## [How do you run Ubuntu Server with a GUI?](https://askubuntu.com/questions/53822/how-do-you-run-ubuntu-server-with-a-gui)
```sh
# Minimal GUI:
sudo apt install xorg
sudo apt install --no-install-recommends openbox

# Minimal GUI with display manager:
sudo apt install xorg
sudo apt install --no-install-recommends lightdm-gtk-greeter
sudo apt install --no-install-recommends lightdm
sudo apt install --no-install-recommends openbox

#A more functional minimal desktop environment (the one I use):
sudo apt install xorg
sudo apt install --no-install-recommends lightdm-gtk-greeter
sudo apt install --no-install-recommends lightdm
sudo apt install --no-install-recommends lxde-icon-theme
sudo apt install --no-install-recommends lxde-core
sudo apt install --no-install-recommends lxde-common
sudo apt install --no-install-recommends policykit-1 lxpolkit
sudo apt install --no-install-recommends lxsession-logout
sudo apt install --no-install-recommends gvfs-backends

#
sudo apt install xorg
sudo apt install xubuntu-core
```
## [Can I access Ubuntu from Windows remotely?](https://askubuntu.com/questions/592537/can-i-access-ubuntu-from-windows-remotely)
