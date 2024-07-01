# Lenovo Yoga Pro 9i generation 9 (2024) -- 16IMH9

[Official documentation and technical specifications reference page.](https://psref.lenovo.com/Product/Yoga/Yoga_Pro_9_16IMH9)

This repository holds documentation about adaptation and configuration of the Lenovo Yoga Pro 9i predominantly with focus on GNU/Linux.

It's a complementation on repositories:

* <https://github.com/karypid/YogaPro-16IMH9>
* <https://github.com/maximmaxim345/yoga_pro_9i_gen9_linux>
* <https://github.com/thiagotei/linux-realtek-alc287>

## Configuration

The machine used was with following configuration:

* Intel Core Ultra 9 185H
* NVIDIA GeForce RTX 4070 Laptop GPU
* 64GB soldered memory, not upgradable
* 6 stereo speakers, 2W x4 (dual side woofers), 2W x2 (tweeters), optimized with Dolby Atmos, Smart Amplifier (AMP)
* 16" 3.2K (3200x2000) Mini LED SDR 600nits / HDR 1,200nits Anti-glare 16:10 SDR 1,200:1 / HDR 1,000,000:1 100% P3, 100% Adobe RGB, 100% sRGB 165Hz (Max) EyesafeÂCertified 2.0, Dolby Vision, VESA DisplayHDR 1000, TCON

<!--
### Chipsets

| Chipset | Functionality | Comments |
| :------ | :------------ | :------- |
| Realtek ALC287 | | |
/-->

# GNU/Linux

## Distributions

* [KDE neon](https://neon.kde.org/) hangs after GRUB with 20240618 images. Likely using too old kernel to deal with the CPU.
* [openSUSE Tumbleweed](https://get.opensuse.org/tumbleweed/) did get to the installer, but couldn't start a live session.
* [Ubuntu Server 24.04 LTS](https://ubuntu.com/download/alternative-downloads) installed, but could not use wireless device during installation process.
* [Arch Linux](https://archlinux.org/) booted.

## Audio

* There are glitches in sound and unresponsibe behaviour especially when switching between sound profiles, what Ubuntu 24 labels `Play HiFi quality Music` and `Pro Audio` (16 bit@44.1 kHz and 24 bit@48 kHz respectively). Windows has the same problem it seems, it also does not happend on the fly and without glitches.
* Glitches in playback seem to be related to timing issues and typically can stop when the audio device goes down into power saving mode, ergo when the sound playback stops.
* Running kernel versions 6.8, 6.10 with OEM variants from Ubuntu helps a bit, meaning 6.8 had the issues on regular basis, while 6.10 much less.
* Setting CPU in `performnace` mode/governor, as in help keeping a stable frequency, does not help either.

### Speakers

Script `lenovo-yoga-pro-9i-16imh9--speakers-setup` and service definition `lenovo-yoga-pro-9i-16imh9--speakers-setup.service` will setup the speaker system after sound hardware initialization.

```bash
# install -m 755 lenovo-yoga-pro-9i-16imh9--speakers-setup /usr/local/bin/
# cp -v lenovo-yoga-pro-9i-16imh9--speakers-setup.service /etc/systemd/system/
# systemctl daemon-reload
# systemctl enable --now lenovo-yoga-pro-9i-16imh9--speakers-setup.service
```

The script is a [cleaned up version of Maxim's] based on what shows up in [kernel discussion](https://bugzilla.kernel.org/show_bug.cgi?id=217449).

<!--
### Headphones
## Monitor
### Color profiles
### HDR
## Network
## Performance
## Battery
--/>
