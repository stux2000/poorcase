# Introduction #

Generally when you are working with a disk image, it is likely more than 4 separate files.  The linux kernel by default only registers four loopback devices, /dev/loop0 through /dev/loop3.  Below will describe a number of methods to create additional devices manually, and have them show up automatically on the next reboot.

# Details #

## Default on Boot ##

With a kernel paramater, you can set the default number of devices the kernel will make available.

> `max_loop=255`

This will set the default created loopback devices to 255.

## Manually by Hand ##

There are two programs that can be used to create devices in /dev.

  * `/dev/MAKEDEV` - a shell script
  * `/sbin/mknod` - a binary executable

### MAKEDEV ###

MAKEDEV is a script that has some smarts to it that wraps the /sbin/mknod executable and lets you specify devices to be created by name.

  * `/dev/MAKEDEV /dev/loop4`

That will create a single device, the 5th loopback device.

If you want to create more, use a shell one-liner:

  1. `for foo in` ``````seq 0 255` ``````; do /dev/MAKEDEV /dev/loop$foo;done`

That will create all 255 possible /dev/loop devices.

### mknod ###

mknod requires a little more knowledge of the types of devices you are creating.  mknod can be used to create device nodes, sockets, etc.  mknod accepts four arguments

  * name (the name of the file to create in /dev)
  * type (block, character, socket)
  * major (a number, associated with a kernel "subsystem" such as loop)
  * minor (a number, associated with the Nth instance of a the subsystem)

  * `mknod /dev/loop0 b 7 0`

  * `for foo in` ``````seq 0 255` ``````; do mknod /dev/loop$foo b 7 $foo;done`