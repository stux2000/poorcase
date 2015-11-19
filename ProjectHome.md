Poorcase is a perl script that takes all the dirty work of virtually reconstructing a "dd 4g" split disk image back into something more friendly under a Linux operating system.

It supports both read-write and read-only mode, and does not require you to concatenate the split disk image together yourself -- this is all done using Device Mapper, partx, and loopback devices.

(I use this to decrypt "whole disk encryption" through a virtual machine booted from a "universal boot cd" with the encryption software pre-packaged, along with the recovery key)

Changelog:

  * V1.1: Additional error checking when creating partition tables
  * v1.0: Initial release