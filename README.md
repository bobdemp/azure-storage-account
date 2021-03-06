# azure-storage-blob
Information on Azure Blob Storage

-------
Video
-------

AZ-900 Episode 11 | Azure Storage Services | Blob, Queue, Table, Files, Disk and Storage Tiers

https://www.youtube.com/watch?v=_Qlkvd4ZQuo

-------
What is the structure of Blob?
-------

Account → Container → Blob

Blob Storage is relatively intuitive and similar to a traditional file structure: directory>subdirectory>file schema. Each Azure Blob Storage account can contain an unlimited number of containers, and each container can contain an unlimited number of blobs. People often think of the container as the directory in the above example, and try to create folders within the containers to replicate a traditional structure, producing a virtual file structure. However, it is better to think of the container as the subdirectory from above and the account itself as the directory. To avoid unnecessary complications, try to make the files as flat as possible without virtual subdirectories.

-------
What are the types of blobs?
-------

Block Blobs: Optimized for large 'blocks' of data and identified by a single block ID, a block blob can hold 50k blocks.

Page Blobs: Collections of 512-byte pages optimized for read/write operations.

Append Blobs: Composed of block blobs optimized for append operations, new blocks are added to the end of the blob. Updating/deleting are not supported.


-------
What are the storage tiers?
-------

Azure also provides the option to customize storage options based on the purpose of the storage through different tiers. Currently, Microsoft offers three different storage tiers: Hot, Cool, and Archive.

Hot Access Tier
This tier is used for storing objects that are actively and consistently read from and written to. The access costs for this tier are the lowest among the tiers, however the storage costs are the highest. Generally, once frequent access to the data is no longer necessary, the data should be migrated to a different tier.

Cool Access Tier
Conversely, the cool access tier has higher access costs and lower storage costs than the hot access tier. This is meant for data that is no longer frequently used but users need immediate access should the need arise. Data in this tier should be expected to remain for at least 30 days.

Archive Access Tier
This tier has the cheapest storage cost and the highest access cost of the tiers. Microsoft expects that data placed in this tier will persist for at least 180 days and the account will incur an early deletion charge if the data is removed prior to 180 days. Data in this tier is not immediately available: Microsoft takes these objects offline and you will not be able to read or modify them. In order to access objects in this tier, you must first 'rehydrate' them, which is basically Microsoft's terminology for moving the object back to an online tier such as cool or hot access.

Here is a quick graph to help picture how the access tiers are utilized:

![image](https://user-images.githubusercontent.com/38502893/169266415-27757d07-15f5-44e6-a413-58ca9711d63d.png)

The Y axis is how often the data needs to be accessed, while the X axis represents the length of time the data needs to be retained. The 'Hot' access tier is accessed often but is not required to be static very long, while the 'Cool' tier is not expected to be accessed often but is expected to remain available for 30-180 days, and finally the 'Archive' tier is not expected to be accessed outside of an anomaly.

-------
Flat listing versus hierarchical listing
-------

https://docs.microsoft.com/en-us/azure/storage/blobs/storage-blobs-list?tabs=dotnet#flat-listing-versus-hierarchical-listing

Blobs in Azure Storage are organized in a flat paradigm, rather than a hierarchical paradigm (like a classic file system). However, you can organize blobs into virtual directories in order to mimic a folder structure. A virtual directory forms part of the name of the blob and is indicated by the delimiter character.

To organize blobs into virtual directories, use a delimiter character in the blob name. The default delimiter character is a forward slash (/), but you can specify any character as the delimiter.

If you name your blobs using a delimiter, then you can choose to list blobs hierarchically. For a hierarchical listing operation, Azure Storage returns any virtual directories and blobs beneath the parent object. You can call the listing operation recursively to traverse the hierarchy, similar to how you would traverse a classic file system programmatically.
