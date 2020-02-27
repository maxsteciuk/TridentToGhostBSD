During initial installation of Project Trident it was based on FreeBSD CURRENT branch. As of time of migration from Project Trident to GhostBSD FreeBSD CURRENT version is 13.0. GhostBSD does have a repository based on FreeBSD-13.0-CURRENT. However all of the latest updates are coming to FreeBSD-12.1-STABLE branch. Here is a simple walkthrough of what I had to in order to achieve migrationg to the latest branch of GhostBSD:

1. System ABI is sourced either from **/etc/pkg.conf**, **/usr/local/etc/pkg.conf** or from **/bin/sh** by default. Update ABI as follows in **/etc/pkg.conf** or **/usr/local/etc/pkg.conf**. The configuration setting is an architecture triple: <OS name>:<OS version>:<machine architecture>
>> ABI = FreeBSD:12:amd64
2. Bootstrap package repository:
>> sudo pkg bootstrap -f
3. Update repository cache:
>> sudo pkg update -f
4. Install updates from the package repository:
>> sudo pkg upgrade -f
5. Ensure essential GhostBSD packages are installed:
>> sudo pkg install -g *ghostbsd*
5. Reboot the system
>> sudo reboot

## Notes:
Because this is a major system update some packages need to re-installed. For example, I needed to (re)install Xorg input drivers in order to fix my issue with an unresponsive keyboard and mouse.
>> sudo pkg install xorg-drivers
