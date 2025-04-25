# 2025-04-25: Installing a Custom Login screen

## Issues
1. The theme was built for qt5 but the version and sddm-greeter support i had was qt6.
2. I wanted an Amadeus themed login screen and settled for this one [sddm-theme-amadeus](https://github.com/Michal-Szczepaniak/sddm-theme-amadeus.git), but the look wasn't to my liking so I redesigned it a bit. (I have no idea how to change qml code and work do stuff for such designs)
3. Finally when I was done with tweaking the theme, it was time to apply it. But on reboot, the 'fallback theme'of sddm was loaded.

## Cause
- this section is only relevant to the '3' issue, so the cause was that this theme was made about 7years ago with support for qt5 and 'sddm-greeter'. But my current 'Kubuntu 24.10' setup has  qt6 as default and the default and ONLY greeter being "sddm-greeter-qt6", an updated version of the older "sddm-greeter" version. So, when the sddm was loading the theme it looked for the 'sddm-greeter' binary in /usr/bin (it wasnt there). I tracked this issue through the sddm entries using 'journal ctl -u sddm'. The line describing this scenario was **"The theme at "/usr/share/sddm/themes/sddm-theme-amadeus" requires missing "/usr/bin/sddm-greeter" . Using fallback theme."**


## Fix
- The custom theme 'amadeus' was actualy very simple in this case. It was a couple of text box overlayed upon a amadeus themed wallpaper. and the custom font, with glow effect did the trick. My fix was to change the wallpaper to another Amadeus themed wallpaper. But now, the textboxes had to repositioned. So, I opened the picture in GIMP, found the coordinated at my required position, changed the values in Main.qml file and changed font.pixelsize along with width & height and there it was. A custom login page.
- To the problem '3', tricking sddm to run 'sddm-greeter-qt6' whenever prompted for 'sddm-greeter' worked. Simply created alink to the qt6 version of greeter with the relevant name in /usr/bin directory using the command: _sudo ln -s /usr/bin/sddm-greeter-qt6 /usr/bin/sddm-greeter_

## Plan
Now, I wanna make an animated login screen with "amadeus-thene", similar to something like this guy's [wallpaper-engine](https://steamcommunity.com/sharedfiles/filedetails/?id=2809050179) on steam.
