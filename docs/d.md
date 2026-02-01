# Partition Alignment

As you create partitions, you will see that different utilities have different defaults. Some of this is very historical. Long ago, we needed to understand the actual geometry of hard disks and understand the cylinders, heads and sectors (CHS) we were using. In fact, we used to put this information into the BIOS so the system could correctly operate the hard drive. None of this has really been the case since CHS was abandoned in favour of _logical block addressing_ (LBA) in the 1990s. The values in the ATA CHS registers have no connection to the underlying topology of a modern disk. Look up _zoning_, there are not a fixed number of sectors per track! Alignment to track/cylinder boundaries is not required but is still commonly enforced.

All my old Linux examples had disk drives with 63 sectors per track and the Linux partition utility __fdisk__ started the first partition on sector 63; track alignment. But this means all the old examples have partitions aligned to an odd number.

From c. 2009 we moved from 512b to 4,096b sectors and the correct alignment for performance is a 4KB alignment, almost all block operations are in quanta of 4KB. Different authorities give figures for performance penalties should you get this wrong, but I have seen claims as much as x25.

Most modern tools use a 1MB alignment and start at sector 2048 * 512 = 1,048,576, this also works fine with 4KB sectors as 256 * 4096 = 1,048,576.