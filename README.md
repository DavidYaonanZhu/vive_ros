# vive_ros

Video example: [https://youtu.be/1hiX0f6UAew](https://youtu.be/1hiX0f6UAew)

## Installation instructions

Installation instructions based on: `https://www.gamingonlinux.com/articles/first-steps-with-openvr-and-the-vive-on-linux.7229`


### Download and build Valve's OpenVR SDK (most recently tested version):

      cd ~
      mkdir libraries
      cd libraries
      git clone https://github.com/ValveSoftware/openvr.git -b v1.3.22
      cd openvr
      mkdir build
      cd build
      cmake -DCMAKE_BUILD_TYPE=Release ../
      make

### Allow hardware access
Then plug-in VIVE to your computer and make sure you can see the devices on `/dev/hidraw[1-6]`.

Copy the file `88-vive.rules` to the folder `/etc/udev/rules.d`. Then run:

      sudo /etc/init.d/udev restart

### Install Steam and SteamVR

Go to `http://store.steampowered.com/` and download Steam for Linux.
After successfully installing and running Steam, it should store its files on: `~/.local/share/Steam`

Install SteamVR by using this URL `steam://install/250820`.
Files should be located on: `~/.local/share/Steam/steamapps/common/SteamVR`

### Configure display.

Go to your OS display options to enable HMD's display.

## Usage

Before start:

* Make sure VIVE is present as several `/dev/hidraw*` and you have access permissions.
* Make sure VIVE display is enabled as extended view.
* Libraries and Steam are present on the folders described by `INSTALL.md`.

Procedure:

1. Start a `roscore`
2. Launch the SteamVR's `vrserver` by launching the file: `roslaunch vive_ros server_vr.launch`
3. Launch the node: `roslaunch vive_ros vive.launch`
4. To close the node you can `Ctrl+C`. To close the vr server you have to kill the process. For convenience: `rosrun vive_ros close_servervr.sh`

Update in my version of code:
1. Hardware Safety code added in order to shutdown of hardware. This will prevent hardware from any damage caused due to abrupt shutdown.

2. It has code updated for publishing HTC Vive Component (HTC Vive Headset and 2 HTC Controllers) data.
