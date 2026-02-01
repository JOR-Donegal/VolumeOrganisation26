# GPT
MBR is old and was written for the computers of another era. The problems of MBR were not readily resolvable and an entire new standard was developed.

_Global Unique Identifiers_ (GUID) are unique identifiers which are so large that a collision (two systems with the same GUID) is not feasible. GUIDs are typically 128 bits long and are represented by 32 hexadecimal characters. The _GUID Partition Table_ (GPT) standard uses these identifiers and GPT is part of UEFI specification, which replaces the older BIOS used as the lowest software layer in PC computers.

GPT is more suited to modern requirements.

- It can address 2^64^ Logical Block Addresses (LBAs)
- It can accommodate up to 128 partitions with no extended partitions
- The GUIDs provide unique disk labelling
- It includes for meta-data backup and integrity checking

<figure>
<img src = "https://jor-donegal.github.io/VolumeOrganisation26/images/fig3.png">
<figcaption>Fig 3. GPT overview.</figcaption>
</figure>

To protect the disk, a legacy MBR header exists at LBA 0. This shows the whole disk as being a single partition of type 0xEE. Any operating system which cannot read GPT should just show the disk as being of an unrecognizable type and ignore it.

<figure>
<img src = "https://jor-donegal.github.io/VolumeOrganisation26/images/fig4.png">
<figcaption>Fig 4. Protective MBR.</figcaption>
</figure>

_Logical Block Address_ (LBA) 1 contains the real header for the GPT disk.

<figure>
<img src = "https://jor-donegal.github.io/VolumeOrganisation26/images/fig5.png">
<figcaption>Fig 5. GPT Header.</figcaption>
</figure>

An 8 byte signature “EFI PART” marks the start of the header and basic meta data relating to the header itself follows.  The location of this header and the backup header are both defined. This will normally be the second sector of the disk (LBA 1) and the last. The start and end of the partitions is given. A 16 byte unique ID for the disk is specified.  The start of the partition table is stated, as are the number of entries and their size.

<figure>
<img src = "https://jor-donegal.github.io/VolumeOrganisation26/images/fig6.png">
<figcaption>Fig 6. Start of header.</figcaption>
</figure>

The partition table entries are 128 bytes long.
Each type of partition has a GUID associated with it, this is the first 16 bytes.
Each partition then has its own unique GUID.
The start and end LBA of the partition is defined.
64 bits are available for attribute flags, many of these are as yet undefined.
Finally 72 bytes are available for partition name; using UTF-16, this gives a 36 character name.