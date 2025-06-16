# GNOME Setup

## Replace GNOME Totem with mpv

Totem is GNOME's default video player. It's not bad, but [mpv](https://mpv.io/) is just better.

```text
sudo dnf swap totem mpv
```

To get hardware acceleration on it: <https://wiki.archlinux.org/title/Mpv#Hardware_video_acceleration>  
Make sure you set up [RPMFusion](SYSTEM.md#enable-rpmfusion) already.

## Replace GNOME System Monitor

GNOME System Monitor looks out of place with the rest of the system (or so I think). You might want to replace it.

### (with) htop

[`htop`](https://htop.dev/) is a lightweight system monitor **for the terminal.**

```text
sudo dnf swap gnome-system-monitor htop
```

### (with) Resources

If you want something graphical, you can use something like [Resources](https://github.com/nokyan/resources).

```text
sudo dnf rm gnome-system-monitor
flatpak install flathub net.nokyan.Resources
```

## Remove unused GNOME apps

These apps remain unused for me, at least. Feel free to keep whichever ones you need.

Cheatsheet:
> **rhythmbox:** a music player  
> **gnome-connections**: allows you to connect to and use other desktops  
> **gnome-contacts**: keeps and organizes contact information  
> **evince**: document viewer (PDF, DjVu, etc.)
> **gnome-tour**: a guided tour and greeter for GNOME  
> **simple-scan**: makes a digital copy of your photos and documents

```text
sudo dnf rm rhythmbox gnome-connections gnome-contacts evince gnome-tour simple-scan
```

If you're not doing office work, remove LibreOffice:

```text
sudo dnf rm "libreoffice-*"
```

## (Install) GNOME Tweaks

GNOME Tweaks allows (proper) configuring of system fonts, themes, mouse, touchpad and keyboards, enabling titlebar buttons, etc. It's likely some functionality you didn't find the in the native installation is in it, thus proving itself essential to any desktop with GNOME.

```text
sudo dnf install gnome-tweaks
```

## Extensions

Install [Extension Manager](https://flathub.org/apps/com.mattjakeman.ExtensionManager):

```text
flatpak install flathub com.mattjakeman.ExtensionManager
```

Pick some extensions: <https://extensions.gnome.org/#sort=downloads> (you can also browse in the Extension Manager app)

You can't live without [Just Perfection](https://extensions.gnome.org/extension/3843/just-perfection/).

## Theming

I think GNOME is quite limited in regard to theming. That said, I don't find it that much of a necessity since the desktop already looks decent. If you still want to spice some things up, then...

As a prerequisite, every GTK theme you pick should support GNOME Shell / libadwaita / GTK4 theming. You need this in order to have a consistent looking system. Make sure you install the extension [User Themes](https://extensions.gnome.org/extension/19/user-themes/) to apply your changes.

Find some themes here ([Pling](https://www.pling.com/browse?cat=134&ord=latest)), though I personally recommend [vinceliuice](https://github.com/vinceliuice)'s themes. They mostly fit the criteria and are decent looking.

I don't use an icon theme because they never really provide enough icons and it feels like an unnecessary change. Adwaita doesn't even look that bad.

A custom system font may be a good idea. I use JetBrains Mono (install using `sudo dnf install jetbrains-mono-fonts`).

## Remove GNOME Software (NOT RECOMMENDED)

***I*** was annoyed by how it just auto-started, ran in the background and use a fair amount of system resources. If you don't mind or your machine is any decent, then keep it. It usually proves quite useful, especially for a Linux newbie.

```text
sudo dnf rm gnome-software
```
