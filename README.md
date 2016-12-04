# mkeosimg

Your EdgeRouter's internal USB drive died, and you don't have a spare
couple hours to figure out how TFTP works. Run this script instead *on
your nearest Linux machine* and generate a .img that you can dd straight
to a new USB drive.

# Usage

* If you have a backup config file such as
  edgeos_routername_NNNNNNNN.tar.gz, copy it into this directory and
  rename it `edgeos_config.tar.gz`.

* `sudo ./mkeosimg ER-e100.v1.xxxxxxx.tar` (you downloaded that file
  from the [Ubiquiti](https://www.ubnt.com/) site. Pick the latest
  system update for your router).

* Download the resulting .img if you built this elsewhere (such as on
  a Google Compute Engine instance that you spun up just for this
  project). You should have gzipped it because that'll make it around
  20x smaller.

* `sudo dd if=ER-e100.v1.xxxxxxx.img of=/dev/path/to/usb/drive bs=1M`
  (adapt to your OS of choice).

* Insert the new USB drive into your router and boot it up. If you
  included your backup config in the first step, then your router will
  start shuttling around packets on your network just like it used to;
  otherwise you'll have to set it up as a brand-new device.

Inspired by
https://github.com/vyos/emrk/blob/master/bin/emrk-reinstall. Some parts
of the code were stolen from there as well.

Beware! There are lots of things out there that call themselves "EMRK"
and succeed to varying degrees in helping with EdgeRouter unbricking.
