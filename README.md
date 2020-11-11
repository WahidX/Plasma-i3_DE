# Plasma-i3_DE

!! Hello !!\
Here I'll be describing how you can setup your Plasma Desktop Environment with i3 as the Window Manager.

## Screenshots
...

## Installation Packages

We're gonna install a couple packages that are required or nice-to-haves on i3. This consists of:\

    i3-gaps, obviously
    i3-status
    nitrogen
    rofi(optional)
    
and their dependencies.\
Use this command to install all of this\

#### pacman:
` sudo pacman -Syu i3-gaps nitrogen i3-dmenu-desktop i3-status rofi`

#### apt:
` sudo apt-get update && sudo apt-get install i3-gaps nitrogen i3-dmenu-desktop i3-status rofi`

#### zypper:
` sudo zypper in i3-gaps nitrogen i3-dmenu-desktop i3-status rofi`


## Configuration
1. Create a new XSession in /usr/share/xsessions as su.\
`sudo touch /usr/share/xsessions/plasma-i3.desktop`\
Now we have to add these into the plasma-i3.desktop file:\
Using nano you can proceed like:\
` sudo nano /usr/share/xsessions/plasma-i3.desktop`\
Now paste these into the file:\
`[Desktop Entry]\
Type=XSession\
Exec=env KDEWM=/usr/bin/i3 /usr/bin/startplasma-x11\
DesktopNames=KDE\
Name=Plasma with i3\
Comment=Plasma with i3`\

2. The i3 installation could have installed other .desktop files, you can remove them if you'd like. Only leave the default plasma.dektop and plasma-i3.desktop in folder if want.

3. For the config use your existing i3 config or create a new config or use my i3 config using this command. (this also works when you're still in KDE).
`$ i3-config-wizard` 
i3 config should be located at ~/.config/i3/config, although other locations are possible.

4. Adding stuff to the i3 config
To improve compatibility with Plasma, we need to add some lines in the i3 config Or you can copy my i3 config with these patches.
Add the following lines in your i3 config. [1]

# Plasma compatibility improvements
for_window [window_role="pop-up"] floating enable
for_window [window_role="task_dialog"] floating enable
`
for_window [class="yakuake"] floating enable
for_window [class="systemsettings"] floating enable
for_window [class="plasmashell"] floating enable;
for_window [class="Plasma"] floating enable; border none
for_window [title="plasma-desktop"] floating enable; border none
for_window [title="win7"] floating enable; border none
for_window [class="krunner"] floating enable; border none
for_window [class="Kmix"] floating enable; border none
for_window [class="Klipper"] floating enable; border none
for_window [class="Plasmoidviewer"] floating enable; border none
for_window [class="(?i)*nextcloud*"] floating disable
for_window [class="plasmashell" window_type="notification"] border none, move right 700px, move down 450px
no_focus [class="plasmashell" window_type="notification"]
# below one needed to kill the existing window that covers everything
for_window [title="Desktop — Plasma"] kill; floating enable; border none

`
5. Disabling shortcuts that breaks stuff
Launch the Plasma System Settings and go to Workspace > Shortcuts > Global Shortcuts > Plasma and disable the shortcut "Activities" that uses the combination Meta+Q. also I'll recommend to disable other shortcuts using Meta key.

6. Using the plasma shutdown screen
To use the plasma shutdown/logout/reboot screen, delete this line (or comment out)
`$bindsym $mod+Shift+e exec "i3-nagbar " ...`
and add the following one(s) instead:

`# using plasma's logout screen instead of i3's
bindsym $mod+Shift+e exec --no-startup-id qdbus org.kde.ksmserver /KSMServer org.kde.KSMServerInterface.logout -1 -1 -1`

**Now you can sign in i3**


7.Editing the bar (optional)

The i3 bar has a nice feature that allows it to be hidden, unless you press $mod. I enabled this, because I have the Plasma status bar. (Again this is done in my config)
`
bar{
    mode hide
}
`

8. Setting the Background (optional)
By default, i3 doesn't set a background so we will use nitrogen.



That's it! I hope this little tutorial helped you, and if you see anything you'd like to improve, absolutely feel free to do so!
Thank you !
