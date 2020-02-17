Project Trident used to be a FreeBSD desktop operating system based on TrueOS but recently the decision was to move it to Void Linux. More details can be found at the following URL: [Project Trident on Void Linux](https://project-trident.org/post/2019-12-26_stable12-u13_available/).  Since I would like to continue using FreeBSD as my desktop workstation, here is a few  simple steps needed to rebase the existing Project Trident installation (prior to Void Linux migration) to GhostBSD. GhostBSD is another alternative of FreeBSD desktop operation system based on TrueOS where the default desktop environment is Mate.

## Back up current Trident installation
1. sudo beadm create GhostBSD
2. sudo beadm activate GhostBSD
3. sudo reboot
## Switch package repository from Project Trident to GhostBDD
4. Disable current Trident package repository in the following existing file **/etc/pkg/Train.conf**:
```
 Trident-release: {
  url: "https://pkg.project-trident.org/pkg/release",
  signature_type: "pubkey",
  pubkey: "/usr/share/keys/train-pkg.key",
  enabled: no
 }
```
5. Enable latest GhostBSD package repository in the following newly created file **/etc/pkg/GhostBSD.conf**:
```
GhostBSD_PKG: {
  url: "http://pkg.us.ghostbsd.org/stable/${ABI}/latest",
  enabled: yes
}
```
## Update packages from latest GhostBSD package repository
6. sudo pkg update
7. sudo pkg upgrade
8. sudo pkg install mate lightdm lightdm-gtk-greeter
## Enable dbus and lightdm services
dbus was disabled in one of Project Trident updates but it is prerequisite for lightdm to work

9. sudo rc-update add dbus 
10. sudo rc-update add lightdm
