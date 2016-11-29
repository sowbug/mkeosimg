# mkeosimg

Your EdgeRouter's internal USB drive died, and you don't have a spare
couple hours to figure out how TFTP works. Run this script instead and
generate a .img that you can dd straight to a new USB drive.

# Usage

* If you have a backup config file such as
  edgeos_routername_NNNNNNNN.tar.gz, copy it into this directory and
  rename it `edgeos_config.tar.gz`.

* `sudo ./mkeosimg ER-e100.v1.xxxxxxx.tar` (you downloaded that file
  from the [Ubiquiti](https://www.ubnt.com/) site).

* Download the resulting .img if you built this elsewhere (such as on
  a Google Compute Engine instance that you spun up just for this
  project). You should have gzipped it because that'll make it around
  20x smaller.

* `sudo dd if=ER-e100.v1.xxxxxxx.img of=/dev/path/to/usb/drive bs=1M`
  (adapt for your OS of choice).

* Insert the new USB drive into your router and boot it up.

Inspired by
https://github.com/vyos/emrk/blob/master/bin/emrk-reinstall.
