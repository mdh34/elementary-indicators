# elementary-indicators
An unofficial guide to restore indicator functionality on elementary OS

## An overview
The indicator stack on elementary OS consists of the `indicator-application` package and the corresponding `wingpanel-indicator-ayatana` wingpanel component.

The standard Ubuntu `indicator-application` package needs patching to enable support for Pantheon - you can download a premade patched .deb [here](https://github.com/mdh34/elementary-indicators/releases) or read the instructions below to patch it yourself.

The `wingpanel-indicator-ayatana` package is no longer included in the standard elementary repos, however you can download the latest .deb [here](https://launchpad.net/~elementary-os/+archive/ubuntu/stable/+files/wingpanel-indicator-ayatana_2.0.3+r27+pkg17~ubuntu0.4.1.1_amd64.deb) and the source is still avaliable [here](https://github.com/elementary/wingpanel-indicator-ayatana).

## Installing the packages
To install the packages, you can use a .deb installer like [Eddy](http://appcenter.elementary.io/com.github.donadigo.eddy/) or run `sudo dpkg -i filename` in your terminal.
Once you've installed both packages, a reboot should get your indicators working in Pantheon.

## Patching indicator-application
### Update the .desktop
First, download the source to a directory of your choice by running `bzr branch lp:indicator-application` in your terminal (you'll need the `bzr` package installed if you don't already)

The patch itself is very small and straightforward - edit the `indicator-application.desktop.in` file located in the data folder and edit it so this line:

`OnlyShowIn=Unity;GNOME;`

becomes

`OnlyShowIn=Unity;GNOME;Pantheon;`

and save the file.

### Generate a patched .deb
Now you can generate a patched .deb - the first step is to install the build dependencies by running:

`sudo apt install debhelper dh-translations dh-autoreconf dbus-test-runner gnome-common xvfb libglib2.0-dev libgtk-3-dev libdbus-glib-1-dev libjson-glib-dev intltool libappindicator3-dev libindicator3-dev libdbusmenu-glib-dev libdbusmenu-gtk3-dev`

in your terminal.

The final step is to run `debuild -i -us -uc -b` in the root of the `indicator-application` folder. Once this has finished, there should be a .deb for you to install in the parent directory.
