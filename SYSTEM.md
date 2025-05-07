# System Setup

## ToC

- [System Setup](#system-setup)
  - [ToC](#toc)
  - [Enable RPMFusion](#enable-rpmfusion)
  - [NVIDIA 101](#nvidia-101)
  - [Disable Chrome and PyCharm repositories](#disable-chrome-and-pycharm-repositories)
  - [Enable Intel GuC and HuC and Framebuffer compression (Intel only)](#enable-intel-guc-and-huc-and-framebuffer-compression-intel-only)
    - [Verify if it's working](#verify-if-its-working)
  - [Enable Flathub](#enable-flathub)
  - [Theme and/or change your shell](#theme-andor-change-your-shell)
  - [Replace tuned with auto-cpufreq](#replace-tuned-with-auto-cpufreq)
  - ["No more blurry fonts"](#no-more-blurry-fonts)
  - [Install micro](#install-micro)
  - [Speed up DNF](#speed-up-dnf)
  - [Capslock Delay Fix](#capslock-delay-fix)
  - [What else?](#what-else)
    - [Educate yourself](#educate-yourself)
    - [(Install) some cools apps](#install-some-cools-apps)
    - [Install a custom kernel (completely optional)](#install-a-custom-kernel-completely-optional)

## Enable RPMFusion

In order to get hardware acceleration, proprietary video codecs and some closed-source apps.

Install free and non-free repos:  
<https://rpmfusion.org/Configuration#Command_Line_Setup_using_rpm>

Afterwards, set up multimedia:  
<https://rpmfusion.org/Howto/Multimedia>

You might want to update your system at this point.

```text
sudo dnf offline-upgrade download
sudo dnf offline-upgrade reboot
```

## NVIDIA 101

Refer to <https://rpmfusion.org/Howto/NVIDIA>.

## Disable Chrome and PyCharm repositories

```text
sudo dnf config-manager setopt google-chrome.enabled=0 copr:copr.fedorainfracloud.org:phracek:PyCharm.enabled=0
```

## Enable Intel GuC and HuC and Framebuffer compression (Intel only)

Add kernel parameters to load GuC and HuC (contrary to popular belief, they are not enabled by default except on Intel gen12+ platforms in the kernel) by running the following:

```text
sudo nano /etc/modprobe.d/i915.conf
```

and paste the following into it:

```text
options i915 enable_guc=3
options i915 enable_fbc=1
```

Save and close.  
Then rebuild your `initramfs` with:

```text
sudo dracut --force
```

Then reboot (important).

### Verify if it's working

Running

```text
sudo dmesg | grep guc 
```

Should return something like `GuC firmware i915/tgl_guc_62.0.0.bin version 62.0 submission:enabled`

```text
sudo dmesg | grep huc 
```

Should return something like `HuC firmware i915/tgl_huc_7.9.3.bin version 7.9 authenticated:yes`

Sources:

1. <https://discussion.fedoraproject.org/t/intel-graphics-best-practices-and-settings-for-hardware-acceleration/69944#h-4-enable-intel-guc-and-huc-and-framebuffer-compression-5>  
2. <https://wiki.archlinux.org/title/Intel_graphics#Enable_GuC_/_HuC_firmware_loading>

## Enable Flathub

```text
flatpak remote-add --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo
```

## Theme and/or change your shell

Pick between `fish`, `zsh`, `bash`. I'd personally go with `fish` for the user-friendliness and other stuff.

Pick your theme. I personally use [Tide](https://github.com/IlanCosman/tide). Some people like [Starship](https://starship.rs/). Do some research.

## Replace tuned with auto-cpufreq

`tuned` provides the Balanced, Performance, Powersave power profiles in GNOME. I don't like it.

```text
git clone https://github.com/AdnanHodzic/auto-cpufreq.git
cd auto-cpufreq && sudo ./auto-cpufreq-installer
```

Afterwards, install the daemon with the graphical app.

## "No more blurry fonts"

<https://blog.aktsbot.in/no-more-blurry-fonts.html>

## Install micro

If you're too stupid to use `vim`, but also too smug to use `nano`, use [micro](https://micro-editor.github.io/).

## Speed up DNF

You'll preferably want the maximum amount of parallel downloads (20) if you have a good bandwidth, and if Fedora can't pick out actually decent mirrors, then enable `fastestmirror` (though I can't guarantee an improvement).

```text
sudo $EDITOR /etc/dnf/dnf.conf
```

Have the file look a bit like this:

```text
[main]
max_parallel_downloads=20
fastestmirror=True
```

## Capslock Delay Fix

If you're someone who uses Capslock instead of Shift (like me), you've likely run into an issue where capslock disables too late and results in text like "HEllo WOrld".

Here's the fix:

<https://forum.manjaro.org/t/caps-lock-behaviour-wayland/79868/8>

## What else?

### Educate yourself

Extensively read [why privacy matters](https://www.privacyguides.org/en/basics/why-privacy-matters/) and always utilize some
[privacy tools](https://www.privacyguides.org/en/tools/).

Ideally, get a secure encrypted DNS resolver. I use NextDNS. [Set it up.](https://github.com/yokoffing/NextDNS-Config)

### (Install) some cools apps

- [Flatseal](https://flathub.org/apps/com.github.tchx84.Flatseal)
- [Warehouse](https://flathub.org/apps/io.github.flattool.Warehouse)
- [Main Menu](https://flathub.org/apps/page.codeberg.libre_menu_editor.LibreMenuEditor)

All from the [Flathub](https://flathub.org/).

### Install a custom kernel (completely optional)

Install a more optimized kernel, for the sake of it. For example, the [CachyOS Kernel](https://copr.fedorainfracloud.org/coprs/bieszczaders/kernel-cachyos).

Also check out the [add-ons repository](https://copr.fedorainfracloud.org/coprs/bieszczaders/kernel-cachyos-addons/) where you can install `uksmd`, sched-ext schedulers, `ananicy-cpp`, as well the settings used in the CachyOS distribution.
