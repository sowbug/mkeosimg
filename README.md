# mkeosimg

Your EdgeRouter's internal USB drive died, and you don't have a spare
couple hours to figure out how TFTP works. Run this script instead *on
your nearest Linux machine* and generate a .img that you can dd straight
to a new USB drive.

If you want to create a USB boot drive directly, use `./mkeosdrive` instead.

# Usage

* `sudo ./mkeosimg ER-e100.v1.xxxxxxx.tar` (you downloaded that file
  from the [Ubiquiti](https://www.ui.com/download/edgemax) site. Pick
  the latest system update for your router).

* If you have a backup config file that you'd like to include, such as
  edgeos_routername_NNNNNNNN.tar.gz, just provide the path to it as the
  second parameter.

* If you want to use more of the available space on a larger flash drive,
  you can enter the total image size in GB as the third parameter.
  If you don't want to provide a config file, but still want to have a
  larger image, use "-" (without the quotes) as the second parameter.
  If no drive size is specified, the script will default to 2 GB.

* Download the resulting .img if you built this elsewhere (such as on
  a Google Compute Engine instance that you spun up just for this
  project). You should have gzipped it because that'll make it around
  20x smaller.

* `sudo dd if=ER-e100.v1.xxxxxxx.img of=/dev/path/to/usb/drive bs=1M`
  (adapt to your OS of choice) to write the image to your USB drive.

* If you want, you can directly create a USB drive without creating an
  image file first. Use `./mkeosdrive` instead, and supply the target
  device as the first parameter. All other parameters are shifted by one
  position accordingly.

  `sudo ./mkeosdrive /dev/path/to/usb/drive ER-e100.v1.xxxxxxx.tar`

* Insert the new USB drive into your router and boot it up. If you
  included your backup config in the first step, then your router will
  start shuttling around packets on your network just like it used to;
  otherwise you'll have to set it up as a brand-new device.

# Troubleshooting

* Did everything, but router's still not booting? Your USB drive might
  be on the slow side. See [issue
  #7](https://github.com/sowbug/mkeosimg/issues/7) for more detail,
  and thanks [@kosta](https://github.com/kosta) for filing the issue.

# Credits and Miscellaneous

Inspired by
https://github.com/vyos/emrk/blob/master/bin/emrk-reinstall. Some parts
of the code were stolen from there as well.

Beware! There are lots of things out there that call themselves "EMRK"
and succeed to varying degrees in helping with EdgeRouter unbricking.
