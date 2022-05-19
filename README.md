# azure-storage-blob
Information on Azure Blob Storage

-------
What is the structure of Blob?
-------

Account → Container → Blob

Blob Storage is relatively intuitive and similar to a traditional file structure: directory>subdirectory>file schema. Each Azure Blob Storage account can contain an unlimited number of containers, and each container can contain an unlimited number of blobs. People often think of the container as the directory in the above example, and try to create folders within the containers to replicate a traditional structure, producing a virtual file structure. However, it is better to think of the container as the subdirectory from above and the account itself as the directory. To avoid unnecessary complications, try to make the files as flat as possible without virtual subdirectories.
