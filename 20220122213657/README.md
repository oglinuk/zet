# TIL `sfdisk`

`fdisk` is the usual goto tool for partitioning a device, but it has the
limitation of being only interactive. Today I learned about `sfdisk`,
which "is a script-oriented tool for partitioning any block device."

```
DESCRIPTION
       sfdisk is a script-oriented tool for partitioning any block device.

       Since  version  2.26  sfdisk supports MBR (DOS), GPT, SUN and SGI disk labels, but no longer provides any functionality for CHS (Cylinder-Head-Sector) addressing.  CHS has never been important
       for Linux, and this addressing concept does not make any sense for new devices.

       sfdisk (since version 2.26) aligns the start and end of partitions to block-device I/O limits when relative sizes are specified, when the default values are used or  when  multiplicative  suf‐
       fixes (e.g. MiB) are used for sizes.  It is possible that partition size will be optimized (reduced or enlarged) due to alignment if the start offset is specified exactly in sectors and parti‐
       tion size relative or by multiplicative suffixes.

       The recommended way is not to specify start offsets at all and specify partition size in MiB, GiB (or so).  In this case sfdisk align all partitions to block-device I/O  limits  (or  when  I/O
       limits  are too small then to megabyte boundary to keep disk layout portable).  If this default behaviour is unwanted (usually for very small partitions) then specify offsets and sizes in sec‐
       tors.  In this case sfdisk entirely follows specified numbers without any optimization.

       sfdisk does not create the standard system partitions for SGI and SUN disk labels like fdisk(8) does.  It is necessary to explicitly create all partitions including  whole-disk  system  parti‐
       tions.

       sfdisk  uses  BLKRRPART  (reread  partition table) ioctl to make sure that the device is not used by system or another tools (see also --no-reread).  It's possible that this feature or another
       sfdisk activity races with udevd.  The recommended way how to avoid possible collisions is to use exclusive flock for the whole-disk device to serialize device access.  The exclusive lock will
       cause udevd to skip the event handling on the device.  For example:

              flock /dev/sdc sfdisk /dev/sdc

       Note, this semantic is not currently supported by udevd for MD and DM devices.

EMPTY DISK LABEL
       sfdisk  does not create partition table without partitions by default. The lines with partitions are expected in the script by default. The empty partition table has to be explicitly requested
       by "label: <name>" script header line without any partitions lines. For example:

              echo 'label: gpt' | sfdisk /dev/sdb

       creates empty GPT partition table. Note that the --append disables this feature.

BACKING UP THE PARTITION TABLE
       It is recommended to save the layout of your devices.  sfdisk supports two ways.

       Use the --dump option to save a description of the device layout to a text file.  The dump format is suitable for later sfdisk input.  For example:

              sfdisk --dump /dev/sda > sda.dump

       This can later be restored by:

              sfdisk /dev/sda < sda.dump

       If you want to do a full (binary) backup of all sectors where the partition table is stored, then use the --backup option.  It writes the sectors to ~/sfdisk-<device>-<offset>.bak files.   The
       default  name  of  the backup file can be changed with the --backup-file option.  The backup files contain only raw data from the device.  Note that the same concept of backup files is used by
       wipefs(8).  For example:

              sfdisk --backup /dev/sda

       The GPT header can later be restored by:

              dd  if=~/sfdisk-sda-0x00000200.bak  of=/dev/sda  \
                seek=$((0x00000200))  bs=1  conv=notrunc

       Note that sfdisk since version 2.26 no longer provides the -I option to restore sectors.  dd(1) provides all necessary functionality.

AVAILABILITY
       The sfdisk command is part of the util-linux package and is available from https://www.kernel.org/pub/linux/utils/util-linux/.
```

Related:

* `man sfdisk`

Tags:

	#partitioning #essential-command #automation #scripting
