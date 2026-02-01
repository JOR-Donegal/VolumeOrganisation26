# Virtualizing Storage

Most operating system implement some form of _logical volume manager_ to abstract the storage from the requirements of the operating system. A physical volume (PV) used to be a hard drive, but on a modern system it could be a partition, or it could be a concatenation of drives. It could also be presented as a logical unit number (LUN) of a remote storage array.

The physical volume will probably store data in sectors but these sectors are normally too small for optimal usage by the operating system. Sectors will be aggregated into blocks and blocks might be aggregated into _physical extents_ (PE), a contiguous area of storage.

The PEs aggregate to form a _volume group_ or VG. Volume groups can be resized dynamically by adding new PVs.

<figure>
<img src = "https://jor-donegal.github.io/VolumeOrganisation26/images/fig7.png">
<figcaption>Fig 7. Extents.</figcaption>
</figure>

The OS will be presented with _logical extents_ (LEs). These may map directly to PEs or more complex arrangements may exist. For example, we sometimes mirror data to two disks for high availability. In this case, we might have a single LE map to two discrete PEs on separate PVs. Virtual partitions can be created from LEs called _logical volumes_ or LVs.

LVs can be expanded by adding new LEs to them.

LVs can be moved from PV to PV as required.

<figure>
<img src = "https://jor-donegal.github.io/VolumeOrganisation26/images/fig8.png">
<figcaption>Fig 8. Hierarchy.</figcaption>
</figure>

Software RAID allows us to make some very beneficial use of this flexibility.