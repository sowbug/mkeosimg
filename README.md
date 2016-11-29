# mkeosimg

Your EdgeRouter's internal USB drive died, and you don't have a spare couple hours to figure out how TFTP works. Run this script instead and generate a .img that you can dd straight to a new USB drive.

# Usage

* `sudo mkeosimg ER-e100.v1.xxxxxxx.tar`
* Download the resulting .img.gz if you built this elsewhere, or gunzip it
* `sudo dd if=ER-e100.v1.xxxxxxx.tar of=/dev/path/to/usb/drive bs=1M` (adapt for your OS of choice)
* Insert the new USB drive into your router, boot it up, and reconfigure.

# TODO

* Integrate a config backup into the restored image so you don't have to waste time with patch cables on 192.168.1.100.

Inspired by https://github.com/vyos/emrk/blob/master/bin/emrk-reinstall.
