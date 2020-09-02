# Plasma-i3_DE

i3 and KDE Plasma

How to install the i3 window manager on KDE Plasma


Situation before installation

    Manjaro KDE Edition, all updates installed
    KDE plasma
    KWin

Installation
Packages

We're gonna install a couple packages that are required or nice-to-haves on i3. This consists of:

    i3-gaps, obviously
    nitrogen
    rofi(optional)
    morc_menu (not required)
    i3-status for the status bar of i3

and their dependencies.

Use this command to install all of this

`$ sudo pacman -S i3-gaps nitrogen i3-dmenu-desktop morc_menu i3-status`

Configuration
Create a new XSession

Create a new file called plasma-i3.desktop in the /usr/share/xsessions directory as su. [1]

Write the following into /usr/share/xsessions/plasma-i3.desktop:

[Desktop Entry]
Type=XSession
Exec=env KDEWM=/usr/bin/i3 /usr/bin/startplasma-x11
DesktopNames=KDE
Name=Plasma with i3
Comment=Plasma with i3

The i3 installation could have installed other .desktop files, you can remove them if you'd like. I only have the default plasma.dektop and plasma-i3.desktop in my folder.

For the following use your existing i3 config or create a new config using $ i3-config-wizard (this also works when you're still in KWin).

Your i3 config should be located at ~/.config/i3/config, although other locations are possible.
Adding stuff to the i3 config

To improve compatibility with Plasma, add the following lines in your i3 config. [1]

# Plasma compatibility improvements
for_window [window_role="pop-up"] floating enable
for_window [window_role="task_dialog"] floating enable

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

Or you can copy my i3 config with these patches.

Killing the existing window that covers everything

Now with my installation, there was a Plasma Desktop window that covered everything and had to be closed with $mod+Shift+q every time I logged in. To circumvent that, follow this tutorial.

Add this line to your i3 config: for_window [title="Desktop — Plasma"] kill; floating enable; border none

Disabling a shortcut that breaks stuff

Launch the Plasma System Settings and go to Workspace > Shortcuts > Global Shortcuts > Plasma and disable the shortcut "Activities" that uses the combination Meta+Q.
Using the plasma shutdown screen

To use the plasma shutdown/logout/reboot screen, delete this line (or comment out) [2]

$bindsym $mod+Shift+e exec "i3-nagbar " ...

and add the following one(s) instead:

# using plasma's logout screen instead of i3's
bindsym $mod+Shift+e exec --no-startup-id qdbus org.kde.ksmserver /KSMServer org.kde.KSMServerInterface.logout -1 -1 -1

Setting the Background (optional)

By default, i3 doesn't set a background and it requires a third party to do that. I am using the default background provided by the Plasma theme with the name of "Andromeda".

I installed these following packages: $ sudo pacman -S andromeda-wallpaper plasma5-themes-andromeda sddm-andromeda-theme andromeda-icon-theme and enabled everything up in the Plasma settings.

To set up the same wallpaper in i3, add the following line to the i3 config:

exec --no-startup-id feh --bg-scale /usr/share/plasma/look-and-feel/org.manjaro.andromeda.desktop/contents/components/artwork/background.png

Editing the bar (optional)

The i3 bar has a nice feature that allows it to be hidden, unless you press $mod. I enabled this, because I have the Plasma status bar.
You can take a look at my i3 config for this.


That's it! I hope this little tutorial helped you, and if you see anything you'd like to improve, absolutely feel free to do so!
Enable transparency (optional)

If you'd like to enable transparency, you need to install a compositor. I use picom, and it works really well with minimal (no) configuration. First, install picom: $ sudo pacman -S picom

Then, add this line to your i3 config: exec_always --no-startup-id picom -bc

The result is something like this:

screenshot of my setup with transparency enabled

Thank you !
