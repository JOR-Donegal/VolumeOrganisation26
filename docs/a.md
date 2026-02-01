# MBR

My first hard disk was a staggeringly big 32 megabytes, sometime around 1988, on an Amstrad 1512. At that stage, I could hack floppy discs and took great pleasure going into programmes with a hex editor, completely changing how they looked. But this first hard drive was too big to format like a floppy disk and for the first time, I has to figure out partitioning a disk.

The partitioning scheme introduced in 1983 was called _Master Boot Record_ or MBR. This allowed for up to four separate partitions, each independent and with its own file system. In MBR the first sector of the hard drive is no longer part of a file system, instead it contains meta-data describing the partition layout of the entire physical drive.

<figure>
<img src = "https://jor-donegal.github.io/VolumeOrganisation26/images/fig1.png">
<figcaption>Fig 1. MBR, first sector.</figcaption>
</figure>

The first 445 bytes of sector 1 contains _bootstrap_ code. The term bootstrap means for a system to start itself up or "pull itself up by its own bootstraps". For the system to work, one of the partitions must be _bootable_, it must be able to load an operating system (OS). The _boot loader_ determines which partition is to be booted from and then chain loads the volume boot record from that partition’s sector 1. If the boot partition was FAT (explained in later notes!), the first three bytes are a jump command and the system would proceed to boot from this partition.

<figure>
<img src = "https://jor-donegal.github.io/VolumeOrganisation26/images/fig2.png">
<figcaption>Fig 2. MBR, partitions.</figcaption>
</figure>

MBR allowed for up to four separate partitions, each independent and with its own file system. 

To get by the limit of four partitions, the concept of the primary partition and the extended partition were implemented. All primary partitions are defined in sector one of the hard drive. If we define one partition as being an extended partition, we can put a partition table inside the partition and pretend it’s a disk. If it’s a disk we can create partitions inside of it and one of these could be an extended partition, which we could pretend was a disk….and so on ad infinitum, ad absurdum!

If anyone has ever come up with a more inelegant way of fixing a problem, I have yet to find it. MBR was messy and limited. A maximum of 2^32^ Logical Block Addresses (LBA) gave a maximum addressable space of 2^32^ x 512 or 2TB.