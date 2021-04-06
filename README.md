# hid-mapper-pkg
 PKGBUILD for hid_mapper

hid_mapper connects usb hid devices to linux /dev/input/event*.

This package combines the latest hid_mapper patches with a systemd service
file, udev rules and hwdb files. It was written principally to allow usb ir
receivers, originally designed by Philips/NXP, to be used as a remote control
for vdr (http://www.tvdr.de/).

Examples of the remote control transmitters are RC1974505 from Olidata
(sold by Pollin Electronic GmbH) and the remote control provided with the
ZOTAC ZBOX.

There are two slightly different receivers, which look identical (small
black tower) but have distinct idProduct attributes (0471:0613 and 0471:20cc).
However, they both respond to the same codes (RC6A).
