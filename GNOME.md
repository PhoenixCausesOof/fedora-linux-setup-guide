# GNOME Setup

## Replace GNOME Totem with mpv

```text
sudo dnf swap totem mpv
```

Check out [configuring MPV](https://wiki.archlinux.org/title/Mpv#Configuration). Also make sure you're getting hardware acceleration properly.

## Replace GNOME System Monitor

### (with) htop

[`htop`](https://htop.dev/) is a lightweight system monitor for the terminal.

```text
sudo dnf swap gnome-system-monitor htop
```

### (with) Resources

If you want something graphical, you can use something like [Resources](https://github.com/nokyan/resources).

```text
sudo dnf rm gnome-system-monitor
flatpak install flathub net.nokyan.Resources
```

No matter what system monitor you go with, just remove GNOME's.

## Remove unused GNOME apps

These apps remain unused for me, at least. Feel free to keep whichever ones you need (though you'll need to figure out which does what).

```text
sudo dnf rm rhythmbox gnome-connections gnome-contacts evince gnome-tour simple-scan
```

If you're not doing office work, remove LibreOffice:

```text
sudo dnf rm "libreoffice-*"
```

## (Install) GNOME Tweaks

GNOME Tweaks allows (proper) configuring of system fonts, themes, mouse, touchpad and keyboards, enabling titlebar buttons, etc. It's essential in any GNOME system.

```text
sudo dnf install gnome-tweaks
```

## Extensions

Install [Extension Manager](https://flathub.org/apps/com.mattjakeman.ExtensionManager):

```text
flatpak install flathub com.mattjakeman.ExtensionManager
```

Pick some extensions: <https://extensions.gnome.org/#sort=downloads> (you can also browse in the Extension Manager app)

## Theming

I think GNOME is quite limited in regard to theming. That said, I don't find it that much of a necessity since the desktop already looks decent. If you still want to spice some things up, then...

As a prerequisite, every GTK theme you pick should support GNOME Shell / libadwaita / GTK4 theming. You need this in order to have a consistent looking system. Make sure you install the extension [User Themes](https://extensions.gnome.org/extension/19/user-themes/) to apply your changes.

Find some themes here ([Pling](https://www.pling.com/browse?cat=134&ord=latest)), though I personally recommend [vinceliuice](https://github.com/vinceliuice)'s themes. They mostly fit the criteria and are decent looking.

I don't use an icon theme because they never really provide enough icons and it feels like an unnecessary change. Adwaita doesn't even look that bad.

A custom system font may be a good idea. I use JetBrains Mono (install using `sudo dnf install jetbrains-mono-fonts`).

## Mutter Triple-buffering

Install a version of `Mutter` with the triple-buffering patch:

```text
sudo dnf copr enable trixieua/mutter-patched -y
sudo dnf update --refresh
```

Sources:

* <https://gitlab.gnome.org/GNOME/mutter/-/merge_requests/1441>
* <https://copr.fedorainfracloud.org/coprs/trixieua/mutter-patched/>

## Remove GNOME Software (NOT RECOMMENDED)

This is probably not a good idea since it allows discovering new apps, and installing stuff is much easier with it, but I simply don't like how it auto-starts and runs in the background, and uses a decent amount of resources. This is only specific to my setup, though.

```text
sudo dnf rm gnome-software
```
