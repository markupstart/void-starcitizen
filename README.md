Notes on using the Lug Helper to install Star Citizen in Void Linux

Lug Helper located here: https://github.com/starcitizen-lug/lug-helper

*Star Citizen max-map-count and file limits adjustments.

1. Edit  /etc/sysctl.conf add 
``` 
vm.max_map_count=16777216
```
2. Edit  /etc/security/limits.conf add
```
 * hard nofile 524288
```
3. Edit /etc/pam.d/lightdm add
```
 session required pam_limits.so
```
4. Edit /etc/pam.d/login add
```
 session required pam_limits.so
```
5. Reboot after editing and saving the files.

*Packages needed for Star Citizen (for AMD video cards - NVIDIA will be a bit different)
Add the needed repos

```
sudo xbps-install -S  void-repo-multilib  void-repo-multilib-nonfree  void-repo-nonfree
 ```
Update packages for xbps
 ```
sudo xbps-install -Sy
```
install packages that are needed
```
sudo xbps-install -S zenity lutris wine winetricks mesa-vulkan-radeon mesa-vulkan-radeon-32bit Vulkan-Tools vulkan-loader vulkan-loader-32bit libunwind mesa-32bit gnutls gnutls-32bit psmisc freetype fluidsynth wine-32bit
```
6. Make sure to launch lutris one time before starting the lug-helper.  Once it loads all the necessary files and libraries close lutris.
7. Run the lug-helper and follow the onscreen prompts to install star citizen
8. Launch Lutris, right click on Star Citizen go to configure>system options "Prefer System Libraries" should be enabled.

NVIDIA Notes:
1. If you have NVIDIA instead of AMD video card step 3 above will look like this:
```
sudo xbps-install -S zenity lutris wine winetricks nvidia nvidia-libs-32bit Vulkan-Tools vulkan-loader vulkan-loader-32bit libunwind mesa-32bit gnutls gnutls-32bit psmisc freetype fluidsynth wine-32bit
```

*NOTE for Lutris: if Lutris errors on finding libvulkan only!
```
sudo mv /etc/ld.so.cache /tmp # delete cache
```

```
sudo ldconfig # regenerate cache
```

```
ldconfig -p | grep /usr/lib32/libvulkan.so
```

*STEAM Notes: If Steam doesn't load or errors out, install the following package.
1. mesa-ati-dri-32bit
