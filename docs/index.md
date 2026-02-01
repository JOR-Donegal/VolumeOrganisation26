# Introduction

!!! abstract "Volume Organisation"

Only a generation ago, hard disks appeared as the miraculously fast and infinitely large solution to all storage problems. Little did we know…..!

The earliest problems we had related to the crude and limited early file systems we used. The restrictions on these file systems meant we had to partition disks into volumes suited to our requirements; break them up into different logical sections so it appeared that we had multiple physical disks. In these notes, we will look at the original way we did that (MBR) and the current method (GPT).

As our storage needs grew, cases existed where we needed to aggregate small disks to create logical volumes larger than we could physically. This concept is the basis for many of the approaches we take in enterprise and data centre storage. Most operating systems include some sort of _logical volume manager_ or LVM which allows us to abstract the old, crude, inflexible concepts of partitions into something more closely aligned with modern OS requirements.

We need to understand the principles behind both approaches, where they are used and why.